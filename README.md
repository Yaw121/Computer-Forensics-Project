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


