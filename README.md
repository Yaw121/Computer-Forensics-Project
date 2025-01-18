# Computer-Forensics-Project

<details>
<summary><b>LAB 1 EXPLORING THE WINDOWS FILE SYSTEM</b></summary>

  ### INTRODUCTION

  The Windows New Technology File System (NTFS) file system is commonly used to 
organize and handle functions such as read, write and search on most Windows 
Operating Systems, starting with Windows NT. In this lab, we will explore the NTFS 
system and how to interpret the Master File Table or MFT. 

### OBJECTIVE 
In this lab, I will be conducting forensic practices using various tools. I will be 
performing the following tasks: 
1. Getting Familiar with MFT File Viewer 
2. Identifying Attributes with MFT File Viewer

   1. Getting familiar with MFT File Viewer using the CAINE VM for forensics;
  
   a. Open a new terminal by clicking on the MATE Terminal icon located on the 
  bottom panel and navigate /usr/local/bin directory by typing the command cd /usr/local/bin followed 
  by pressing Enter.
![image](https://github.com/user-attachments/assets/4d1f59af-f085-44e2-8457-90580e964614)

b. Launch the MFT File Viewer application by entering the command below.  
MFTView.py /home/caine/Desktop/Windows\ MFT/MFT

![image](https://github.com/user-attachments/assets/4885c5b8-4c96-4795-934e-4b1b991bac5e)
A new MFT File Viewer screen will appear. 

C. Expand the MFT file by clicking on the arrow next to the folder icon in the left 
pane.  

![image](https://github.com/user-attachments/assets/169fc715-9e98-4900-a616-4a2e12230948)

D. In the left pane, click on the $MFT file to explore the metadata and Once $MFT is selected, click on the Metadata tab in the middle pane.

![image](https://github.com/user-attachments/assets/cac803ec-f900-4e83-a93d-9456fe05827a)

E.  On the Metadata tab, this is the first record or “Record 0” for the file system. 
Found within the MFT record are various attributes. Click on the Attributes tab.

![image](https://github.com/user-attachments/assets/7e616ccc-b206-48b3-9592-510371596f8e)

In each Record, there are attributes. The first attribute type 0x10 is called 
$Standard Information. Its type is 16 which is the decimal equivalent to hex 
value of 0x10. Its respective size is 96 bytes and the file is Resident (True) in the 
MFT. Resident means its size is less than 512 bytes, so it can reside in the MFT 
and does not have to be outside of the MFT located on the disk.

F. Click on the Hex Dump tab to view the hex values.
![image](https://github.com/user-attachments/assets/e781f3e0-e680-4618-a28f-a5dc024c0ec0)
. Notice that the MFT header fields all start with File 0 at offset 0x00.

G. Note that the size of the MFT record located at offset 0x1c to 0x1f is the default 
size of 0x400 or 262144 bytes. 
![image](https://github.com/user-attachments/assets/33143219-06bd-4778-babf-bd3e74b23342)

H. Locate the length of the header at offset 0x14 and is 0x38 or 56 bytes.
![image](https://github.com/user-attachments/assets/32178233-5ac0-44ae-83ec-06e53b91b24e)


<summary><b>Identifying Attributes with MFT File Viewer</b><summary></summary>

1. While on the Hex Dump tab, locate where the Standard Information attribute 
0x10 starts on offset 0x38.
![image](https://github.com/user-attachments/assets/453c72a6-b30d-40e3-9a3e-3df27852737f)

2. The size of the Standard Information attribute is at offset 0x04 and 0x05 from 
the beginning of the attribute. Its size is 0x60 or 96 bytes.
![image](https://github.com/user-attachments/assets/a60ba025-f2db-4279-bbd1-3df95977cafe)

3. Identify the creation date and time at 0x18 to 0x1F. When decoded, it can be 
concluded that this is stored in a Windows 64 bit hex format – Little Endian.
![image](https://github.com/user-attachments/assets/a5159f24-fdb5-42a6-9469-bda727d71e5e)

4. The last modified date and time for the file is next. Notice that the value is the 
same as the previous creation date and time.
![image](https://github.com/user-attachments/assets/ff774821-2b0f-40cc-9d44-3ec47c572888)

5. Next is the last access date and time. Notice the same value again.
![image](https://github.com/user-attachments/assets/b5f6bc14-59b8-45e2-9042-2ff3f7cbb1e9)

6. The next line of hex is the record access date and time. Notice the dates are the 
same.
![image](https://github.com/user-attachments/assets/44e0d3ca-6dc7-4a31-b65e-e444e5ea8999)

7. Navigate to the Metadata tab and compare the values to the actual values. The 
hex values should match. 
![image](https://github.com/user-attachments/assets/f532495b-1a77-49de-9c7a-cafe7e17723c)

8. Click on the Attributes tab and Identify the next attribute, 0x30 $Filename Information. Its type is 48, which is 
decimal for 0x30. Its respective size is 104 bytes and its resident. 
![image](https://github.com/user-attachments/assets/ead8a582-a38e-47b7-9c3b-63e8d799e16c)

9. Click on the Hex Dump tab, At offset 0x98, the attribute 0x30 can be located
![image](https://github.com/user-attachments/assets/d119a593-ed5e-43f4-9bd9-df0dd8dceb2b)

10.  Identify the size by locating bytes 0x04 and 0x05 from the 0x30. Notice the size is 
68 bytes in hex, which is 104 bytes in decimal. It is also a resident record.
![image](https://github.com/user-attachments/assets/f8c421bc-a72d-49f2-ac6b-edfabd7d29d1)

11. Click on the Attributes tab and identify the 0x80 attribute
![image](https://github.com/user-attachments/assets/a152706d-dc94-443b-911f-fe9dd27f9566)
Notice the attribute is the $Data attribute, which is type 0x80 or 128. Its size is 
72 bytes and its non-resident.

12. Click on the Hex Dump tab to analyze the $Data attribute more closely. Identify offset 0x100 to locate attribute 0x80. Move to bytes 0x04 and 0x05 from 
there to find the size. 
![image](https://github.com/user-attachments/assets/194b6484-2a08-4510-baec-f8c31d0c875a)
    
13. Notice that it is 48 in hex or 72 bytes in decimal. Move three more bytes to find 
the non-resident flag set
![image](https://github.com/user-attachments/assets/7f3cef2e-e470-44eb-995a-f4a6031b72b7)

14. Notice that the end of the MFT record is at offset 0x200
 ![image](https://github.com/user-attachments/assets/64f3157a-f3ca-4fde-8b32-cc7d18257d92)
   
15. Click on the Attributes tab and Compare the values found from the Hex Dump tab to the Attributes tab.
![image](https://github.com/user-attachments/assets/1179f7a4-53db-4569-af93-f69b8e6fc6dd)

16 Click on the Hex Dump tab. The last record is $Bitmap and its type 0xb0 is 176 
bytes in decimal. Its size is 80 in hex and is non-resident.
  ![image](https://github.com/user-attachments/assets/6724de88-8e5f-4c70-80be-6ff08ba60054)

17. Each record’s respective metadata can have multiple attributes and the same 
techniques that were applied in this lab can be used for each NTFS System file. 
As an example, click on the $Bitmap file in the left pane. Navigate to the Attributes tab while having the $Bitmap file selected. Notice the resident and non-resident data is shown for each attribute when 
looking through the different Records. 
![image](https://github.com/user-attachments/assets/e239eab0-e020-4503-aa6d-496e9f2f16ea)

If the Hex Dump data cannot be seen underneath Resident, expand the window 
size so that the window takes up the entire screen. Once this is done, the Hex 
Dump data will appear. 
</details>



<details>
  <summary><b>ACQUIRING AN IMAGE OF EVIDENCE MEDIA</b></summary>
  <b>OBJECTIVE</b>

  The objective of this lab is to acquire a forensic image of evidence media while strictly adhering to the first rule of digital forensics: preserving the integrity of the original evidence. After securing and retrieving the evidence, the lab will demonstrate the process of creating an exact, bit-for-bit copy (image) of the original data using appropriate forensic tools. The exercise will emphasize the importance of conducting analysis solely on the acquired copy to avoid altering the original data. Furthermore, the lab will explore the use of write-blocking devices, particularly in the context of FAT and NTFS file systems, and how they are crucial when using Windows-based acquisition tools. The goal is to ensure that the original evidence remains unmodified, guaranteeing the accuracy and validity of any subsequent forensic analysis.



<b>Task 1 - Using Autopsy to Acquire a Drive Image</b>

Autopsy is a powerful forensic analysis tool that allows you to acquire and examine data from various file systems. It supports file systems such as Microsoft FAT and NTFS, as well as Linux Ext2, Ext3, and Ext4, and other UNIX file systems. Autopsy can be used on Windows XP or older operating systems to perform thorough investigations and data analysis.

<b>STEPS</b>
We will be doing this lab on a provisioned Windows 10 OS on MidTap.

1. Open the <b>File Explorer</b> icon on the task bar, the navigate to the C:\work location
   This folder will serve as the storage location for data and other files generated by Autopsy while acquiring and analyzing evidence.

![image](https://github.com/user-attachments/assets/cdec71c7-be21-42a2-80ff-308ae6b5601c)

The following steps will demonstrate how to acquire an image of the drive labeled E, named USB. Please note that this is not an actual USB drive, but a fixed drive on the computer.

The process of acquiring an image can be applied to other types of media as well, including fixed disk drives and portable storage devices like USB flash drives.

2. Right-click Autopsy 4.6.0 on desktop, then click Run as administrator on the menu. Click Yes in the UAC if necessary.
![image](https://github.com/user-attachments/assets/1104f0b8-da79-48a1-bb46-56394b84db5b)


3. In the Autopsy welcome window, click New Case.
![image](https://github.com/user-attachments/assets/2fa41a1c-9186-4669-b14a-ceb7028471c2)

4. In the New Case Information box, type Proj01 in the Case Name box and set the Base Directory to Work. Click Next.
![image](https://github.com/user-attachments/assets/d7249f82-8d64-4550-8f95-d63f42b0904f)

5. In the Optional Information box, click Finish.
![image](https://github.com/user-attachments/assets/24d899fa-bb8e-4d8e-ad56-92c9d18665ee)

6. In the Add Data Source dialog box, click Local Disk, and click Next.
![image](https://github.com/user-attachments/assets/a32b32f8-1f39-4fc6-a6bf-a6cbda15f449)

7. In the Select Data Source box, select the disk USB (E:), then click Next.
  ![image](https://github.com/user-attachments/assets/e0dde5a6-c958-4cbf-984d-f09b225c1fca)

8. Click Next in the Configure Ingest Modules window.

9. Once the drive is finished being analyzed, click Finish
![image](https://github.com/user-attachments/assets/459bc727-2fd2-44f2-ba73-3f9392fcfd3a)


10. Click Case, select Exit from the menu to exit Autopsy.
![image](https://github.com/user-attachments/assets/99bef6cc-012c-4e1a-b7c1-c0d4013aa36d)


THIS EXERCISE COMPLETES MY FIRST FORENSICS DATA ACQUISITION.
</details>


<details>

<summary><b>USING AUTOPSY TO ANALYZE EVIDENCE</b></summary>

In the following steps, I will analyze George Montgomery’s drive. The first task is loading the acquired image into Autopsy by following these steps:

1. Start Autopsy as an Admin
 ![image](https://github.com/user-attachments/assets/72b1d5aa-d69e-4bb5-902f-60538de175a1)
 
2. Create a new Case by clicking on New case

3.  In the Case Information dialog box, in the Case Name text box, type:  InChp01.  The name is solely for this lab.   However, you can use the name of the case you will be working on.
 ![image](https://github.com/user-attachments/assets/8d721922-47eb-4324-8ae1-8e9e986d63b0)
Set the Base Directory to your Work directory. Click Next.

4. Click Finish in the Optional Information dialog box.
![image](https://github.com/user-attachments/assets/a44ed6af-5a85-4612-bb2a-e47465892675)

4. In the Add Data Source box, click Disk Image or VM File and click Next.
![image](https://github.com/user-attachments/assets/51df3b45-56e9-4ffa-b14d-7c4a838f4e1d)


5. Leave Autopsy open and open File Explorer. Navigate to the folder C:\Work > Data files > Ch01 containing the image. Right click Ch01Inchp01.exe, point to 7-zip, then click Extract Here to extract the contents. Close File Explorer.
![image](https://github.com/user-attachments/assets/fb8975b0-56dc-4cf4-b38f-e815e786e852)

6. Back in Autopsy, click Browse then navigate to C:\Work > Data files > Ch01 and click InChp01.dd, then click Open. Click Next.
![image](https://github.com/user-attachments/assets/5879fe8e-3796-4fed-b95c-8e5c03137745)

7. Click Next in the Configure Ingest Modules dialog box. Once the data source has been added, click Finish.
![image](https://github.com/user-attachments/assets/4ae07ee4-a82f-4ed1-98cf-4f0f75c1a642)

8. Click to expand Data Sources > Inchp01.dd in the left navigation pane. The Inchp01.dd file is then loaded in the main window.
![image](https://github.com/user-attachments/assets/07c8943a-5fd7-41a0-bb8e-2ebb69a7d04f)

9. In the right pane (the work area), click the confirmation.txt file to view its contents in the data area
![image](https://github.com/user-attachments/assets/1120f711-86bc-43e1-be98-3a802a0e7c32)

In the data area, you see the contents of the confirmation.txt file. Continue to navigate through the work and data areas and inspect the contents of the recovered evidence.
</details>


<details>
<summary><b>ANALYZING DATA</b></summary>

The next step involves analyzing the data and searching for information relevant to the complaint. This can be time-consuming, even if you know what to look for. To locate evidentiary artifacts, forensic analysts search for specific data values, which can include unique words, nonprintable characters (e.g., hexadecimal codes), or special printable characters like copyright (©) or registered trademark (®) symbols. Forensic tools, like Autopsy, allow you to search for these "keywords," which may consist of character strings or hexadecimal values (e.g., A9 for copyright). For this case, you will follow the steps to search for any reference to the name "George."

1. In the Autopsy window, Expand Data Sources > Inchp01.dd. Click Keyword Search in the upper-right hand corner. In the Search text box, type: password and click Search
   ![image](https://github.com/user-attachments/assets/83e7de34-f921-49d8-afd5-2cc8954fba9f)

2. When the search is finished, Autopsy displays the results in the search results pane in the work area. Note the tab labeled, Keyword search 1- password.
For each search you do in a case, Autopsy adds a new tab to help catalog your searches.
![image](https://github.com/user-attachments/assets/0c8ed4b4-ff8e-48ac-ae60-11bde085682a)

3. Click confirmation.txt.
Notice that confirmation.txt file is found to contain the string ‘password.’
![image](https://github.com/user-attachments/assets/14947637-43a4-456d-8902-cb9a13059b26)

4. Click to expand Results > Keyword Hits > Single Literal Keyword Search and note there are 2 instances of the keyword ‘password’.
![image](https://github.com/user-attachments/assets/3916bf30-13f1-4f3f-9117-980e4eaa72c5)


<b>GENERATING A REPORT</b>
Creating reports is an essential part of any digital forensics investigation. Using Autopsy, you can create reports in various formats. For this task, we will generate an HTML report

<b>STEPS</b>

1. Click Generate Report button at the top and Click the type of report you would like to generate under Report Modules - in this case choose HTML Report and click Next.
   ![image](https://github.com/user-attachments/assets/0260df69-6cf5-4a90-8f21-6dd39e6a92ee)

2. Leave All Results selected and then click Finish.
![image](https://github.com/user-attachments/assets/4fc3218d-b98d-462b-9142-e94c352f4431)

3. In the Report Generation Process dialog box, click Close.
   ![image](https://github.com/user-attachments/assets/86fc6b10-004e-458a-ba7c-06af566c94dc)

4. Click Reports in the navigation pane on the left and your report will appear in the right pane on the Listing tab
   ![image](https://github.com/user-attachments/assets/73e4fee3-5cfa-4025-87c6-c56374a66eef)

5. Double-click on the report, then choose to open it with your favorite browser to view the report.Double-click on the report, then choose to open it with your favorite browser to view the report.
![image](https://github.com/user-attachments/assets/50544a53-3d31-4f41-88ca-e9d17cb585d1)

</details>

<details>
<summary><b>SCENARIO BASED PROJECT</b></summary>

<b>SCENARIO</b>

The case in this project involves a suspicious death. Joshua Zarkan found his girlfriend’s dead body in her apartment and reported it. The first responding law enforcement officer seized a USB drive. A crime scene evidence technician skilled in data acquisition made an image of the USB drive with Autopsy and named it daylightTest.eve. Following the acquisition, the technician transported and secured the USB drive and placed it in a secure evidence locker at the police station. You have received the image file from the detective assigned to this case. He directs you to examine it and identify any evidentiary artifacts that might relate to this case.


1. First, let's run the Autopsy app as an Admin and create a new case. Enter C1Prj01 as the case name, make C:\Work\Data files\Ch01\ the Base Directory and then click Next. Click Finish
   ![image](https://github.com/user-attachments/assets/c12e3b0d-2c17-442e-9fb9-4b1f728fa4d4)


2. To add an image file, click Disk Image or VM File, then click Next.
   ![image](https://github.com/user-attachments/assets/9fb98885-9c37-428f-84ae-d72cb8843943)

3. Navigate to C:\Program Files (x86)\Technology Pathways\ProDiscover\Sample Images, click All Files, then click daylightTest.eve and then click Open.
![image](https://github.com/user-attachments/assets/f7750ede-4623-490d-b82d-0758371a47db)

4. Click Next in the Configure Ingest Modules, then click Finish.
   ![image](https://github.com/user-attachments/assets/43ade6b8-c0fc-4c91-9b76-3f6004b67241)

 5. Click to expand Views > File Types > By Extension > Documents > Plain Text (2), in the Listing area, notice the files that are listed  
   ![image](https://github.com/user-attachments/assets/557ef144-673e-42b0-b069-4fb2082fe599)

6. Right-click any file and click View in New Window. View the file, and then exit the program.
![image](https://github.com/user-attachments/assets/3bc662fd-a17f-4478-92ac-428a686fca7c)

7. If you decide to export a file, right-click the file and click Extract File(s). (Note: Creating a separate folder for exports is a good idea to keep your files organized.)
In the Save As dialog box that opens, navigate to the location where you want to save the file, and then click Save.

<b>FINAL REPORT</b>
Upon examining the acquired image of the USB drive (daylightTest.eve), two plain text files were identified: winter.txt and summer.txt. The content of winter.txt includes the text "2 pm," while summer.txt contains the text "3 pm." These times may hold significance in relation to the case, possibly indicating key moments that could be relevant to the timeline of events surrounding the suspicious death. The presence of these files and their specific references to times could potentially correlate with statements or evidence already collected, and further analysis may be necessary to determine their connection to the incident. As such, these files will be further investigated to understand their context and potential relevance to the ongoing investigation.
</details>

<details>
  <summary><b>SCENARIO 2</summary>

In this project, you work for a large corporation’s IT security company. Your duties include conducting internal computing investigations and forensics examinations on company computing systems. A paralegal from the Law Department, Ms. Jones, asks you to examine a USB drive belonging to an employee who left the company and now works for a competitor. The Law Department is concerned that the former employee might possess sensitive company data. Ms. Jones wants to know whether the USB drive contains anything significant.

In addition, she informs you that the former employee might have had access to confidential documents because a co-worker saw him accessing his manager’s computer on his last day of work. These confidential documents consist of 24 files with the text “fragment.” She wants you to locate any occurrences of these files on the USB drive’s bit-stream image.

    <b>STEPS<b>


</details>

























