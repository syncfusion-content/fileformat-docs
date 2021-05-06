---
layout: post
title: File Formats Offline Installer | file-formats | Syncfusion
description: this section provides information regarding the Syncfusion File Formats Offline installer and steps for installing it
platform: file-formats
control: Installation and Deployment
documentation: ug

---

# Installation using Offline Installer

You can refer to the [**Download**](https://help.syncfusion.com/file-formats/installation-and-upgrade/download) section to learn how to get the FileFormats trial or licensed installer.

## Installing with UI   

The steps below show how to install the Essential Studio FileFormats installer.

1.	Open the Syncfusion FileFormats offline installer file from downloaded location by double-clicking it. The Installer Wizard automatically opens and extracts the package

    ![Installer extraction wizard](Platform_images/Step-by-Step-Installation_img1.png)

    N> The Installer wizard extracts the syncfusionessentialfileformats_(version).exe dialog, which displays the package's unzip operation.

2.	To unlock the Syncfusion offline installer, you have two options:

   
    * *Login To Install*
   
    * *Use Unlock Key*
   
   
   
    **Login To Install**
   
    You must enter your Syncfusion email address and password. If you don't already have a Syncfusion account, you can sign up for one by clicking **"Create an account"**. If you have forgotten your password, click on **"Forgot Password"** to create a new one. Once you've entered your Syncfusion email and password, click Next.

    ![Login credentials](Platform_images/Step-by-Step-Installation_img2.png)   


    **Use Unlock Key**
   
    Unlock keys are used to unlock the Syncfusion offline installer, and they are platform and version specific. You should use either Syncfusion licensed or trial Unlock key to unlock Syncfusion FileFormats installer.
   
    The trial unlock key is only valid for 30 days, and the installer will not accept an expired trial key. 
   
    To learn how to generate an unlock key for both trial and licensed products, see [this](https://www.syncfusion.com/kb/2326) Knowledge Base article.

    ![Product key](Platform_images/Step-by-Step-Installation_img3.png)   


3.	After reading the License Terms and Privacy Policy, check the **“I agree to the License Terms and Privacy Policy”** check box. Click the Next button.


4.	Change the install and sample locations here. You can also change the Additional settings. Click Next\Install to install with the default settings.


    ![Advanced options](Platform_images/Step-by-Step-Installation_img4.png)

    **Additional Settings**
    
	* Select the **Install Demos** check box to install Syncfusion samples, or leave the check box unchecked, if you do not want to install Syncfusion samples
	* Select the **Register Syncfusion Assemblies in GAC** check box to install the latest Syncfusion assemblies in GAC, or clear this check box when you do not want to install the latest assemblies in GAC.
    * Select the **Configure Syncfusion controls in Visual Studio** check box to configure the Syncfusion controls in the Visual Studio toolbox, or clear this check box when you do not want to configure the Syncfusion controls in the Visual Studio toolbox during installation. Note that you must also select the Register Syncfusion assemblies in GAC check box when you select this check box.
    * Select the **Configure Syncfusion Extensions controls in Visual Studio** checkbox to configure the Syncfusion Extensions in Visual Studio or clear this check box when you do not want to configure the Syncfusion Extensions in Visual Studio.
    * Check the **Create Desktop Shortcut** checkbox to add a desktop shortcut for Syncfusion Control Panel
    * Check the **Create Start Menu Shortcut** checkbox to add a shortcut to the start menu for Syncfusion Control Panel




5.	If any previous versions of the current product is installed, the Uninstall Previous Version(s) wizard will be opened. Select **Uninstall** checkbox to uninstall the previous versions and then click the Proceed button.


    ![Advanced options](Platform_images/Step-by-Step-Installation_img7.png)
	
	
	N> From the 2021 Volume 1 release, Syncfusion has added the option to uninstall previous versions from 18.1 while installing the new version.
	
	
	N> If any version is selected to uninstall, a confirmation screen will appear; if continue is selected, the Progress screen will display the uninstall and install progress, respectively. If none of the versions are chosen to be uninstalled, only the installation progress will be displayed.
	
	**Confirmation Alert**
	
	![Confirmation wizard](Platform_images/Step-by-Step-Installation_img8.png)
	
	**Uninstall Progress:**
	
	![Uninstalling wizard](Platform_images/Step-by-Step-Installation_img9.png)
	
	**Install Progress**
	
	![Installing wizard](Platform_images/Step-by-Step-Installation_img5.png)

    N> The Completed screen is displayed once the FileFormats product is installed. If any version is selected to uninstall, The completed screen will display both install and uninstall status.
	
	![Completed wizard](Platform_images/Step-by-Step-Installation_img10.png)
	
7.  After installing, click the **Launch Control Panel** link to open the Syncfusion Control Panel.


8.  Click the Finish button. Your system has been installed with the Syncfusion Essential Studio FileFormats product.

## Installing in silent mode

The Syncfusion Essential Studio FileFormats Installer supports installation and uninstallation via the command line.

### Command Line Installation

To install through the Command Line in Silent mode, follow the steps below.

1.	Run the Syncfusion FileFormats installer by double-clicking it. The Installer Wizard automatically opens and extracts the package.
2.	The file syncfusionessentialfileformats_(version).exe file will be extracted into the Temp directory.
3.	Run %temp%. The Temp folder will be opened. The syncfusionessentialfileformats_(version).exe file will be located in one of the folders.
4.	Copy the extracted syncfusionessentialfileformats_(version).exe file in local drive.
5.	Exit the Wizard.
6.	Run Command Prompt in administrator mode and enter the following arguments.

   
    **Arguments:** “installer file path\SyncfusionEssentialStudio(platform)_(version).exe” /Install silent /UNLOCKKEY:“(product unlock key)” [/log “{Log file path}”] [/InstallPath:{Location to install}] [/InstallSamples:{true/false}] [/InstallAssemblies:{true/false}] [/UninstallExistAssemblies:{true/false}] [/InstallToolbox:{true/false}]


    N> [..] – Arguments inside the square brackets are optional.

    **Example:** “D:\Temp\syncfusionessentialfileformats_x.x.x.x.exe” /Install silent /UNLOCKKEY:“product unlock key” /log “C:\Temp\EssentialStudio_Platform.log” /InstallPath:C:\Syncfusion\x.x.x.x /InstallSamples:true /InstallAssemblies:true /UninstallExistAssemblies:true /InstallToolbox:true

	
7.  Essential Studio for FileFormats is installed.

    N> x.x.x.x should be replaced with the Essential Studio version and the Product Unlock Key needs to be replaced with the Unlock Key for that version.
   

### Command Line Uninstallation

Syncfusion Essential FileFormats can be uninstalled silently using the Command Line.

1.	Run the Syncfusion FileFormats installer by double-clicking it. The Installer Wizard automatically opens and extracts the package.
2.	The file syncfusionessentialfileformats_(version).exe file will be extracted into the Temp directory.
3.	Run %temp%. The Temp folder will be opened. The syncfusionessentialfileformats_(version).exe file will be located in one of the folders.
4.	Copy the extracted syncfusionessentialfileformats_(version).exe file in local drive.
5.	Exit the Wizard.
6.	Run Command Prompt in administrator mode and enter the following arguments.
   
    **Arguments:** “Copied installer file path\syncfusionessentialfileformats_(version).exe” /uninstall silent 

    **Example:** “D:\Temp\syncfusionessentialfileformats_x.x.x.x.exe" /uninstall silent


7.  Essential Studio for WPF is uninstalled.
   
   
