# Evidence Acquisition Using KAPE

## LAB \#1 (Module 1)

# Network Configuration {#network-configuration .list-paragraph}

Kindly note that this is an offline lab. Please use the URLs provided to register and download KAPE.

# Tasks {#tasks .list-paragraph}

## Task 1. Understanding KAPE Basics

You are required to understand KAPE's basics: modules, targets, etc.

## Task 2. Acquiring Evidence Using KAPE

You are required to understand how to use KAPE from the command line and answer the questions below with full details:

1.  Show how to acquire all the registry files and store them in the path Z:\\Case1\\RegFiles.

2.  When a malware is executed, it will leave different execution evidence, use KAPE to acquire all the evidence of execution from the victim's system. Store the evidence in a VHDX file with the name     CASE2.

3.  Show how to acquire the file system evidence with the event logs all in once acquisition. Then we want to store the evidence in a VHDX file with the name CASE3.

4.  Show how to acquire all the evidence on the system and store them in a VHDX file with the name CASE4.

**Note: If you do not have an external or a secondary drive to be used as Z:, you can create a VHD drive and add the Z: drive letter to it.**

<https://docs.microsoft.com/en-us/windows-server/storage/disk-management/manage-virtual-hard-disks>

<https://www.windowscentral.com/how-create-and-set-vhdx-or-vhd-windows-10>

## Task 3. KAPE GUI and Updates

You are required to acquire evidence using the KAPE GUI, then use a module(s) to process the evidence acquired. You are also required to check how to make sure KAPE is up to date.

## Task 4. KAPE DIY Tasks

You are required to do some research and experimentations alone to answer the given tasks.

# SOLUTIONS

Below, you can find solutions for each task. Remember though, that you can follow your own strategy, which may be different from the one explained in the following lab.

## Task 1. UNDERSTANDING KAPE BASICS

**Part \#1: Download KAPE**

1\. Use the URL below to register and download KAPE: <https://www.kroll.com/en/services/cyber-risk/investigate-and-respond/kroll-artifact-parser-extractor-kape>

2\. Extract the files to a folder of your selection. In this lab, I will be using the path C:\\kape

**Part \#2: Navigation and Basic Usage of KAPE**

1\. Go to the directory where KAPE was extracted and navigate the directories to have an idea of the directories and files there. You should see something similar to Figure 1.1.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image3.PNG)

Figure 1.1 - KAPE Directory

You can see a couple of directories and the standard kape.exe file and the gkape.exe (the GUI file). The tool by default is already bundled with numerous modules and targets which could be used. They could be found within the modules and targets directories, as shown in Figure 1.2.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image4.PNG)![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image5.PNG)

Figure 1.2 - KAPE Modules and Targets

**Part \#3: KAPE Modules**

The modules directory contains different directories, each refer to what they are used for. Inside the modules directory you will see many files with the **.mkape** file extension (assuming it's "module kape"). These modules are used to define how we process the evidence, whether using a script or program. Each module could be used to execute a single executable or reference other KAPE modules. Therefore, each module is created for a single purpose "category."

We can check the available modules by navigating the modules directory or using kape.exe with the command options --mlist and/or --mdetail, as shown in Figure 1.3.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image6.PNG)

Figure 1.3 - Listing KAPE Modules using kape.exe

Or with more details, as shown in Figure 1.4.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image7.PNG)

Figure 1.4 - Listing KAPE Modules using kape.exe with More Details

Finally, you can specify a subdirectory to check, as shown in Figure 1.5.

![A screen shot of a social media post Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image8.PNG)

Figure 1.5 - Listing Specific KAPE Modules using kape.exe

Let's check some of the modules preconFigured for us. Open using Notepad the file named !EZParser, as shown in Figure 1.6.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image9.PNG)

Figure 1.6 - Contents of !EZParser Module

We can see at the beginning of the file we have the following:

a.  Metadata about the file, such as version and export format.

b.  Processors section, which contains executables that are being called along with the command line options and variables and ExportFormat.

If you navigate to the **bin** directory, you can see the binaries, which will be run for those specific modules or at least for some of them including AmCacheParser.exe, AppCompatCacheParser, EvtxECmd, etc.

In the modules directory, there is a directory named **!Disabled**, which is used to disable modules. All you need to do, is move the .mkape file there and it will be disabled

Let's check this time the module file for PECmd which, is shown in Figure 1.7.

![A screenshot of a social media post Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image10.PNG)

Figure 1.7 - Contents of PECmd Module

As you can see in the Processors group, there are one or more PECmd entries. In this example, we have three entries, since PECmd is capable of exporting data using three different formats. In the header, we can see that the ExportFormat is set to **'csv'**. Hence, the first processor in the list will be used.

Values that are surrounded by **%** mark will be replaced by **KAPE** at runtime. These variables are already determined in the manual and in the included modules. For example, KAPE will replace:

-   %sourceDirectory% with the value passed by --msource

-   %destinationDirectory% with the value passed by --mdest

Using this method, **KAPE** is capable of performing its tasks despite the drive letters, source or destination directories, UNC paths, etc.

Let's check another example or two (psfile and ifconfig), as shown in Figures 1.8 and 1.9, respectively.

![A screenshot of a social media post Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image11.PNG)

Figure 1.8 - Contents of psfile Module

![A picture containing bird Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image12.PNG)

Figure 1.9 - Contents of ifconfig Module

Finally, in some modules we need to be able to handle redirection and this is where KAPE has an additional property named ExportFile which is used in the processor section to specify the file to export the results to (the redirected output). As we saw in the examples found in Figure 1.8, the ExportFile redirected the output to psfile.txt and in Figure 1.9, the output was redirected to ipconfig.txt. If an executable is used but no ExportFile defined, then it will depend on the user to use the redirection arrow to save their output.

**Part 4: KAPE Targets**

The targets determine files and directories that will be collected by KAPE, in other words they define the evidence you want to collect. Targets are found in the **target** folder and the have the **.tkape** file extension. We can use Notepad to check their content.

Now, similar to what we did with modules, we can either navigate to the targets directory and see what we have, or we can check the targets directory using kape.exe with the command options --tlist and --tdetail as shown in Figures 1.10 and 1.11 respectively.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image13.PNG)

Figure 1.10 - Listing Available Targets using kape.exe

![A screen shot of a computer Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image14.PNG)

Figure 1.11 - Listing Available Targets using kape.exe with Details

Open the FileSystem.tkape target file found under the **Windows** directory, as shown in Figure 1.12.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image15.PNG)

Figure 1.12 - Contents of FileSystem.tkape Target File

Again, we have the metadata at the top and here it describes this target is used for File system metadate. We can see here that this target file is actually referencing other targets. Each has a **Name** such as $MFT or $LogFile, the **Category** which here is FileSystem, the **Path** where the target file could be found and the other important property here is the **AlwaysAddToQueue**, which is used because Windows (on a running machine) will say that these files do not exist. This is used especially with files such as $MFT and $SDS, etc.

Let's open the contents of the $MFT.tkape file and see its contents as shown in Figure 1.13.

![A picture containing bird Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image16.PNG)

Figure 1.13 - Contents of $MFT.tkape Target File

Here we can see the path to the file we want this target to collect, which is C:\\$MFT, since that is where this file is located at. For more details about this, please check the **Digital Forensics Professional (DFP)** course.

Let's check another target file. This time I am going to use the LnkFilesAndJumpLists.tkape, since this requires some new settings that I want to explain. After opening the file, as shown in Figure 1.14, we can see that the evidence we are targeting here, depends on the user we are interested in, therefore we need to use wildcards.

![A screenshot of a social media post Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image17.PNG)

Figure 1.14 - Contents of LnkFilesAndJumpLists.tkape Target File

As you can see in the Path property, we are using the %user% wildcard which will be replaced by the user of interest. This is very important since we do not always know what user we are dealing with.

Another interesting feature that I did not cover in the previous example, is the **IsDirectory** with **Recursive** properties. If these are set to true and by giving a base directory, it copies all files and folders under the specified directory.

Let us look at one final example which is the Prefetch.tkape file, as shown in Figure 1.15.

![A picture containing bird Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image18.PNG)

Figure 1.15 - Contents of Prefetch.tkape Target File

As you can see in this example, we do not know the names of the files under the **prefetch** directory, therefore we used the *.pf wildcard. Prefetch files have the .pf file extension.

## Task 2. ACQUIRING EVIDENCE USING KAPE

Let's start using KAPE to acquire some evidence, but before you do that, just run kape.exe with no arguments and see what options are available, as shown in Figure 2.1.

![A screenshot of a cell phone on a table Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image19.PNG)

Figure 2.1 - kape.exe and all the Supported Parameters

In general, the options are divided into two main categories: Modules and Targets. Options which are related to Targets begin with '**t**' and options related to Modules begin with '**m**'.

The main target options required are --tsource,-- tdest, and --target. While the main options required for modules are: --msource, --mdest, and --module. If you use module and target options together, you can exclude --msource, since KAPE will assign it the value of --tdest.

Also, you might have noticed at the end there are a couple of examples on how to use KAPE.

1.  **--tsource**: Stands for the target source, L: drive. This can be locally attached drive, locally or remotely mounted image, or directory.

2.  **--target**: We have list of targets we want KAPE to collect from the L: drive, in this case it is the RegistryHives, but we can specify multiple targets using **,** separated list

3.  **--tdest**: the target destination, where to save the collected data

**Example \#1:** In the first example, I will be using **KAPE** to acquire all of the registry files and store them in the path Z:\\Case1\\RegFiles (used for gathering evidence), as shown in Figure 2.2.

![A screenshot of a computer Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image20.PNG)

Figure 2.1 - Using kape.exe to Acquire all Registry Files

The command used is found below:

```
kape.exe --tsource C: --target RegistryHives --tdest Z:\Case1\RegFiles
```

If we check the output, we will find the contents, as shown in Figure 2.3.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image21.PNG)

Figure 2.3 - Output of Files Generated by KAPE

The `*_ConsoleLog.txt` saves all the console output to this file, the name will be when this output was generated and then `_ConsoleLog.txt`. But if you open the `*_CopyLog.csv` file, you should see the files that were copied, as shown in Figure 2.4.

![A screen shot of a computer Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image22.PNG)

Figure 2.4 - All Files Acquired using KAP

Not only does KAPE acquire them, but also calculates the SHA1 hashes for each file, plus other timestamps. The *_SkipLog.csv file holds all the files that KAPE skipped and is usually due to being a duplicate, as shown in Figure 2.5.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image23.PNG)

Figure 2.5 - Files Skipped by KAPE

Now, by going into the subdirectories we can see the registry files collected, as shown in Figure 2.6.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image24.PNG)

Figure 2.6 - Using kape.exe to Acquire all Registry Files

**Example \#2:** When a malware is executed, it will leave different execution evidence, use KAPE to acquire all the evidence of execution from the victim's system. Store the evidence in a VHDX file with the name CASE2. The results are shown in Figure 2.7.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image25.PNG)

Figure 2.7 - Using kape.exe to Acquire all Evidence of Execution

The command used is found below:

```
kape.exe --tsource C: --tdest Z:\Case2\ --tflush --target EvidenceOfExecution --vss --vhdx CASE2
```

In example \#2, we used the --tflush to make sure the target in --tdest is empty (clean) and then used the targets EvidenceOfExecution to gather all evidence related to executions. We also added the --vss so we can process all Volume Shadow Copies too, since malware could be hidden or even found in previous shadows and finally, we used the --vhdx option to create a **VHDX** file with the name **CASE2**.

If we check the output, we will find the results have been added, as shown in Figure 2.8.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image26.PNG)

Figure 2.8 - Files Acquired for Example \#2

**Example \#3:** This time, we want the file system evidence with the event logs all in once acquisition. Then we want to store the evidence in a VHDX file with the name CASE3. The result of this are shown in Figure 2.9.

![A screenshot of a computer Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image27.PNG)

Figure 2.9 - Using kape.exe to Acquire File System and Event Log Evidence

The command used is found below:

```
kape.exe --tsource C: --tdest Z:\Case3\ --tflush --target FileSystem,EventLogs --vss --vhdx CASE3
```

In example \#3, the only difference this time are the targets we chose, which were FileSystem and EventLogs. Everything else was the same as in example \#2.

**Example \#4:** Acquire all the evidence on the system and store them in a VHDX file with the name CASE4. This is shown in Figure 2.10.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image28.PNG)

Figure 2.10 - Acquiring All Evidence

The command used is found below:

```
kape.exe --tsource C: --tdest Z:\Case4\ --tflush --target !ALL --vss --vhdx CASE4
```

In this example, we used the **!ALL** to tell KAPE we want to acquire from all available targets.

## Task 3. KAPE GUI AND UPDATES

For the GUI fans, **KAPE** also has a GUI interface which is in the main directory and named gkape. If you double click on it, you should see something similar to the interface shown in Figure 3.1 for **gkape** version **v0.9.0.3**.

![A screenshot of a computer Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image29.PNG)

Figure 3.1 - gkape version 0.9.0.3

As shown in Figure 3.1, I used the **Target source** to be C:\\ and the **Target destination** to be Z:\\Case5. Then I selected the **Amcache** target, selected **Process VSCs**, **Deduplicate** and the container is set to **VHDX** with the name CASE5. You can also so at the bottom of the **gkape** window the command that these options selected will be using.

Now in Figure 3.2, the difference to what I did in Case5, was I added the modules I want for processing.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image30.PNG)

Figure 3.2 - Collecting and Processing Evidence using gkape

**Updating KAPE and Tools:**

To make sure you have the latest targets and modules, we can either click on the "**Sync with Github**" button we saw in Figure 3.2 at the bottom of **gkape**, or we can use the command line option as seen below.

```
kape.exe --sync
```
Finally, the script Get-KAPEUpdate.ps1 can be used to check for an updated version of KAPE and download it. The results of executing it is shown in Figure 3.3.

![A screenshot of a cell phone Description automatically generated](https://assets.ine.com/cybersecurity-lab-images/1e108bbc-52ec-4b79-981a-2f6629dba35d/image31.PNG)

Figure 3.3 - Using Get-KAPEUpdate.ps1 to Check for KAPE Updates

## Task 4. KAPE DIY TASKS

Based on your understanding and usage, determine the commands required to perform the collection tasks below:

1.  Collect all Cloud service applications from the C: drive and save the output to Z:\\Evidence\\DIY1.

2.  Collect Evidence of Execution on a system, save the output to a zip file in the path Z:\\Evidence\\DIY2, and make sure the computer name is used as the name for the zip.

3.  Collect all the Windows Browser evidence from C: and all the volume shadow copies and store them in Z:\\Evidence\\DIY3. This time store your collected evidence to a network destination. Note: For this     example, you will need to use UNC paths.

4.  Collect all Prefetch files from the C: drive and save the output to Z:\\Evidence\\DIY5.

5.  Run the KAPE modules needed to process the results acquired in Task \#4.

## References

1.  Introducing KAPE, [[https://binaryforay.blogspot.com/2019/02/introducing-kape.html]](https://binaryforay.blogspot.com/2019/02/introducing-kape.html)

2.  Introduction to KAPE, [[https://cyberforensicator.com/2019/03/18/introduction-to-kape/]](https://cyberforensicator.com/2019/03/18/introduction-to-kape/) 
