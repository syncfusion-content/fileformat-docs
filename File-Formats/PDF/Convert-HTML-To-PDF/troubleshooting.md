---
title: Converting HTML to PDF | Syncfusion
description: Learn how to convert HTML to PDF using Blink rendering engines with various features like TOC, partial web page to PDF etc.
platform: file-formats
control: PDF
documentation: UG
---

# Troubleshooting and FAQ

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">BlinkBinaries are missing</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>When BlinkBinaries are not available in the <i>BlinkPath </i> mentioned location.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
Set the path of the BlinkBinaries folder to the BlinkPath property of BlinkConverterSettings.
<br/><br/>
(Or)
<br/><br/>
Place the BlinkBinaries folder in bin folder of the project. 
<br/><br/>
The BlinkBinaries will be available in the HTMLConverter installed location <span style="color:gray;font-size:14px"><i>($SystemDrive\Program Files (x86)\Syncfusion\HTMLConverter\xx.x.x.xx\BlinkBinaries)</i> </span>
<br><br/>
The BlinkBinaries also available in NuGet package installed location if you are using Blink HTML converter from NuGet packages. 

</td>
</tr>

<tr>
<th style="font-size:14px">Mapping BlinkBinaries in Web Application</th>
<td>
{% highlight c# tabtitle="C#" %}

//To refer BlinkBinaries from project location
settings.BlinkPath = Server.MapPath("BlinkBinaries");

//or

// To refer BlinkBinaries from bin folder of the Project
settings.BlinkPath = Server.MapPath("~/bin/BlinkBinaries");

{% endhighlight %}

</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception
</th>
<th style="font-size:14px">BlinkBinaries access is denied in server.
</th>

<tr>
<th style="font-size:14px">Reason
</th>
<td>If the BlinkBinaries folder does not have elevated permission for the respective user, then the Blink HTML converter may throw this exception.
</td>
</tr>

<tr>
<th style="font-size:14px">Solution
</th>
<td>You can add read/write/execute permission to for the BlinkBinaries folder for the respective user group.
</td>
</tr>
</table>

<table>

<th style="font-size:14px">Exception
</th>
<th style="font-size:14px">Blink rendering engine only supported from .NET Framework 4.5.
</th>

<tr>
<th style="font-size:14px">Reason
</th>
<td>HTML conversion using blink is only supported from .NET framework 4.5 or above. 
</td>
</tr>

<tr>
<th style="font-size:14px">Solution
</th>
<td>The application should target .NET Framework 4.5 or above to convert the HTML using the Blink rendering engine. 
</td>
</tr>

</table>

<table>
<th style="font-size:14px">Exception
</th>
<th style="font-size:14px">Failed to convert Webpage Exception
</th>

<tr>
<th style="font-size:14px">Reason
</th>
<td>Missing or mismatch of <a href="https://www.nuget.org/packages/Newtonsoft.Json/6.0.8">Newtonsoft.Json</a> package in the project.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>For converting HTML to PDF in Blink, you need to refer to the Newtonsoft.Json assembly or NuGet package with version 6.0.8 in the application, otherwise conversion will get failed.
</td>
</tr>

<tr>
<th style="font-size:14px">Reason
</th>
<td>The exception may occur if the Newtonsoft.Json assembly or NuGet package version is above 6.0.8.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>The Newtonsoft.Json package version is above 6.0.8, then include the following assembly binding redirection in the app.config/web.config file.
<br><br/>
{% highlight html %}

<runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="Newtonsoft.Json" publicKeyToken="30ad4fe6b2a6aeed" culture="neutral" />
        <bindingRedirect oldVersion="0.0.0.0-8.0.0.0" newVersion="8.0.0.0" />
      </dependentAssembly>
    </assemblyBinding>
</runtime>
{% endhighlight %}

</td>
</tr>

<tr>
<th style="font-size:14px">Reason
</th>
<td>If the temporary folder does not have elevated permission for the respective user, then the Blink HTML converter may throw this exception.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>The Blink HTML converter has support for setting the temporary path. Using the <i>TempPath</i> property, you can set any folder path that has read/write/execute permission. Then, the converter uses this path for creating temporary files. Refer to the following code snippet to set temp folder.
<br><br/>
{% highlight c# tabtitle="C#" %}

BlinkConverterSettings settings = new BlinkConverterSettings();
settings.TempPath = "D://MyProject//bin";

{% endhighlight %}
</td>
</tr>

<tr>
<th style="font-size:14px">Reason
</th>
<td>The exception may occur in Windows 7/Windows server 2008 environment due to limitation of <i>ClientWebSocket</i> implementation.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>To overcome the exception in Windows 7/Windows server 2008 environment, add the <a href="https://www.nuget.org/packages/System.Buffers/">System.Buffers.4.5.0</a> NuGet package in the sample for conversion. 
</td>
</tr>

<tr>
<th style="font-size:14px">Reason
</th>
<td>The exception may occur in Linux CentOS/Docker environment due to the chrome browser unable to launch from sandbox mode in CentOS.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>To overcome the exception in Linux CentOS/Docker environment, provide the execute permission for chrome and chrome-wrapper file inside the BlinkBinaries folder.
<br/>
<b>Refer to the following screenshot:</b>
<br/>
<img src="htmlconversion_images/Permission_chrome.png" alt="Blink chrome file permission">
<br/>
<img src="htmlconversion_images/Permission_chrome-wrapper.png" alt="Blink chrome wrapper file permission">
<br/>
Also, please add the below command line arguments in our converter setting,
<br/>
<table>
<tr>
<td>
{% highlight c# tabtitle="C#" %}

//Set command line arguments to run without sandbox.
blinkConverterSettings.CommandLineArguments.Add("--no-sandbox");
blinkConverterSettings.CommandLineArguments.Add("--disable-setuid-sandbox");

{% endhighlight %}
</td>
</tr>
</table>
<br>
</td>
</tr>

<tr>
<th style="font-size:14px">Reason
</th>
<td>Sometimes this exception occurs for only particular URL
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>Please contact Syncfusion <a href="https://www.syncfusion.com/support/directtrac/incidents/newincident">support</a> with input HTML, code snippet, and environment details (OS, culture settings, bit version etc.,).
</td>
</tr>

</table>

<table>
<th style="font-size:14px">Issue
</th>
<th style="font-size:14px">Blink converter may create PDF with blank pages.
</th>

<tr>
<th style="font-size:14px">Reason
</th>
<td>When the webpage (HTML) is not available or accessible.
</td>
</tr>

<tr>
<th style="font-size:14px">Solution
</th>
<td>Please check the internet connection and the HTML page is available in the mentioned location.
<br><br/>
Check the HTML file or URL is rendered properly in Chrome browser’s print preview. 
</td>
</tr>
</table>

<table>
<th style="font-size:14px">Issue
</th>
<th style="font-size:14px">Images or other contents in the HTML are missing in the resultant PDF document.
</th>

<tr>
<th style="font-size:14px">Reason
</th>
<td>The issue may be due to the slow internet connection or due to the behavior that the conversion completed before the page is loaded completely.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>To overcome this issue, add suitable delay for the conversion using the [AdditionalDelay](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_AdditionalDelay) property of the HTMLConverter. 
<br><br/>
{% highlight c# tabtitle="C#" %}

BlinkConverterSettings settings = new BlinkConverterSettings();
settings.AdditionalDelay = 2000;

{% endhighlight %}
</td>
</tr>

<tr>
<th style="font-size:14px">Reason
</th>
<td>While converting HTML string to PDF, the resources may be missed due to the invalid Base URL.
</td>
</tr>
<tr>
<th style="font-size:14px">Solution
</th>
<td>Overcome this issue by passing the valid base URL (path of the resources) along with the HTML string.
</td>
</tr>

</table>

<table>
<th style="font-size:14px">Issue
</th>
<th style="font-size:14px">Blink conversion failed in Azure app service (Windows).
<i>“The process was terminated due to an unhandled exception”</i>
</th>

<tr>
<th style="font-size:14px">Reason
</th>
<td>Blink rendering engine uses GDI calls for viewing and rendering the webpages. But Azure app service blocks GDI calls in Azure website environment. As azure website does not have the elevated permission and enough rights, so we could not launch the Chrome headless browser in Azure app service (Azure website and Azure function).
</td>
</tr>

<tr>
<th style="font-size:14px">Solution
</th>
<td>You can convert HTML to PDF using the Blink rendering engine in Azure cloud service (which has the elevated permission and rights to access the GDI calls). 
Refer to this <a href="https://www.syncfusion.com/kb/10258/how-to-convert-html-to-pdf-in-azure-using-blink">link</a> for more information. 
</td>
</tr>
</table>

<table>
	<tr>
		<th style="font-size:14px" colspan="2">HTML conversion support in Azure</th>
	</tr>
	<tr>
		<th style="font-size:14px">Azure App Service (Linux)</th>
		<td>Yes</td>
	</tr>
	<tr>
		<th style="font-size:14px">Azure Functions (Linux)</th>
		<td>Yes</td>
	</tr>
	<tr>
		<th style="font-size:14px">Azure Cloud Service</th>
		<td>Yes</td>
	</tr>
		<tr>
		<th style="font-size:14px">Azure App Service with Linux docker</th>
		<td>Yes</td>
	</tr>
</table>