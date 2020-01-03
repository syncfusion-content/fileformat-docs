---
layout: post
title: Installation and Deployment process for Syncfusion FileFormat product
description: This section provides information regarding learn how to install and deploy the Syncfusion Essential Studio File Formats components
platform: file-formats
control: Installation and Deployment
documentation: ug
---

# Installation using Web Installer


## Overview

Starting with version 16.2 (2018 Vol 2), Syncfusion provides Web Installer for Essential Studio platforms. This installer reduces the burden of downloading the installer of larger size. You can just download and launch the online installer which will be of smaller size and it will downloads and installs the Essential Studio products you have selected. The Essential Studio Web Installer includes the following platforms. You can download the latest version Essential Studio Web Installer [here](https://www.syncfusion.com/downloads/latest-version) . 

Starting with the version 17.3 (2019 Vol 3), Syncfusion provides updated version of Web Installer which allows both installation and uninstallation of the platforms for that specific version.

**Web (Essential JS 2)**

* ASP.NET MVC
* ASP.NET Core
* JavaScript

**Mobile**

* Xamarin
* Flutter

**Desktop**

* Windows Forms
* WPF
* Universal Windows Platform

**FileFormats**

* Read and Write Excel, Word, PDF and PowerPoint files

**Web (Essential JS 1)**

* ASP.NET Web Forms
* ASP.NET MVC
* ASP.NET Core
* JavaScript
* PHP
* JSP

   N> Universal Windows Platform will be installed in Windows 8.1 and later.  

 
## Installation

The following procedure illustrates how to install Essential Studio Platform Online Installer. 

1.  Double-click the Syncfusion Essential Studio Platform Online Installer file. The installer Wizard opens and extracts the package automatically.

    ![Installer Extraction Wizard](WebInstaller/Step-by-Step-Installation_img1.png)

    
    N> The installer wizard extracts the syncfusionfileformatswebinstaller_{version}.exe dialog, displaying the unzip operation of the package.
    
2. Welcome wizard of the Syncfusion Online Installer will be displayed. Click Next.

   ![Welcome wizard](WebInstaller/Step-by-Step-Installation_img2.png)

  
3.  Platform Selection wizard will be displayed. Select the platforms to be installed from the **Available** tab. Select **Install All** checkbox to select all the platforms. Click Next.
    
	![Platform Selection wizard Available](WebInstaller/Step-by-Step-Installation_img3.png)
	
	I> If the required software of the selected platform was not already installed, **Additional Software Required** alert will be displayed. However, you can continue the installation and install the required software later.
	
	![Additional Software Alert](WebInstaller/Step-by-Step-Installation_img5.png)
		
	
4. Confirmation wizard will be displayed. Here you can view and modify the list of platforms that will be installed.

    ![Confirmation for install](WebInstaller/Step-by-Step-Installation_img6.png)
	
	N> You can check the Estimated size of the Download and Installation by clicking the **Download Size and Installation Size** link.
	
	![Downaload and Installation size](WebInstaller/Step-by-Step-Installation_img7.png)

5.  Configuration wizard will be displayed. Here you can change the Download, Install and samples location. Also, you can change the Additional settings by platform basis. To install using the default configuration, click Next.

    ![Install and samples location for install](WebInstaller/Step-by-Step-Installation_img8.png)
	
	I> From version 17.3 (2019 Vol 3), Syncfusion provides option to provide custom download location.
	
 
    N> From the 2018 Volume 2 release, Syncfusion has changed the install and samples location 
	   **Default Install location:** {ProgramFilesFolder}\Syncfusion\{Platform}\{version}
	   **Default Samples location:** C:\Users\Public\Documents\Syncfusion\{platform}\{version}
	   However, you can change the locations by clicking browse button.

	

    * Select the **Install Demos** check box to install Syncfusion samples, or leave the check box clear, when you do not want to install Syncfusion samples.
    * Select the **Register Syncfusion Assemblies in GAC** check box to install the latest Syncfusion assemblies in GAC, or clear this check box when you do not want to install the latest assemblies in GAC.
    * Select the **Configure Syncfusion controls in Visual Studio** check box to configure the Syncfusion controls in the Visual Studio toolbox, or clear this check box when you do not want to configure the Syncfusion controls in the Visual Studio toolbox during installation. Note that you must also select the Register Syncfusion assemblies in GAC check box when you select this check box.
    * Select the **Configure Syncfusion Extensions controls in Visual Studio** checkbox to configure the Syncfusion Extensions in Visual Studio or clear this check box when you do not want to configure the Syncfusion Extensions in Visual Studio.
	* Select the **Create Desktop Shortcut** checkbox to create the desktop shortcut for Syncfusion Control Panel.


6.  After reading the License Terms and Conditions, check the **I agree to the License Terms and Privacy Policy** check box. Click Next.

7. Login wizard will be displayed. You should enter your Syncfusion Direct-Trac login credentials. If you don't have Syncfusion Direct-Trac login credentials, then you can click on **Create an Account**. Else if you forgot your password, click on **Forgot Password** to create new password. Click Install. 

    ![Login wizard install](WebInstaller/Step-by-Step-Installation_img9.png)
	
	I> The selected platforms will be installed based on your Syncfusion License (Trial or Licensed).

8. Download and Installation progress will be displayed.

    ![Download and Installation progress install](WebInstaller/Step-by-Step-Installation_img10.png)

9. Once the Installation is complete, **Summary** wizard will be displayed. Here you can check the list of platforms which are installed successfully and failed. Click Finish to exit the Summary wizard. 

    ![Installation Summary](WebInstaller/Step-by-Step-Installation_img11.png)
	
	* Click **Launch Control Panel** to open the Syncfusion Control Panel.


## Uninstallation

Till version 17.2, Syncfusion Web Installer had option for installation alone. Starting with the version 17.3 (2019 Vol 3), Syncfusion provides option for uninstalling the platforms of the same version from the Web Installer application itself. Select the list of the platforms to be uninstalled and Web Installer will uninstall those platforms one by one.

The following procedure illustrates how to uninstall Essential Studio Platform from Web Installer. 

1.  Double-click the Syncfusion Essential Studio Platform Online Installer file. The installer Wizard opens and extracts the package automatically.

    ![Installer Extraction Wizard uninstall](WebInstaller/Step-by-Step-Installation_img1.png)
	
2. Welcome wizard of the Syncfusion Online Installer will be displayed. Click Next.

   ![Welcome wizard uninstall](WebInstaller/Step-by-Step-Installation_img2.png)
   
3. Platform Selection wizard will be displayed. Select the platforms to be uninstalled from the **Installed** tab. Select **Uninstall All** checkbox to select all the platforms. Click Next.
    
	![Platform Selection wizard Installed](WebInstaller/Step-by-Step-Installation_img4.png)
	
4. Confirmation wizard will be displayed. Here you can view and modify the list of platforms that will be uninstalled. Click Uninstall.

    ![Confirmation for uninstall](WebInstaller/Step-by-Step-Installation_img12.png)
	
5. Uninstallation progress will be displayed.
  
    ![Progress for uninstall](WebInstaller/Step-by-Step-Installation_img13.png)
	
6. Once the Uninstallation is complete, **Summary** wizard will be displayed. Here you can check the list of platforms which are uninstalled successfully and failed. Click Finish to exit the Summary wizard. 

    ![Uninstallation Summary](WebInstaller/Step-by-Step-Installation_img14.png)
	
	
## Installation and Uninstallation

Till version 17.2, Syncfusion Web Installer had option for installation alone. Starting with the version 17.3 (2019 Vol 3), Syncfusion provides option for both install and uninstall the platforms of the same version from the Web Installer application itself.

The following procedure illustrates how to install/uninstall Essential Studio Platform from Web Installer. 

1.  Double-click the Syncfusion Essential Studio Platform Online Installer file. The installer Wizard opens and extracts the package automatically.

    ![Installer Extraction Wizard Install/Uninstall](WebInstaller/Step-by-Step-Installation_img1.png)
	
2. Welcome wizard of the Syncfusion Online Installer will be displayed. Click Next.

   ![Welcome wizard for Install/Uninstall](WebInstaller/Step-by-Step-Installation_img2.png)
   
3. Platform Selection wizard will be displayed. Select the platforms to be installed from the **Available** tab and platforms to be uninstalled from the **Installed** tab. Click Next.

   **Available**
	
    ![Platform Selection wizard Available Install/Uninstall](WebInstaller/Step-by-Step-Installation_img3.png)
	
   **Installed**
	
    ![Platform Selection wizard Installed](WebInstaller/Step-by-Step-Installation_img4.png)
	
4. Confirmation wizard will be displayed. Here you can view and modify the list of platforms that will be installed/uninstalled.

    ![Confirmation for install/uninstall](WebInstaller/Step-by-Step-Installation_img15.png)
	
	N> You can check the Estimated size of the Download and Installation by clicking the **Download Size and Installation Size** link.
	
	![Downaload and Installation size install/uninstall](WebInstaller/Step-by-Step-Installation_img16.png)

5.  Configuration wizard will be displayed. Here you can change the Download, Install and samples location. Also, you can change the Additional settings by platform basis. To install using the default configuration, click Next.

    ![Install and samples location install/uninstall](WebInstaller/Step-by-Step-Installation_img8.png)
	
	I> From version 17.3 (2019 Vol 3), Syncfusion provides option to provide custom download location.
	
6.  After reading the License Terms and Conditions, check the **I agree to the License Terms and Privacy Policy** check box. Click Next.

7. Login wizard will be displayed. You should enter your Syncfusion Direct-Trac login credentials. If you don't have Syncfusion Direct-Trac login credentials, then you can click on **Create an Account**. Else if you forgot your password, click on **Forgot Password** to create new password. Click Install. 

    ![Login wizard install/uninstall](WebInstaller/Step-by-Step-Installation_img9.png)
	
	I> The selected platforms will be installed based on your Syncfusion License (Trial or Licensed).

8. Download, Installation and Uninstallation progress will be displayed.

    ![Download and Installation progress install/uninstall](WebInstaller/Step-by-Step-Installation_img17.png)

9. Once the Installation is complete, **Summary** wizard will be displayed. Here you can check the list of platforms which are **installed/uninstalled** successfully and failed. Click Finish to exit the Summary wizard. 

    ![Summary install/uninstall](WebInstaller/Step-by-Step-Installation_img18.png)
	
	* Click **Launch Control Panel** to open the Syncfusion Control Panel.
