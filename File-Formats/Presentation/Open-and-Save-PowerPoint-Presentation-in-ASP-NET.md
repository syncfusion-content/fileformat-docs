---
title: Open and save Presentation in ASP.NET | Syncfusion
description: Open and save Presentation in ASP.NET using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation in ASP.NET

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in ASP.NET**.

## Steps to open and save PowerPoint Presentation programmatically

Step 1: Create a new C# ASP.NET web application project.

![Create ASP.NET Web project](Workingwith_Web/Project-Open-and-Save.png)

Step 2: Select the **Empty** template to create the project.

![Select Web Forms template](Workingwith_Web/Empty-Open-and-Save.png)

Step 3: Install the [Syncfusion.Presentation.AspNet](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.AspNet Nuget package](Workingwith_Web/Nuget-Open-and-Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in **MainPage.aspx.cs**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 5: Add a new button in the **MainPage.aspx** as shown below.

{% tabs %}
{% highlight HTML %}

<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="MainPage.aspx.cs" Inherits="Read_and_edit_PowerPoint_presentation.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
       <asp:Button ID="Button1" runat="server" Text="Open and Save Presentation" OnClick="OnButtonClicked" />
       </div>
    </form>
</body>
</html>

{% endhighlight %}
{% endtabs %}

Step 6: Include the below code snippets in the click event of the button in **MainPage.aspx.cs**, to **open an existing PowerPoint Presentation in ASP.NET**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open(Server.MapPath("~/App_Data/Template.pptx"));

{% endhighlight %}
{% endtabs %}

Step 7: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Gets the first slide from the PowerPoint presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the first shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 8: Add below code example to **save the PowerPoint Presentation in ASP.NET**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint presentation
pptxDoc.Save("Result.pptx", FormatType.Pptx, Response);
//Close the PowerPoint presentation
pptxDoc.Close();

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/ASP.NET).

By executing the program, you will get the **PowerPoint document** as follows.

![ASP.Net output PowerPoint document](Workingwith_Core/Open-and-Save-output-image.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.