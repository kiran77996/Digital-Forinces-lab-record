# Experiment - 6
# Use Sleuth Kit to Analyze Digital Evidence

---

## Aim
To understand and demonstrate the usage of Sleuth Kit in analyzing digital evidence for forensic investigation purposes.

---

## Description
The Sleuth Kit (TSK) is a powerful open-source digital forensics toolkit that enables investigators to analyze disk images and recover files. This experiment focuses on using various Sleuth Kit commands and tools to examine digital evidence, recover deleted files, and analyze file system artifacts.

---

## Tools Used
1. The Sleuth Kit (TSK)
2. Command Line Interface
3. Disk Image (for analysis)
4. AutopsyⓇ (GUI frontend for Sleuth Kit)

---

## Procedure

### 1. Installation and Setup
1. Download and install The Sleuth Kit from the official website
2. Verify the installation by running basic commands
3. Prepare a disk image for analysis

### 2. Basic File System Analysis
1. Use `mmls` to display the partition layout
    ```bash
    mmls Evidence.dd
    ```
    Note the Start Sector of the partition (e.g., 2048).

    ![mmls output](https://github.com/Yaswanth767/Digital-Forensics/blob/main/images/Screenshot%202025-10-23%20222452.png?raw=true)

<!-- [Insert Screenshot: Place the screenshot of mmls command output showing partition table] -->

2. Use `fsstat` to examine file system details
    ```bash
    fsstat -o 63 Evidence.raw
    ```
    ![fsstat output](https://github.com/Yaswanth767/Digital-Forensics/blob/main/images/Screenshot%202025-10-23%20222446.png?raw=true)

    <!-- [Insert Screenshot: Place the screenshot showing file system information] -->

### 3. File Recovery and Analysis
1. Use `fls` to list files and directories
    ```bash
    fls -o 63 Evidence.dd
    ```
    ![fls output 1](https://github.com/Yaswanth767/Digital-Forensics/blob/main/images/Screenshot%202025-10-23%20224310.png?raw=true)
    ![fls output 2](https://github.com/Yaswanth767/Digital-Forensics/blob/main/images/Screenshot%202025-10-23%20222608.png?raw=true)
    <!-- [Insert Screenshot: Place the screenshot showing file listing] -->

2. Use `icat` to extract files using their inode numbers and to recover
    ```bash
    icat evidence_disk.dd inode_number > recovered_file
    ```
    ![icat output](https://github.com/Yaswanth767/Digital-Forensics/blob/main/images/Screenshot%202025-10-23%20222954.png?raw=true)

    <!-- [Insert Screenshot: Place the screenshot of file recovery process] -->



<!-- ### 4. Timeline Analysis
1. Create a timeline of file activity
```bash
fls -m "/" evidence_disk.dd > body.txt
mactime -b body.txt > timeline.txt
```
[Insert Screenshot: Place the screenshot showing timeline analysis] -->

<!-- ### 5. Deleted File Recovery
1. Use `ils` to list deleted inodes
```bash
ils evidence_disk.dd
``` -->
<!-- [Insert Screenshot: Place the screenshot showing deleted inodes] -->

### 4. Analyze Metadata
    1. use this command to displays timestamps, size, and allocation info for that file.

    ```bash
    istat -o 63 Evidence 6342-128-4
    ```

---

## Results
The experiment successfully demonstrated:

1. Basic file system analysis capabilities of Sleuth Kit
2. File system structure examination and interpretation
3. Recovery of both active and deleted files
4. Timeline analysis of file system activities
5. Understanding of digital forensics investigation workflow using Sleuth Kit

Key findings included:
- Successfully identified partition structure
- Retrieved file system metadata
- Recovered deleted files
- Created comprehensive timeline of file system activities
- Demonstrated proper digital forensics investigation procedures

---

## Conclusion
The Sleuth Kit proves to be an essential tool in digital forensics investigations, providing detailed insights into file systems and enabling investigators to recover and analyze digital evidence effectively. Through this experiment, we gained practical experience in using various Sleuth Kit commands and understanding their application in real-world forensic scenarios.

---## Experiment No - 06: Use Sleuth Kit to Analyze Digital Evidence

### Description
The **Sleuth Kit (TSK)** is a suite of command-line tools for analyzing disk images and recovering digital evidence. This guide outlines the steps to use TSK on a Windows machine for digital forensics.

---

### Step 1: Install Sleuth Kit

1.  **Download Sleuth Kit:**
    * Visit the official Sleuth Kit website or the provided Google Drive link (https://drive.google.com/drive/u/1/folders/1ilSFY7Tqn2L7AjQGhq8yJ8kixc_xTU-v) and download the latest Windows version.
2.  **Install Sleuth Kit:**
    * Run the installer and follow the instructions to install Sleuth Kit on your Windows machine.

---

### Step 2: Acquire the Disk Image

Before analysis, a **bit-by-bit copy** (disk image) of the storage device evidence is required.

1.  **Create Disk Image:**
    * Use a forensic tool like **FTK Imager** or **dd** to create a bit-by-bit copy.
    * Ensure the image is in a TSK-supported format, such as **.dd**, **.raw**, **.img**, or **.E01**.
2.  **Download Files (for this exercise):**
    * Download the following files from the Google Drive:
        * `4Dell Latitude CPi.E01`
        * `4Dell Latitude CPi.E02`

---

### Step 3: Mount the Disk Image (Optional)

Mounting the disk image simplifies the navigation and analysis of the file system.

1.  **Mount the Image:**
    * Use a tool like **OSFMount** to mount the image as a virtual drive on your Windows system.
    * *Note: This step is optional but can aid in easy file system navigation.*

---

### Step 4: Analyze the File System

Use the Sleuth Kit command-line tools to examine the file system structure and locate evidence.

1.  **Navigate to the Sleuth Kit Directory:**
    * Open the **Command Prompt** (cmd) and use the `cd` command to navigate to the directory where Sleuth Kit is installed (e.g., `C:\Program Files\SleuthKit\bin`).

2.  **Identify File System Type with `fsstat`:**
    * **Command:**
        ```arduino
        fsstat [image file] > filesystem_info.txt
        ```
    * **Purpose:** This command outputs detailed information about the file system, which is crucial for structural understanding.

3.  **List Partitions with `mmls`:**
    * **Command:**
        ```arduino
        mmls [image file] > partitions.txt
        ```
    * **Purpose:** This command lists the partitions present within the image file.

4.  **Analyze File System with `fls`:**
    * **Command:**
        ```arduino
        fls -r [image file] > file_list.txt
        ```
    * **Purpose:** The `-r` flag recursively lists files and directories in the file system, along with their metadata (inode numbers).

5.  **Recover Deleted Files with `icat`:**
    * **Command:**
        ```css
        icat [image file] [inode number] > [output file]
        ```
    * **Purpose:** To extract a specific file, replace `[inode number]` with the inode found from the `fls` output.

---

### Step 5: Analyze Metadata

Extract file metadata to gain insight into a file's history, creation, and usage.

1.  **View Metadata with `istat`:**
    * **Command:**
        ```css
        istat [image file] [inode number] > metadata_info.txt
        ```
    * **Purpose:** Provides detailed information about a file, including **timestamps (MAC times)**, size, and allocation status.

---

### Step 6: Timeline Analysis (Optional)

Creating a timeline of file activity is vital for reconstructing events.

1.  **Generate a Body File using `fls`:**
    * **Command:**
        ```css
        fls -m / -r [image file] > body.txt
        ```
    * **Purpose:** Generates a **body file** (`body.txt`) containing the essential metadata (MAC times, file paths) needed for timeline analysis.

2.  **Create Timeline with `mactime`:**
    * **Command:**
        ```css
        mactime -b body.txt > timeline.txt
        ```
    * **Purpose:** Processes the body file to create a **timeline** (`timeline.txt`) sorted by the Modified, Accessed, and Changed (MAC) times of the files.

---

### Step 7: Generate a Report

Document the findings by compiling all the collected data into a comprehensive report.

1.  **Compile the Data:**
    * Gather all the output files (e.g., `filesystem_info.txt`, `partitions.txt`, `file_list.txt`, `metadata_info.txt`, `timeline.txt`).
2.  **Analyze and Document:**
    * Review the findings, highlight crucial evidence, and write a report summarizing the investigation's methodology and results.

---

### Step 8: Finalize and Store Evidence

Ensure all evidence and reports are securely managed to maintain integrity and follow the chain of custody.

1.  **Archive Evidence:**
    * Use a secure, verifiable method to **archive** the original disk image and the analysis results.
2.  **Store Securely:**
    * Store the archived data in a secure location, strictly adhering to the **chain of custody** procedures.

**Result**
