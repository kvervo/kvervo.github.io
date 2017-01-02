---
author: supay
layout: post
excerpt_separator: <!-- more -->
comments: true
title: Using the Isolated Storage Explorer Tool
dsq_thread_id:
  - 345077375
tags:
  - wp7
post_format: [ ]
---
From [MSDN][1]:

> Isolated Storage Explorer (ISETool.exe) is a command-line tool that gets installed with the Windows Phone SDK. You use Isolated Storage Explorer to list, copy, and replace files and directories in isolated storage. This enables you to verify that the files are being saved in the correct location with the correct data. Isolated Storage Explorer can be used in the emulator or a device, and can be used for applications that target Windows Phone OS 7.0 and Windows Phone OS 7.1.

This tool is quite helpful when developing applications that rely heavily on saving data into the Isolated Storage.
However, using it is quite difficult. You have to get the product id from the manifest xml, type the full path of the ISETool.exe file and also provide a path where to save the snapshots.

<!-- more -->
So, I wrote a small batch script that simplifies the whole procedure of using ISETool.exe. The script will get the product id of your application for you and will launch the ISETool.exe with all needed parameters.

![Screenshot1]({{ site.baseurl }}images/posts/Capture.png)

The script allows you to take and restore snapshots. It also allows you to list the files and directories for the root path of the Isolated Storage.

### How to use it

*   Make sure you have the latest [Windows Phone SDK][3]
*   Download the package from [GitHub][4] ([.zip][5])
*   Unzip it to the root folder of your project (where your .sln file is)
*   Run ISETool.bat
*   Enter your project’s name*
*   Enter path where you would like to save the snapshots(*You can skip this step and the default path will be used: C:\%YOUR\_PROJECT\_NAME%.Storage\\*)
*   Choose a task

![Screenshot1]({{ site.baseurl }}images/posts/Capture1.png)

\* – The script takes for granted that the folder containing all files for your project is named after your project name. If not, enter the name of the folder containing your source files. For example, on the screenshot the folder containing the source files has the same name as the project: PhoneApp.

Hope you find this tool useful.

If you have any comments or suggestions, feel free to leave them in the comments below.

 [1]: http://msdn.microsoft.com/en-us/library/hh286408(v=vs.92).aspx "How to: Use the Isolated Storage Explorer Tool"
 [2]: http://blog.supaywasi.com/wp-content/uploads/2011/08/Capture.png "ISETool Batch Script"
 [3]: http://create.msdn.com/en-us/resources/downloads "App Hub - downloads"
 [4]: https://github.com/kvervo/ISETools-Batch-script "ISETools.bat.zip"
 [5]: https://github.com/downloads/kvervo/ISETools-Batch-script/ISETools.bat.zip "ISETools.bat.zip"
