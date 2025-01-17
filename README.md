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

<details>
<summary><b>Identifying Attributes with MFT File Viewer</b><summary></summary>

1. 
</details>


