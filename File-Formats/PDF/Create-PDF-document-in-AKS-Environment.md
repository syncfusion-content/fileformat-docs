---
title: Create PDF document in AKS Environment | Syncfusion
description: Create PDF document in AKS Environment  using .NET PDF library without the dependency of Adobe Acrobat.
platform: file-formats
control: PDF
documentation: UG
---

# Create PDF document in AKS Environment 

The [Syncfusion .NET Core PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net-core) is used to create, read, edit PDF documents programmatically without the dependency of Adobe Acrobat. Using this library, you can **create PDF document in AKS Environment**.

## Steps to create PDF document in AKS Environment 
Step 1: Create Azure Container Registry.
![Azure Container Registry](AKS_images/Azure_container_Registry.png)

Step 2: Create a new ASP.NET Core Web App (Model-View-Controller).
![Create a ASP.NET Core Web App project](AKS_images/Create_net_core_web_app.png)

Step 3: Create a project name and select the location.
![Configure your new project](AKS_images/Set_project_name.png)

Step 4: Click **Create** button.
![Additional Information](AKS_images/Sample_addition_information.png)

Step 5: Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core/) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.Pdf.Net.Core NuGet package](AKS_images/NuGet_package.png)


Step 6: A default action method named Index will be present in *HomeController.cs*. Right click on Index method and select Go To View where you will be directed to its associated view page *Index.cshtml*. Add a new button in the *Index.cshtml* as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

    @{
        Html.BeginForm("CreatePDFDocument", "Home", FormMethod.Get);
        {
            <div>
                <input type="submit" value="Create PDF Document" style="width:200px;height:27px" />
            </div>
        }
        Html.EndForm();
    }

{% endhighlight %}

{% endtabs %}

Step 7: Include the following namespaces in *HomeController.cs*.

{% tabs %}

{% highlight c# tabtitle="C#" %}

    using Syncfusion.Pdf.Graphics;
    using Syncfusion.Pdf;
    using System.Diagnostics;
    using Syncfusion.Drawing;

{% endhighlight %}

{% endtabs %}

Step 8: Add a new action method named CreatePDFDocument in HomeController.cs file and include the below code example to generate a PDF document in *HomeController.cs*. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

    public IActionResult CreatePDFDocument()
    {
        //Create a new PDF document.
        PdfDocument document = new PdfDocument();
        //Add a page to the document.
        PdfPage page = document.Pages.Add();
        //Create PDF graphics for the page.
        PdfGraphics graphics = page.Graphics;
        //Set the standard font.
        PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
        //Draw the text.
        graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));
        //Saving the PDF to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        document.Save(stream);
        //Set the position as '0'.
        stream.Position = 0;
        //Download the PDF document in the browser.
        FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
        fileStreamResult.FileDownloadName = "Sample.pdf";
        return fileStreamResult;
    }

{% endhighlight %}

{% endtabs %}

## Steps to publish as AKS Environment

Step 1: Right-click the project and select Publish option.
![Right-click the project and select the Publish option](AKS_images/Click_publish_button.png)

Step 2: Select the publish target as **Docker Contain Registry**.
![Select the publish target as Azure](AKS_images/Target.png)

Step 3: Select the Specific target as **Azure Contain Registry**.
![Select the publish target](AKS_images/Specific_target.png)

Step 4: Once you select your Subscription, The registry we created earlier and the resource group it is in should be detected. Select it and click Finish. 
![Select the Resourse_group_name](AKS_images/Resourse_group_name.png)

Step 5: Click Publish button to publish the azure container registry.Publish_azure_container
![Publish container registry](AKS_images/Publish_azure_container.png)

step 6: You will see in the Output window the container being built and pushed to the ACR.
![ACR output window](AKS_images/ACR_output.png)

## Deploy Container Image to AKS
Step 1: Now we can deploy container to the AKS cluster. Start by opening the Azure portal, browsing to the Subscription and opening the Cloud Shell (BASH). We will use the kubectl tool to manage the cluster.

Step 2: You need to gather the credentials in order to interact with the cluster using kubectl in Azure Cloud Shell use the following command:
{% tabs %}

{% highlight c# tabtitle="C#" %}

    az aks get-credentials --resource-group rg-uk-aks-demo --name aks-uk-demo-msdn

{% endhighlight %}

{% endtabs %}

Step 3: You can review the credentials with the following command:
{% tabs %}
{% highlight c# tabtitle="C#" %}

     cat .kube/config

{% endhighlight %}

{% endtabs %}

Note: If you forgot to attach the ACR when creating the AKS resource (Like I did the first time), you can attach it after. I had to use the following command: `az aks update -n aks-uk-demo-msdn -g rg-uk-aks-demo --attach-acr acrmkmsdn`

Step 4: Now in the Cloud Shell, create a new file called deploy.yaml as follows:
{% tabs %}
{% highlight c# tabtitle="C#" %}

     code deploy.yaml

{% endhighlight %}

{% endtabs %}

Step 5: Then we pasted in the following Kubernetes Deployment and Service configurations. Note, change yours to match your app name, container name, registry, etc.
{% tabs %}
{% highlight c# tabtitle="C#" %}

    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: asp-docker-app
    spec:
    replicas: 2
    selector:
        matchLabels:
        app: asp-docker-app
    template:
        metadata:
        labels:
            app: asp-docker-app
        spec:
        containers:
        - name: asp-docker-app
            image: acrmkmsdn.azurecr.io/aspdockerapp:latest
    ---
    apiVersion: v1
    kind: Service
    metadata:
    name: asp-docker-app
    spec:
    type: LoadBalancer
    ports:
        - port: 80
        targetPort: 80
        protocol: TCP
    selector:
        app: asp-docker-app

{% endhighlight %}

{% endtabs %}

Step 6: Once you save and close the code editor, it’s finally time to apply the configuration:
{% tabs %}
{% highlight c# tabtitle="C#" %}

     kubectl apply -f deploy.yaml

{% endhighlight %}

{% endtabs %}

Step 7: Notice the deployment and service shows as created.

![Deployemnt created](AKS_images/Deployemnt_created.png)

Step 8: You can run the following commands:
{% tabs %}
{% highlight c# tabtitle="C#" %}

    kubectl get pods
    kubectl get nodes
    kubectl get service
    kubectl describe deployment

{% endhighlight %}
{% endtabs %}

or
{% tabs %}
{% highlight c# tabtitle="C#" %}

    kubectl get all

{% endhighlight %}
{% endtabs %}

Step 9: This will show the pods, services, apps and replica sets.
![Kubectl details](AKS_images/Kubectl_details.png).

Step 10: We can see the EXTERNAL-IP of the LoadBalancer above as being 20.117.254.138 and the port as 80. I should now be able to use this to browse the the web app running on AKS.
![Web app in AKS](AKS_images/Web_app_in_AKS.png).

If we head over to the Azure portal, select the AKS resource > Workloads > asp-docker-app, we can see the pods.
![Pods details](AKS_images/Pods_details.png).

And that’s it, the containerised ASP.NET Core Web App is running on the AKS cluster.

Select the PDF document and Click **Create PDF document** to generate the PDF document.You will get the output **PDF document** as follows.
![Create PDF document in Azure App Service on Linux](AKS_images/Output.png)

## Delete deployment
If you want to clean up the cluster, you can run the following commands:
{% tabs %}
{% highlight c# tabtitle="C#" %}

    kubectl delete -f deploy.yaml
    kubectl delete svc asp-docker-app --namespace=default

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub]().

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core) to explore the rich set of Syncfusion PDF library features. 

An online sample link to [create PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HelloWorld#/material3) in ASP.NET Core. 