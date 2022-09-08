# How to Acquire Data using Linux (Offline)

## LAB 2

# Scenario

In this **offline** exercise, we will go through the process of preparing our evidence storage environment, and collecting the most important data from an offline (dead-box) hard disk drive in order to use it later on for analysis and investigations.

The scope of this lab is using a Linux operating system (<u>that you will set up locally</u>) to perform image acquisition of a hard disk drive.

# Goals

-   Prepare an evidence storage environment

-   Use Linux to prepare forensic images

-   Hash files and drives for validation

-   Bonus: copy forensic images to CD/DVDs

# What you will learn

-   How to prepare the evidence storage (target) environment to store evidence

-   How to organize your evidence storage

-   How to use different Linux tools to create forensic images

-   How to hash files and drives and why

-   How to compress and split forensic images to be stored on CD/DVD drives

To guide you throughout the lab process, you will find different Tasks. Tasks are designed for educational purposes, as well as to show you the usage of different tools and different methods to achieve the same goal. Please note that Tasks are not meant to be used as a methodology.

Armed with the knowledge acquired from the content and the skills acquired from the Task(s), you can achieve the Lab goal. If this is the first time doing a lab, we advise that you follow these Tasks.

Once you have completed all Tasks, you can proceed to the end of the lab manual and check the solutions.

# Recommended tools

-   **Virtualbox**

-   **Linux operating system with dd**

-   **Different Linux CLI Commands**

-   **The dcfldd tool**

# Setting up the environment

-   The tasks below assume you are using a Linux Operating System (Kali, SIFT, Ubuntu, etc.) locally. Please download the appropriate ISO to create such a Virtual Machine on your personal computer. We will be using Virtualbox.

-   In order to complete task 5, you need to install the dcfldd tool, which can be done on a Linux Debian/Ubuntu flavor like this:

```bash
sudo apt-get install dcfldd
```

-   This lab assumes you are going to image a previously connected hard disk drive. In a real-life scenario, you will be plugging this drive yourself; you will not find it already plugged in for you.

-   In a real-life scenario, it would be better to perform hard disk drive imaging using a write-blocker, to make sure you will not mistakenly damage your evidence.

    
    
    **Instructions to configure your Virtual Machine for this lab:**

We need two extra drives that will be used as follows:

I.  Drive A: this will be used to simulate the storage location used for evidence that we acquire, which is supposed to be big enough. I recommend making this around 100GB. Make it even bigger if you can, so you won't be facing disk space issues later on when you're working with different cases.

II. Drive B: this will be used to simulate the suspect's drive (or USB drive). I highly recommend you make this no less than 8GB. There are a couple of files that could be added to this drive if you want to simulate having a file on it, or you can just add your own later.

After you have installed or imported your Linux OS, all you need to do is:

1.  From Virtualbox, go to the virtual machine you prepared and click on Settings.

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp1.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image3.png)

2.  After clicking on the Settings button, you will get to the following window:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp2.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image4.png)

3.  Go to the Storage tab, which leads you to this:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp3.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image5.png)

4.  Now please be focused what you're going to do next, as this is an important step in your configurations. I highly recommend you click on the Controller saying "**SATA**," just like the figure below, and then click on the blue icon with a green plus in the middle of it:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp5.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image6.png)

5.  You may be wondering what will happen if you don't click on Controller: SATA. If you do not, you will need to adjust the whole document to be using "/dev/hdb" instead of "/dev/sdb" and using     "/dev/hdd" instead of "/dev/sdd." The reason behind that, is PATA drives use the hdx naming convention, while SATA drives follow the sdx naming convention, where x is any character starting from a. This is all you need to know here, you can check any Linux administration book for more details if you want.

6.  Now, after you press that button, a drop-down menu will appear, just like in the figure below:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp6.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image7.png)

7.  Click on the "**Add Hard Disk**" menu to proceed.

8.  You will reach a window asking if you want to add an existing drive to the system or you want to create a new disk. Please make sure you chose "**Create new disk**," unless you already have a disk and you     just want to add it to the system.

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp7.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image8.png)

9.  The next window will ask you about the hard disk type. Actually, I'm not interested in a specific type, so just chose the default one **VDI (VirtualBox Disk Image)** and proceed:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp8.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image9.png)

10. On the next window, I recommend you leave the default; this has some pros and cons. The good thing is that it won't reserve all the space that we talked about straight away, but it will be dynamically     growing. If we chose the second option, it will statically reserve all the Gigabytes that we specified for this disk. So, I will go with **Dynamically Allocated** and proceed:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp9.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image10.png)

11. Now you need to specify the name you want for the evidence storage drive, I have named it "**EvidenceStorage**," but you can name it whatever you want, just make sure you remember your naming conventions later.

    12. Also, you need to specify the drive size. Since we are preparing Drive A, this will be our Evidence Storage container, and it will have **100GB** in size. When done, click on the **Create** button to proceed.

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp10.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image11.png)

13. Please proceed to create the Suspect's drive that will be used for testing.

14. Now, repeat the same process for Drive B, and when you reach the page that you saw in the previous figure, make sure you do the following:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp11.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image12.png)

15. When you are sure of your settings, click the **Create** button to proceed.

16. You should get something like the following:

![C:\\Users\\Binary\\Desktop\\AddStorage\\dfp12.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image13.png)

17. Now start your Linux system and log into it.

18. The result is that we have the following:

-   **EvidenceStorage** drive is now found under **/dev/sdb**

-   **SuspectDrive** is now found under **/dev/sdd**

19. BTW, you can also validate your work using:

**#dmesg | grep sd**

20. In the output, you should find something saying that sdb is 100GB (or whatever size you chose) and sdd is 8GB (or whatever size you chose).

21. Or maybe:

**# sudo fdisk -l /dev/sdb**

**# sudo fdisk -l /dev/sdd**

22. You need to remember this carefully so you could easily work the lab. If you make any changes, then you will need to adapt to fit your needs.

23. Now, you can start working on the lab.

# Tasks

## Task 1: Preparing the Evidence Drive (Target)

Before you start the image acquisition process, you are required to prepare your storage environment and use a conventional way to store your evidence. Wipe your target drive, make sure it is clean for storing evidence. The reason this is done is to make sure there are no other files or material on the drive that might jeopardize your evidence. Remember, you may not be able to acquire data again, for various reasons!

To complete this task, we need you to do the following:

1.  Wipe your evidence storage (target drive) and format the drive with an Ext4 filesystem.

2.  Mount your evidence storage drive.

3.  Create a proper directory structure for your evidence, and use conventional naming for evidence that will be acquired.

## Task 2: Hashing Files and Drives

In this task, we assume you have already prepared your evidence storage, and it is now time to start gathering information related to the case. One of the most important parts in data acquisition is hashing. Hashing will be used later on for evidence validation. Don't take this task lightly; your evidence might not be admissible in court because they could not be validated!

You are required to store the hash value for any evidence you acquire and add it to the directory used for this case (assuming it is case \#1), this includes the hash value for the attached drive and the forensic image taken.

Please note that some tools like the ones we saw in the FTK Imager lab, generate this information automatically for you, while others embed this information as metadata with the forensic image itself. It is your responsibility to make sure such information is available, so make sure it is found with your evidence.

## Task 3: Imaging a Disk Drive with dd

In this lab, you are required to acquire a forensically sound image of a hard disk drive using the Linux "**dd**" command. Please be careful when using the options "if=" and "of=." Using them incorrectly could destroy the whole evidence or even worse, destroy your whole evidence storage!!!

After finishing the acquisition process, don't forget to hash the complete image and compare it with the hash of the drive you got from the previous task.

## Task 4: Imaging a Single Partition with dd

In this lab you are required to acquire a forensically sound image of a single partition instead of a full disk, also using the Linux "**dd**" command. You need to be aware of the offset of the partition in order to complete this task successfully. Use the "**dd**" man page to assist you with the options needed to fulfill this task.

After finishing the acquisition process, don't forget to hash the image and compare it with the hash of the partition.

## Task 5: Imaging a Disk Drive with GuyMager

In this lab, you are required to do the same acquisition you did in task 3 to acquire a forensically sound image of a hard disk drive, but this time using Guy Voncken's forensic imaging tool named "**Guymager**." The tool only works under Linux and is found in most digital forensics or penetration testing distributions. The tool can generate flat (dd), EWF (E01) and AFF images, plus the support of disk cloning.

You are required to perform the following:

1.  Forensically image the disk drive using the Expert Witness Format (EWF).

2.  Configure Guymager to support the Advanced Forensics Format (AFF), and then take a forensic image using this format.

3.  Understand why you don't need to hash the forensic images when using GuyMager.

4.  Check the metadata files generated with each forensic image.

5.  Compare the size of each image acquired, and compare them with the "dd" raw image you created in Task 3.

Reference: <http://guymager.sourceforge.net/>

## Task 6: Copying to CD/DVDs

Sometimes you need to copy or backup your forensic images to a CD or DVD, but let's say the file is too big to be incorporated within a CD nor a DVD. The solution would be to try to compress and split the forensic image file. Using basic Linux tools, you are required to compress and split the forensic image acquired in previous tasks to be handled by a 700MB CD.

Don't forget to hash your final file results.

# SOLUTIONS

## Task 1: Preparing the Evidence Drive (Target)

Before we start acquiring any evidence, let's first prepare our evidence storage, or in other words, the target drive that will be used to store the acquired evidence. To make sure the drive is clean and no files or previous material can affect the data that will be stored on the drive, let's start by wiping the drive.

In this task, we will wipe the second SATA drive, named "**/dev/sdb**" with the **Ext4** filesystem. If you prefer to wipe the drive with another filesystem, then don't forget to adjust the commands below to support your scenario.

**[Note:]** Wiping a very large drive can take some time, and it depends on the drive size. For this lab, we will be wiping a storage around 32GB, with the evidence being around 8GB in size.

First things first, let's prepare our directory hierarchy for storing evidence. I will be using the following structure:

1.  /cases -> this will hold all the cases being worked on, and will be used as the mount point for our evidence storage (target)
2.  /cases/case\#\## -> where \#\#refers to the case number
3.  /cases/case\#\#\#/Disk1 -> where this directory will hold all evidence acquired from this disk
4.  /cases/case\#\#\#/Disk1/Images -> this will hold the images of this disk
5. /cases/case\#\#\#/Disk1/Images/Part1 -> this will hold all information and images acquired from the first partition within this disk  

If you use the Linux "**tree**" command, you will have something like the directory hierarchy displayed to the right. Don't worry about the rest of the files you see, we will be doing all that.

![](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image14.png)

Note: if the "**tree**" command is not installed, just use the following command:

```
# sudo apt-get install tree
```

Now, let's prepare our evidence drive. First, wipe its content, and make sure it is clean; this can be done using the "**dd**" command line like this:

```
# dd if=/dev/zero of=/dev/sdb bs=512 conv=noerror,sync
```

**Note:** this might take some time depending on different factors!

After we have finished wiping the disk, we need to prepare it to be used for storage, so we need to partition the disk, and we will be doing that using "**fdisk**":

```
# sudo fdisk /dev/sdb
```

You will be presented with the fdisk command prompt, and you are now within the fdisk utility. Press "**n**" and **Enter** to create a new partition on the drive. You will then be asked a couple of questions to create the partition. Just use all the defaults by pressing **Enter**, and then after you finish, just press "**w**" to exit the fdisk utility.

Now, in order to let the Linux Kernel read the changes done (sort of notifying the Kernel), use the "**partprobe**" command as following:

```
# sudo partprobe
```

Now, let's create the Ext4 filesystem on our newly created partition; this can be done using any of the following commands:

```
# sudo mkfs -t ext4 /dev/sdb1
```

Or

```
# sudo mkfs.ext4 /dev/sdb1
```
Now, let's mount the partition to start using it to store our evidence; this can be done using the following command:

```
# sudo mount     /dev/sdb1  /cases/
```

**[Note:]** I have added tabs between the command details, just so you don't think they are concatenated together.

I will assume we are working on case number 003, so let's now start preparing the directory we will be using for this case. We can easily do that like this:

```
# sudo mkdir -p /cases/case003/Disk1/Images/Part1
```

This will create the complete directory hierarchy structure for us. But, before running any commands and do anything, let us go to our case's directory, which is done like this:

```
# cd /cases/case003/Disk1
```

The first thing to do is check what drive name and number has the Linux Kernel assigned the evidence drive that we want to acquire; this can be done using the "**dmesg**" command like this:

```
# dmesg | grep sd | tee disk1_dmesg.txt
```

We used the Linux "**grep**" command here to select only the lines of our interest. Also, we searched for a drive that would start with "**sd**," because we know that our drive is a Serial ATA drive.

I recommend using the Linux "**tee**" command for two reasons:

1.  First, you will be able to see the results of the command performed.

2.  Second, you will be able to store the result in a file of your choice.

By now, you may want to jump into data acquisition, but our preparation has one step left. Let's gather some basic information about the hard disk drive we are dealing with. When using a Linux operating system, this can be done using different command line tools; I will show all of them, and it is up to you to which to choose. The commands available are: **udevadm**, **hdparm**, **lshw**, and **smartctl**. Let's check how to use them, and the results obtained from each.

By the way, I will be using the following naming convention: **EvidenceNameNo_cmd.txt**

The usage of each command is shown below.

First udevadm:

```
# udevadm info --query=all --name=/dev/sdc  | tee disk1_udevadm.txt
```

hdparm:

```
# sudo hdparm -I /dev/sdc | tee disk1_hdparm.txt
```

lshw:

```
# sudo lshw -class disk | tee disk1_lshw.txt
```

smartctl:

```
# sudo smartctl -i /dev/sdc | tee disk1_smartctl.txt
```


Now that we have gathered and prepared the evidence storage environment, let's move on to the next task in this lab.

## Task 2: Hashing Files and Drives

This task is very simple and easy. We will be using the MD5 hashing algorithm, but feel free to adjust the examples below and use another algorithm such as SHA.

In order to hash text files (or any other type of file) using the MD5 algorithm, we will use the Linux "**md5sum**" command, which can be done like this:

```
# md5sum file
```

I assume you are currently in the "**/cases/case003/Disk1**" directory; we want to generate a hash value for all the evidence we have acquired so that if any change happens, we can easily identify that our evidence has been tampered with. To do that, I am going to hash all the text files we created in Task 1 for the disk drive.

```
# md5sum *.txt | tee disk1_info_md5.txt
```

This will create the file "disk1_info_md5.txt" of all the files we previously created (disk1_udevadm.txt, disk1_hdparm.txt, disk1_lshw.txt, disk1_smartctl.txt, etc.) and generate the hash for each of them. This will help us later make sure that none of the files has been modified (tampered).

Now, in order to hash the whole drive, we can still use the same syntax, since the drive is just a special file. This can be seen below:

```
# md5sum /dev/sdb | tee disk1_md5.txt
```

## Task 3: Imaging a Disk Drive with dd

It is time to start acquiring our first forensic image using Linux. We will be using the "**dd**" command line tool, which is one of the oldest commands found on a Linux operating system used to copy data.

From the previous tasks, we know that the drive of interest, or in other words, the drive that we want to create a forensic image for is "/dev/sdc." To take a forensic image of the whole drive using the Linux "dd" command, we will do it like this:

```
dd if=/dev/sdc of=/cases/case003/Disk1/Images/170617HDImage1.raw conv=noerror,sync bs=512
```

Now let's break down what the command and options do:

1.  The "if=" is to specify what is the Input File to read from. In our case, it is "/dev/sdc."

2.  The "of=" is to specify the name of the Output File to store our copy in. In this case, we used the file named "170617HDImage1.raw". You can change it to whatever your naming convention you are using.

3.  The "conv=noerror,sync" is used to instruct "dd" to first ignore any reading error with the "noerror" option, and to continue reading even if a read error was found (do not stop reading). The "sync"     option is used to pad the byte with reading errors with 0x00. If this option is not used, it will mess up your results.

4.  Finally, the "bs" which is for block size, is to specify the size of blocks to read and write. We used 512 bytes here, which is the default, and we didn't have to use it. I added it for clarification.

One important note is to be careful with if= and of= options. Make sure you study your input (source) and output (destination) correctly before hitting Enter on your keyboard. Using the wrong input and output file might destroy the whole evidence with such a mistake!!!

Our final step is to calculate the hash value for the file, which can be done like this:

```
# md5sum 170617HDImage1.raw | tee 170617HDImage1_md5.txt
```

## Task 4: Imaging a Single Partition with dd

Sometimes you may not be interested in imaging the whole disk drive, or maybe you don't have enough storage space for the forensic image of a full disk drive. In such scenarios, you will be mainly interested in imaging a specific partition within the disk drive. The Linux "dd" command could also be used here for this situation, and that is what we will be doing next.

Now, let's assume that we don't know what exact partition we are interested in acquiring, and we need to check which partition to acquire. There are different ways to list partition details within a disk drive, and below is only a few of them.

First, let us use the Linux "**fdisk**" command; this can be done like this:

```
# sudo fdisk -l /dev/sdc
```

Where the "-l" option is used to list the partition table of the "/dev/sdc" disk drive. The results will be something like the figure below:

![G:\\ALI\\Jobs\\eLearnSecurity\\Hassan - Drafts\\guyy\\1\\fdisk.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image15.png)

If you notice, the disk drive has only one single partition, which starts at sector 2048 and ends at sector 4194304. Also, the results show that each sector is 512 bytes, and this occupies 4194304 sectors, and if you calculate them properly (total # of sectors X 512 bytes), you will get the size of the partition, which is 2GB. Remember these details, as we will need them when we start tuning the "dd" command options later.

The second way is by using the "**mmls**" command, which is part of the Sleuth Kit (more on this later in the course). We can use "mmls" to display the whole disk drive table like this:

```
# sudo mmls /dev/sdc
```

The results will be something like the figure below:

![G:\\ALI\\Jobs\\eLearnSecurity\\Hassan - Drafts\\guyy\\1\\mmls.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image16.png)

As you can see, "mmls" displayed far more interesting information, than what we saw in the "fdisk" command results. "mmls" helped display even the unallocated disk slots, which sometimes might be used to hide data! Also, you may have noticed that the results also show that the first truly used disk is at sector 2048, and its size is 4194304 sectors (2147483648 bytes or 2097152 KB or 2048 MB or 2GB). You will need to get used to these calculations a lot.

Now that we have the partition details, starting location and length, we can get back to work, which is acquiring a forensic image for a single partition.

To acquire this partition, all we need to do is the following:

```
dd if=/dev/sdc
of=/cases/case003/Disk1/Images/Part1/170617HDImageP1.raw
conv=noerror,sync bs=512 skip=2048 count=4194304
```
Let's break this down, but only the changed parts, as I assume you already know the rest that we did in the previous task.

1.  The "skip=" option is used to tell "dd" that we want to start the copy from that specific location. The "dd" command already knows that skip=2048, means skip 2048 X 512 bytes or in other simple words; skip 2048 blocks (sectors).

2.  The "count=" option, is to instruct "dd" that we want to copy that amount of blocks (sectors). So in our example here, we used 4194304, because if you go back to either the results from "fdisk" or "mmls,"  you will find that, this is the length of the partition, or the number of blocks (sectors), that this partition occupies.

Now, generate the hash value for our newly created partition:

```
# md5sum /cases/case003/Disk1/Images/Part1/170617HDImageP1.raw | tee 170617HDImageP1_md5.txt
```


Now, just for the record, there is another way of doing this! Yes, and it is even much the same as what we did in Task 3! All you need to do is:

```
dd if=/dev/sdc1
of=/cases/case003/Disk1/Images/Part1/170617HDImageP1_copy.raw
conv=noerror,sync    bs=512
```
As you see, no need for those "skip" and "count" options, just specify the partition directly by its logical name "/dev/sdc1".

To make sure both give you the exact same results, just compare their hash values, which could be done like this:

```
# md5sum /cases/case003/Disk1/Images/Part1/170617HDImageP1.raw =/cases/case003/Disk1/Images/Part1/170617HDImageP1_copy.raw | tee 
170617HDImageP1_md5.txt
```
They should both give you the exact same hash value.

## Task 5: Imaging A Disk Drive with Guymager

In this lab, we will be acquiring a forensic image for a disk drive using the Guymager tool. Using the tool is very simple and straightforward. Let's start solving the tasks required for this part.

To forensically image the disk drive using the Expert Witness format (EWF), we have to start Guymager like this:

```
# sudo guymager
```
After running the command line above, a Window similar to the one in the figure below will appear:

![](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image17.png)

The window shows all the available disk drives that are currently seen by your operating system (Linux Kernel). Our interest in this task is to acquire an image of the "**/dev/sdc**" drive, so right click on the row of the drive and click "**Acquire Image**" as shown in the below figure.

![](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image18.png)

The acquire image dialog will appear, and all you need to do is fill in the details as shown in the figure below

![](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image19.png)

Add the case number, evidence number, examiner's name, and any further details to the description and notes field. Next, select the location to store this image, and this should be "**/cases/case003/Disk1/Images**". Choose the image file name and write it in the image name field. Finally, make sure you select "**Calculate MD5**" and "**Calculate SHA-256**". All this can be seen in the previous figure. When you finish all these settings, press the "**Start**" button. Guymager will start the acquisition process, as seen in the figure below:

![G:\\ALI\\Jobs\\eLearnSecurity\\Hassan - Drafts\\guyy\\1\\guy3.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image20.png)

Guymager will not just show the progress of acquiring the image, but even the progress of verifying the acquisition, which you can see in the figure below:

![G:\\ALI\\Jobs\\eLearnSecurity\\Hassan - Drafts\\guyy\\1\\guy333.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image21.png)

![G:\\ALI\\Jobs\\eLearnSecurity\\Hassan - Drafts\\guyy\\1\\guy333333.png](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image22.png)

Use the Linux "**cat**" command to display all the metadata that has been automatically added to the "**170617HDImage2.info**" file; which can be done like this:

```
# cat /cases/case003/Disk1/Images/170617HDImage2.info
```

Read and check the results displayed. **<u>Note:</u>** the output of the file was not listed here, due to its huge number of lines.

By default, Guymager has disabled acquiring images in the Advanced Forensics Format (AFF), so we need to enable it by modifying the configuration file "**/etc/guymager/guymager.cfg**." To do that, open the file using the following command:

```
# sudo gedit /etc/guymager/guymager.cfg
```
Search for the line that has "**AffEnabled = false**" and change it to true, just like the figure below.

![](https://assets.ine.com/cybersecurity-lab-images/2f4526bd-180f-421c-8b42-9810bf0cfb1a/image23.png)

The rest of the acquisition steps are just the same as acquiring an expert witness format image, so I will leave this as an exercise for you to perform on your own.

If we check the files "**170617HDImage2.info**" and "**170617HDImage3.info**", you will find that the MD5 and SHA-256 hash values for the disk drive have been added and verified. This is the difference between acquiring an image using expert witness format, the advanced forensics format, and the raw data format where you have to perform the calculations yourself.

Finally, if you compare the size of the images acquired, and compare them with the "dd" raw image you created in Task 3, you will find the following:

**170617HDImage1.raw** -> Size is the exact size of the disk, which is 8GB.

**170617HDImage2.E01** -> Size is around 24MB because it supports compression.

**170617HDImage3.aff** -> Size is around 8.6MB because it also supports compression.

## Task 6: Copying to CD/DVDs

With all the new and great tools being released, you might not encounter this issue where you have a big forensic image and need to copy it to a CD, DVD, or maybe to a small thumb drive, but it is not bad to have this capability within your arsenal. You never know when you will need it. Okay, let us get started!

I am going to assume we want to compress and split the raw forensic image we acquired previously named "**170617HDImage1.raw**". We can do that using the following:

```
# gzip -c 170617HDImage1.raw | split -d -b 699M      - 170617HDImage1.raw.
```
This will use the Linux "**gzip**" command to compress the specified file, and then pass it over to the Linux "**split**" command, which will be splitting the file based on chunks of 699MB of size. The "**-d**" option is used so that the prefix used for the split file, will be using a numbering prefix (00, 01, 02, etc.) and not an alphabetic (aa, ab, ac, etc.). The "**-b**" option seems clear, right (SIZE)? But please note, that there is a dash "**-**," after the specified size. This is used to let split know that the input will be from standard input, and the "**170617HDImage1.raw.**" with the dot."", after the file name, so the results will be created like this:

170617HDImage1.raw**.00**

170617HDImage1.raw**.01**

170617HDImage1.raw**.02**

And so on.



Did we forget anything? We did not hash all the results, because if you remember, we are dealing with the raw format, and raw does not incorporate any metadata by default. So, let us do that, hash all chunks:

```
# md5sum 170617HDImage1.raw.* | tee 170617HDImage1.raw_chunks_md5.txt
```


Just in case you want to reconstruct the forensic image back to its original state, do the following:

```
# cat 170617HDImage1.raw.* | gunzip - > 170617HDImage1_copy.raw
```


We used the Linux "**cat**" command to pass the content of the 170617HDImage1.raw**.*** parts to the other Linux command "**gunzip**" and use it to decompress the image. The dash "**-**" was used as explained previously, to read from standard input, and the arrow "**>**" is used to redirect the results to the file we named "**170617HDImage1_copy.raw**".



I would like to do one final step, just to make sure all our work has been performed correctly; which is "verification!" Let's verify the result using the "md5sum" command like this:

```
# msd5sum 170617HDImage1.raw 170617HDImage1_copy.raw
```

If you performed everything correctly, then they must both give you the exact same hash value; congrats, mission accomplished successfully!

That's it for this lab, see you in the next one!
