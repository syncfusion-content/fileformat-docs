# Working in Multi-Threading Environment

Essential PDF allows you to create or modify PDF documents simultaneously in multi-threading environment by using *PdfDocument.EnableThreadSafe*instance.

The following code illustrates how to create a PDF document in multi-threading environment.

{% tabs %}
{% highlight c# %}

    IEnumerable<int> works = Enumerable.Range(0, 100);

    Parallel.ForEach(works, index => GeneratePDF(index));

    private void GeneratePDF(int index)
        {
            //Enable the thread safe in PDF document.
            PdfDocument.EnableThreadSafe = true;

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

            string name = Guid.NewGuid().ToString();

            //Save the document.
            document.Save(name+".pdf");

            //Close the document.
            document.Close(true);
        }
		
{% endhighlight %}
{% highlight vb.net %}

        Dim works As IEnumerable(Of Integer) = Enumerable.Range(0, 100)

        Parallel.ForEach(works, Sub(index) GeneratePDF(index))

        Private Sub GeneratePDF(ByVal index As Integer)

        'Enable the thread safe in PDF document.
        PdfDocument.EnableThreadSafe = True

        'Create a new PDF document.
        Dim document As PdfDocument = New PdfDocument()

        'Add a page to the document.
        Dim page As PdfPage = document.Pages.Add()

        'Create PDF graphics for the page.
        Dim graphics As PdfGraphics = page.Graphics

        'Set the standard font.
        Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

        'Draw the text.
        graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

        Dim name As String = Guid.NewGuid().ToString()

        'Save the document.
        document.Save(name + ".pdf")

        'Close the document.
        document.Close(True)

    End Sub

{% endhighlight %}
{% endtabs %}

You can also modify the existing document in multi-threading environment. The below samples explain how to modify the existing PDF document in multi-threading environment.

{% tabs %}
{% highlight c# %}

    IEnumerable<int> works = Enumerable.Range(0, 100);

    Parallel.ForEach(works, index => GeneratePDF(index));

    private void GeneratePDF(int index)
        {

            //Enable the thread safe in PDF document.
            PdfDocument.EnableThreadSafe = true;

            //Load a PDF document.
            PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

            //Get first page from document
            PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

            //Create PDF graphics for the page
            PdfGraphics graphics = page.Graphics;

            //Set the standard font.
            PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

            //Draw the text.
            graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

            string name = Guid.NewGuid().ToString();

            //Save the document.
            doc.Save(name+".pdf");

            //Close the document.
            doc.Close(true);

        }

{% endhighlight %}
{% highlight vb.net %}

        Dim works As IEnumerable(Of Integer) = Enumerable.Range(0, 100)

        Parallel.ForEach(works, Sub(index) GeneratePDF(index))

        Private Sub GeneratePDF(ByVal index As Integer)

        'Enable the thread safe in PDF document.
        PdfDocument.EnableThreadSafe = True

        'Load a PDF document.
        Dim doc As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

        'Get first page from document
        Dim page As PdfLoadedPage = doc.Pages(0)

        'Create PDF graphics for the page
        Dim graphics As PdfGraphics = page.Graphics

        'Set the standard font.
        Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

        'Draw the text.
        graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

        Dim name As String = Guid.NewGuid().ToString()

        'Save the document.
        doc.Save(name + ".pdf")

        'Close the document.
        doc.Close(True)

    End Sub

{% endhighlight %}
{% endtabs %}
