---
title: Open and save Word document in Azure App Service on Windows | Syncfusion
description: Open and save Word document in Azure App Service on Windows using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Open and save Word document in Azure App Service on Windows

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to create, read, edit and convert Word documents programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **open and save Word document in Azure App Service on Windows**.

## Steps to open and save Word document in Azure App Service on Windows

Step 1: Create a new ASP.NET Core Web App (Model-View-Controller).
![Create a ASP.NET Core Web App project](Azure_Images/App_Service_Linux/Create-Project-WordtoPDF.png)

Step 2: Create a project name and select the location.
![Configure your new project](Azure_Images/App_Service_Windows/Configure-Open-and-Save-Word-Document.png)

Step 3: Click **Create** button.
![Additional Information](Azure_Images/App_Service_Linux/Additional_Information_WordtoPDF.png)

Step 4: Install the [Syncfusion.DocIO.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.DocIO.Net.Core Nuget Package](Azure_Images/App_Service_Windows/Nuget-Open-and-Save-Word-Document.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("OpenAndSaveDocument", "Home", FormMethod.Get);
    {
        <div>
            <br>
            <input type="submit" value="Open and Save Document" style="width:230px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 6: Include the following namespaces in **HomeController.cs**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;

{% endhighlight %}
{% endtabs %}

Step 7: Add a new action method **OpenAndSaveDocument** in HomeController.cs and include the below code snippet to **open an existing Word document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

string filePath = Path.Combine(_hostingEnvironment.WebRootPath, "Data/Input.docx");
using (FileStream docStream1 = new FileStream(filePath, FileMode.Open, FileAccess.Read));
using (WordDocument document = new WordDocument(docStream, FormatType.Docx));

{% endhighlight %}
{% endtabs %}

Step 8: Add below code example to add a paragraph in the Word document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Access the section in a Word document.
IWSection section = document.Sections[0];
//Add new paragraph to the section.
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.FirstLineIndent = 36;
paragraph.BreakCharacterFormat.FontSize = 12f;
//Add new text to the paragraph.
IWTextRange textRange = paragraph.AppendText("In 2000, AdventureWorks Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.") as IWTextRange;
textRange.CharacterFormat.FontSize = 12f;

{% endhighlight %}
{% endtabs %}

Step 9: Add below code example to **save the Word document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the Word document to MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser.
return File(stream, "application/msword", "Sample.docx");

{% endhighlight %}
{% endtabs %}

## Steps to publish as Azure App Service on Windows

Step 1: Right-click the project and select **Publish** option.
![Right-click the project and select the Publish option](Azure_Images/App_Service_Windows/Publish-Create-Word-Document.png)

Step 2: Click the **Add a Publish Profile** button.
![Click the Add a Publish Profile](Azure_Images/App_Service_Linux/Publish_Profile_WordtoPDF.png)

Step 3: Select the publish target as **Azure**.
![Select the publish target as Azure](Azure_Images/App_Service_Linux/Publish_Target_WordtoPDF.png)

Step 4: Select the Specific target as **Azure App Service (Windows)**.
![Select the publish target](Azure_Images/App_Service_Windows/Specific_Target_WordtoPDF.png)

Step 5: To create a new app service, click **Create new** option.
![Click create new option](Azure_Images/App_Service_Linux/Create_New_App_Service_WordtoPDF.png)

Step 6: Click the **Create** button to proceed with **App Service** creation.
![Click the Create button](Azure_Images/App_Service_Windows/Hosting-Open-and-Save-Word-Document.png)

Step 7: Click the **Finish** button to finalize the **App Service** creation.
![Click the Finish button](Azure_Images/App_Service_Windows/Finish-Open-and-Save-Word-Document.png)

Step 8: Click **Close** button.
![Create a ASP.NET Core Project](Azure_Images/App_Service_Windows/Publish-Open-and-Save-Word-Document.png)

Step 9: Click the **Publish** button.
![Click the Publish button](Azure_Images/App_Service_Windows/Before-Publish-Open-and-Save-Word-Document.png)

Step 10: Now, Publish has been succeeded.
![Publish has been succeeded](Azure_Images/App_Service_Windows/After-Publish-Open-and-Save-Word-Document.png)

Step 11: Now, the published webpage will open in the browser. 
![Browser will open after publish](Azure_Images/App_Service_Windows/Browser-Open-and-Save-Word-Document.png)

Step 12: Click **Open and Save Document** button.You will get the output **Word document** as follows.

![Open and Save Word document in Azure App Service on Windows](ASP-NET-Core_images/OpenAndSaveOutput.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Read-and-Save-document/Open-and-save-Word-document/Azure/Azure_App_Service).

Click [here](https://www.syncfusion.com/document-processing/word-framework/net-core) to explore the rich set of Syncfusion Word library (DocIO) features.