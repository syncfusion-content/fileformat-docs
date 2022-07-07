---
title: Working with Drawing Objects | Syncfusion
description: This section explains about drawing objects in Essential XlsIO. XlsIO provides Option button support only for XLSX format.
platform: file-formats
control: XlsIO
documentation: UG
---

# Working with Drawing Objects 

## Form Controls 

You can add and manipulate the text Box, option button, check box, and combo box controls into the worksheet. Enable these controls to create forms which are very user friendly.

N> Support for Active X Form controls is not yet available.

This section explains the usage of the following [Form Controls](https://support.office.com/en-us/article/Overview-of-forms-Form-controls-and-ActiveX-controls-on-a-worksheet-15BA7E28-8D7F-42AB-9470-FFB9AB94E7C2#bmcontrols_on_the_forms_toolbar).

* Text Box
* Check Box
* Combo Box
* Option Button

### Text Box

The **ITextBoxShape** interface represents a text box in a worksheet. Various properties like Horizontal and Vertical Alignment, Alternative Text, Text Rotation, and so on are also supported.

The following code example illustrates how to add and manipulate a text box control.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates a new Text Box
  ITextBoxShape textbox = sheet.TextBoxes.AddTextBox(2, 2, 30, 200);
  textbox.Text = "Text Box 1";
  textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200);
  textbox.Text = "Text Box 2";

  //Reads a Text Box
  ITextBoxShape shape1 = sheet.TextBoxes[0];
  shape1.Text = "TextBox";

  //Format the control
  shape1.Fill.ForeColor = Color.Gold;
  shape1.Fill.BackColor = Color.Black;
  shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent;

  //Remove a Text Box
  ITextBoxShape shape2 = sheet.TextBoxes[1];
  shape2.Remove();

  workbook.SaveAs("Textbox.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creates a new Text Box
  Dim textbox As ITextBoxShape = sheet.TextBoxes.AddTextBox(2, 2, 30, 200)
  textbox.Text = "Text Box 1"
  textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200)
  textbox.Text = "Text Box 2"

  'Reads a Text Box
  Dim shape1 As ITextBoxShape = sheet.TextBoxes(0)
  shape1.Text = "TextBox"

  'Format the control
  shape1.Fill.ForeColor = Color.Gold
  shape1.Fill.BackColor = Color.Black
  shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent

  'Remove a Text Box
  Dim shape2 As ITextBoxShape = sheet.TextBoxes(1)
  shape2.Remove()

  workbook.SaveAs("Textbox.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates a new Text Box
  ITextBoxShape textbox = sheet.TextBoxes.AddTextBox(2, 2, 30, 200);
  textbox.Text = "Text Box 1";
  textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200);
  textbox.Text = "Text Box 2";

  //Reads a Text Box
  ITextBoxShape shape1 = sheet.TextBoxes[0];
  shape1.Text = "TextBox";

  //Format the control
  shape1.Fill.ForeColor = Color.FromArgb(255, 255, 215, 0);
  shape1.Fill.BackColor = Color.FromArgb(255, 0, 0, 0);
  shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent;

  //Remove a Text Box
  ITextBoxShape shape2 = sheet.TextBoxes[1];
  shape2.Remove();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "TextBox";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates a new Text Box
  ITextBoxShape textbox = sheet.TextBoxes.AddTextBox(2, 2, 30, 200);
  textbox.Text = "Text Box 1";
  textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200);
  textbox.Text = "Text Box 2";

  //Reads a Text Box
  ITextBoxShape shape1 = sheet.TextBoxes[0];
  shape1.Text = "TextBox";

  //Format the control
  shape1.Fill.ForeColor = Color.Gold;
  shape1.Fill.BackColor = Color.Black;
  shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent;

  //Remove a Text Box
  ITextBoxShape shape2 = sheet.TextBoxes[1];
  shape2.Remove();

  //Saving the workbook as stream
  FileStream stream = new FileStream("TextBox.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates a new Text Box
  ITextBoxShape textbox = sheet.TextBoxes.AddTextBox(2, 2, 30, 200);
  textbox.Text = "Text Box 1";
  textbox = sheet.TextBoxes.AddTextBox(6, 2, 30, 200);
  textbox.Text = "Text Box 2";

  //Reads a Text Box
  ITextBoxShape shape1 = sheet.TextBoxes[0];
  shape1.Text = "TextBox";

  //Format the control
  shape1.Fill.ForeColor = Syncfusion.Drawing.Color.Gold;
  shape1.Fill.BackColor = Syncfusion.Drawing.Color.Black;
  shape1.Fill.Pattern = ExcelGradientPattern.Pat_90_Percent;

  //Remove a Text Box
  ITextBoxShape shape2 = sheet.TextBoxes[1];
  shape2.Remove();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("TextBox.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TextBox.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

A complete working example to add a text box in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Text%20Box). 

**Text Box in Chart**

Syncfusion XlsIO supports creating and reading text box within Excel chart. The following code example illustrates this.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Read the text 
  for (int i = 0; i < worksheet.Charts.Count; i++)
  {
    for (int j = 0; j < worksheet.Charts[i].TextBoxes.Count; j++)
    {
      String text = worksheet.Charts[i].TextBoxes[j].Text;
    }
  }

  //Creates a new text box in the chart 
  ITextBoxShape textbox = worksheet.Charts[0].TextBoxes.AddTextBox(2, 2, 80, 300);
  textbox.Text = "Text Box in the chart";

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx

  Dim workbook As IWorkbook = application.Workbooks.Open("../../Data/WF_62496_Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  Dim i As Integer
  Dim j As Integer

  For i = 0 To worksheet.Charts.Count - 1 Step i + 1
    For j = 0 To worksheet.Charts(i).TextBoxes.Count - 1 Step j + 1
      Dim text As String = worksheet.Charts(i).TextBoxes(j).Text
    Next
  Next

  Dim textbox As ITextBox = worksheet.Charts(0).TextBoxes.AddTextBox(2, 2, 80, 300)
  textbox.Text = "Text Box in the chart"

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");

  //Creates a storage file from FileOpenPicker
  StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

  //Loads or open an existing workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStorageFile);

  //Access first worksheet from the workbook instance.
  IWorksheet worksheet = workbook.Worksheets[0];

  for (int i = 0; i < worksheet.Charts.Count; i++)
  {                    
    if (worksheet.Rows[i].RowHeight != 0)
    {
      for (int j = 0; j < worksheet.Charts[i].TextBoxes.Count; j++)
      {
        String text = worksheet.Charts[i].TextBoxes[j].Text;
      }
    }
  }
  
  //Creates a new text box in the chart 
  ITextBoxShape textbox = worksheet.Charts[0].TextBoxes.AddTextBox(2, 2, 80, 300);
  textbox.Text = "Text Box in the chart";
  
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
  
  //Creates a storage file from FileSavePicker
  StorageFile outputStorageFile = await savePicker.PickSaveFileAsync();
  
  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(outputStorageFile);

}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Read the text 
  for (int i = 0; i < worksheet.Charts.Count; i++)
  {
    for (int j = 0; j < worksheet.Charts[i].TextBoxes.Count; j++)
    {
      String text = worksheet.Charts[i].TextBoxes[j].Text;
    }
  }

  //Creates a new text box in the chart 
  ITextBoxShape textbox = worksheet.Charts[0].TextBoxes.AddTextBox(2, 2, 80, 300);
  textbox.Text = "Text Box in the chart";

  //Saving the workbook as stream
  FileStream outputStream = new FileStream(Output.xlsx, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(outputStream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Set the default application version
  plication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  string resourcePath = "XamarinSample.Sample.xlsx";
  //"App" is the class of Portable project.
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream(resourcePath);

  //Opens the workbook 
  IWorkbook workbook = application.Workbooks.Open(inputStream);

  //Access first worksheet from the workbook instance.
  IWorksheet worksheet = workbook.Worksheets[0];

  for (int i = 0; i < worksheet.Charts.Count; i++)
  {                 
    for (int j = 0; j < worksheet.Charts[i].TextBoxes.Count; j++)
    {
      String text = worksheet.Charts[i].TextBoxes[j].Text;
    }          
  }

  //Creates a new text box in the chart 
  ITextBoxShape textbox = worksheet.Charts[0].TextBoxes.AddTextBox(2, 2, 80, 300);
  textbox.Text = "Text Box in the chart";

  //Save the workbook to stream in xlsx format. 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);
  workbook.Close();

  //Save the stream as a file in the device and invoke it for viewing
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Check Box

**ICheckBoxShape** object represents a check box in a worksheet. The following code example illustrates how to insert and manipulate a check box control.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create a check box with cell link
  ICheckBoxShape checkBoxRed = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75);
  checkBoxRed.Text = "Red";
  checkBoxRed.CheckState = ExcelCheckState.Unchecked;
  checkBoxRed.LinkedCell = sheet["B2"];
  ICheckBoxShape checkBoxBlue = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75);
  checkBoxBlue.Text = "Blue";
  checkBoxBlue.CheckState = ExcelCheckState.Checked;
  checkBoxBlue.LinkedCell = sheet["B4"];

  //Read a check box
  checkBoxRed = sheet.CheckBoxes[0];
  checkBoxRed.CheckState = ExcelCheckState.Checked;

  //Remove a check box
  checkBoxBlue = sheet.CheckBoxes[1];
  checkBoxBlue.Remove();

  workbook.SaveAs("Checkbox.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Create a check box with cell link
  Dim checkBoxRed As ICheckBoxShape = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75)
  checkBoxRed.Text = "Red"
  checkBoxRed.CheckState = ExcelCheckState.Unchecked
  checkBoxRed.LinkedCell = sheet("B2")
  Dim checkBoxBlue As ICheckBoxShape = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75)
  checkBoxBlue.Text = "Blue"
  checkBoxBlue.CheckState = ExcelCheckState.Checked
  checkBoxBlue.LinkedCell = sheet("B4")

  'Read a check box
  checkBoxRed = sheet.CheckBoxes(0)
  checkBoxRed.CheckState = ExcelCheckState.Checked

  'Remove a check box
  checkBoxBlue = sheet.CheckBoxes(1)
  checkBoxBlue.Remove()

  workbook.SaveAs("Checkbox.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create a check box with cell link
  ICheckBoxShape checkBoxRed = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75);
  checkBoxRed.Text = "Red";
  checkBoxRed.CheckState = ExcelCheckState.Unchecked;
  checkBoxRed.LinkedCell = sheet["B2"];
  ICheckBoxShape checkBoxBlue = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75);
  checkBoxBlue.Text = "Blue";
  checkBoxBlue.CheckState = ExcelCheckState.Checked;
  checkBoxBlue.LinkedCell = sheet["B4"];

  //Read a check box
  checkBoxRed = sheet.CheckBoxes[0];
  checkBoxRed.CheckState = ExcelCheckState.Checked;

  //Remove a check box
  checkBoxBlue = sheet.CheckBoxes[1];
  checkBoxBlue.Remove();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CheckBox";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create a check box with cell link
  ICheckBoxShape checkBoxRed = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75);
  checkBoxRed.Text = "Red";
  checkBoxRed.CheckState = ExcelCheckState.Unchecked;
  checkBoxRed.LinkedCell = sheet["B2"];
  ICheckBoxShape checkBoxBlue = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75);
  checkBoxBlue.Text = "Blue";
  checkBoxBlue.CheckState = ExcelCheckState.Checked;
  checkBoxBlue.LinkedCell = sheet["B4"];

  //Read a check box
  checkBoxRed = sheet.CheckBoxes[0];
  checkBoxRed.CheckState = ExcelCheckState.Checked;

  //Remove a check box
  checkBoxBlue = sheet.CheckBoxes[1];
  checkBoxBlue.Remove();

  //Saving the workbook as stream
  FileStream stream = new FileStream("CheckBox.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create a check box with cell link
  ICheckBoxShape checkBoxRed = sheet.CheckBoxes.AddCheckBox(2, 4, 20, 75);
  checkBoxRed.Text = "Red";
  checkBoxRed.CheckState = ExcelCheckState.Unchecked;
  checkBoxRed.LinkedCell = sheet["B2"];
  ICheckBoxShape checkBoxBlue = sheet.CheckBoxes.AddCheckBox(4, 4, 20, 75);
  checkBoxBlue.Text = "Blue";
  checkBoxBlue.CheckState = ExcelCheckState.Checked;
  checkBoxBlue.LinkedCell = sheet["B4"];

  //Read a check box
  checkBoxRed = sheet.CheckBoxes[0];
  checkBoxRed.CheckState = ExcelCheckState.Checked;

  //Remove a check box
  checkBoxBlue = sheet.CheckBoxes[1];
  checkBoxBlue.Remove();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("CheckBox.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("CheckBox.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add a check box in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Check%20Box). 

### Combo Box

**IComboBoxShape** object represents a combo box in a worksheet. The following code example illustrates how to insert and manipulate a combo box control.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Filling Values
  sheet["A2"].Text = "RGB colors";
  sheet["A3"].Text = "Red";
  sheet["A4"].Text = "Green";
  sheet["A5"].Text = "Blue";
  sheet["B5"].Text = "Selected Index";

  //Create a Combo Box
  IComboBoxShape comboBox1 = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox1.ListFillRange = sheet["A3:A5"];
  comboBox1.LinkedCell = sheet["C5"];
  comboBox1.SelectedIndex = 2;

  //Create a Combo Box
  IComboBoxShape comboBox2 = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox2.ListFillRange = sheet["A3:A5"];
  comboBox2.LinkedCell = sheet["C5"];
  comboBox2.SelectedIndex = 1;

  //Read a Combo Box
  comboBox1 = sheet.ComboBoxes[0];
  comboBox1.SelectedIndex = 1;

  //Remove a Combo Box
  comboBox2 = sheet.ComboBoxes[1];
  comboBox2.Remove();

  workbook.SaveAs("Combobox.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Filling Values
  sheet("A2").Text = "RGB colors"
  sheet("A3").Text = "Red"
  sheet("A4").Text = "Green"
  sheet("A5").Text = "Blue"
  sheet("B5").Text = "Selected Index"

  'Create a Combo Box
  Dim comboBox1 As IComboBoxShape = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100)
  'Assign a value to the Combo Box
  comboBox1.ListFillRange = sheet("A3:A5")
  comboBox1.LinkedCell = sheet("C5")
  comboBox1.SelectedIndex = 2

  'Create a Combo Box
  Dim comboBox2 As IComboBoxShape = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100)
  'Assign a value to the Combo Box
  comboBox2.ListFillRange = sheet("A3:A5")
  comboBox2.LinkedCell = sheet("C5")
  comboBox2.SelectedIndex = 1

  'Read a Combo Box
  comboBox1 = sheet.ComboBoxes(0)
  comboBox1.SelectedIndex = 1

  'Remove a Combo Box
  comboBox2 = sheet.ComboBoxes(1)
  comboBox2.Remove()

  workbook.SaveAs("Combobox.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Filling Values
  sheet["A2"].Text = "RGB colors";
  sheet["A3"].Text = "Red";
  sheet["A4"].Text = "Green";
  sheet["A5"].Text = "Blue";
  sheet["B5"].Text = "Selected Index";

  //Create a Combo Box
  IComboBoxShape comboBox1 = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox1.ListFillRange = sheet["A3:A5"];
  comboBox1.LinkedCell = sheet["C5"];
  comboBox1.SelectedIndex = 2;

  //Create a Combo Box
  IComboBoxShape comboBox2 = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox2.ListFillRange = sheet["A3:A5"];
  comboBox2.LinkedCell = sheet["C5"];
  comboBox2.SelectedIndex = 1;

  //Read a Combo Box
  comboBox1 = sheet.ComboBoxes[0];
  comboBox1.SelectedIndex = 1;

  //Remove a Combo Box
  comboBox2 = sheet.ComboBoxes[1];
  comboBox2.Remove();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ComboBox";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Filling Values
  sheet["A2"].Text = "RGB colors";
  sheet["A3"].Text = "Red";
  sheet["A4"].Text = "Green";
  sheet["A5"].Text = "Blue";
  sheet["B5"].Text = "Selected Index";

  //Create a Combo Box
  IComboBoxShape comboBox1 = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox1.ListFillRange = sheet["A3:A5"];
  comboBox1.LinkedCell = sheet["C5"];
  comboBox1.SelectedIndex = 2;

  //Create a Combo Box
  IComboBoxShape comboBox2 = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox2.ListFillRange = sheet["A3:A5"];
  comboBox2.LinkedCell = sheet["C5"];
  comboBox2.SelectedIndex = 1;

  //Read a Combo Box
  comboBox1 = sheet.ComboBoxes[0];
  comboBox1.SelectedIndex = 1;

  //Remove a Combo Box
  comboBox2 = sheet.ComboBoxes[1];
  comboBox2.Remove();

  //Saving the workbook as stream
  FileStream stream = new FileStream("ComboBox.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Filling Values
  sheet["A2"].Text = "RGB colors";
  sheet["A3"].Text = "Red";
  sheet["A4"].Text = "Green";
  sheet["A5"].Text = "Blue";
  sheet["B5"].Text = "Selected Index";

  //Create a Combo Box
  IComboBoxShape comboBox1 = sheet.ComboBoxes.AddComboBox(2, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox1.ListFillRange = sheet["A3:A5"];
  comboBox1.LinkedCell = sheet["C5"];
  comboBox1.SelectedIndex = 2;

  //Create a Combo Box
  IComboBoxShape comboBox2 = sheet.ComboBoxes.AddComboBox(5, 3, 20, 100);
  //Assign a value to the Combo Box
  comboBox2.ListFillRange = sheet["A3:A5"];
  comboBox2.LinkedCell = sheet["C5"];
  comboBox2.SelectedIndex = 1;

  //Read a Combo Box
  comboBox1 = sheet.ComboBoxes[0];
  comboBox1.SelectedIndex = 1;

  //Remove a Combo Box
  comboBox2 = sheet.ComboBoxes[1];
  comboBox2.Remove();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ComboBox.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ComboBox.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add a combo box in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Combo%20Box). 

### Option Button

**IOptionButtonShape** object represents an option button in a worksheet. The following code example illustrates how to insert and manipulate an option button control.

N> XlsIO provides Option button support only for XLSX format.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create an Option Button
  IOptionButtonShape optionButton1 = sheet.OptionButtons.AddOptionButton(2, 3);
  //Assign a value to the Option Button
  optionButton1.Text = "Fed Ex";

  //Format the control
  optionButton1.Fill.FillType = ExcelFillType.SolidColor;
  optionButton1.Fill.ForeColor = Color.Yellow;
  //Change the check state
  optionButton1.CheckState = ExcelCheckState.Checked;

  //Create an Option Button
  IOptionButtonShape optionButton2 = sheet.OptionButtons.AddOptionButton(5, 3);
  //Assign a value to the Option Button
  optionButton2.Text = "DHL";

  //Read an Option Button
  optionButton1 = sheet.OptionButtons[0];
  optionButton1.CheckState = ExcelCheckState.Unchecked;

  //Remove an Option Button
  optionButton2 = sheet.OptionButtons[1];
  optionButton2.Remove();

  workbook.SaveAs("OptionButton.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Create an Option Button
  Dim optionButton1 As IOptionButtonShape = sheet.OptionButtons.AddOptionButton(2, 3)
  'Assign a value to the Option Button
  optionButton1.Text = "Fed Ex"

  'Format the control
  optionButton1.Fill.FillType = ExcelFillType.SolidColor
  optionButton1.Fill.ForeColor = Color.Yellow
  'Change the check state
  optionButton1.CheckState = ExcelCheckState.Checked

  'Create an Option Button
  Dim optionButton2 As IOptionButtonShape = sheet.OptionButtons.AddOptionButton(5, 3)
  'Assign a value to the Option Button
  optionButton2.Text = "DHL"

  'Read an Option Button
  optionButton1 = sheet.OptionButtons(0)
  optionButton1.CheckState = ExcelCheckState.Unchecked

  'Remove an Option Button
  optionButton2 = sheet.OptionButtons(1)
  optionButton2.Remove()

  workbook.SaveAs("OptionButton.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create an Option Button
  IOptionButtonShape optionButton1 = sheet.OptionButtons.AddOptionButton(2, 3);
  //Assign a value to the Option Button
  optionButton1.Text = "Fed Ex";

  //Format the control
  optionButton1.Fill.FillType = ExcelFillType.SolidColor;
  optionButton1.Fill.ForeColor = Color.FromArgb(255, 255, 255, 0);
  //Change the check state
  optionButton1.CheckState = ExcelCheckState.Checked;

  //Create an Option Button
  IOptionButtonShape optionButton2 = sheet.OptionButtons.AddOptionButton(5, 3);
  //Assign a value to the Option Button
  optionButton2.Text = "DHL";

  //Read an Option Button
  optionButton1 = sheet.OptionButtons[0];
  optionButton1.CheckState = ExcelCheckState.Unchecked;

  //Remove an Option Button
  optionButton2 = sheet.OptionButtons[1];
  optionButton2.Remove();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "OptionButton";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create an Option Button
  IOptionButtonShape optionButton1 = sheet.OptionButtons.AddOptionButton(2, 3);
  //Assign a value to the Option Button
  optionButton1.Text = "Fed Ex";

  //Format the control
  optionButton1.Fill.FillType = ExcelFillType.SolidColor;
  optionButton1.Fill.ForeColor = Color.Yellow;
  //Change the check state
  optionButton1.CheckState = ExcelCheckState.Checked;

  //Create an Option Button
  IOptionButtonShape optionButton2 = sheet.OptionButtons.AddOptionButton(5, 3);
  //Assign a value to the Option Button
  optionButton2.Text = "DHL";

  //Read an Option Button
  optionButton1 = sheet.OptionButtons[0];
  optionButton1.CheckState = ExcelCheckState.Unchecked;

  //Remove an Option Button
  optionButton2 = sheet.OptionButtons[1];
  optionButton2.Remove();

  //Saving the workbook as stream
  FileStream stream = new FileStream("OptionButton.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create an Option Button
  IOptionButtonShape optionButton1 = sheet.OptionButtons.AddOptionButton(2, 3);
  //Assign a value to the Option Button
  optionButton1.Text = "Fed Ex";

  //Format the control
  optionButton1.Fill.FillType = ExcelFillType.SolidColor;
  optionButton1.Fill.ForeColor = Syncfusion.Drawing.Color.Yellow;
  //Change the check state
  optionButton1.CheckState = ExcelCheckState.Checked;

  //Create an Option Button
  IOptionButtonShape optionButton2 = sheet.OptionButtons.AddOptionButton(5, 3);
  //Assign a value to the Option Button
  optionButton2.Text = "DHL";

  //Read an Option Button
  optionButton1 = sheet.OptionButtons[0];
  optionButton1.CheckState = ExcelCheckState.Unchecked;

  //Remove an Option Button
  optionButton2 = sheet.OptionButtons[1];
  optionButton2.Remove();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("OptionButton.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("OptionButton.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add option button in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Option%20Button). 

## Comments

**ICommentShape** object represents a [comment](https://support.office.com/en-au/article/Annotate-a-worksheet-by-using-comments-3b7065dd-531a-4ffe-8f18-8d047a6ccae7) in a worksheet. You can insert both **Regular** and **Rich** **Text** comments. The following code example illustrates how to insert and manipulate comments.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Add Rich Text Comments
  IRange range = sheet.Range["A6"];
  range.AddComment().RichText.Text = "RichText";
  IRichTextString richText = range.Comment.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Color = ExcelKnownColors.Red;
  richText.SetFont(0, 3, redFont);

  workbook.SaveAs("Comments.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Adding comments to a cell
  sheet.Range("A1").AddComment().Text = "Comments"

  'Add Rich Text Comments
  Dim range As IRange = sheet.Range("A6")
  range.AddComment().RichText.Text = "RichText"
  Dim richText As IRichTextString = range.Comment.RichText

  'Formatting first 4 characters
  Dim redFont As IFont = workbook.CreateFont()
  redFont.Bold = True
  redFont.Color = ExcelKnownColors.Red
  richText.SetFont(0, 3, redFont)

  workbook.SaveAs("Comments.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Add Rich Text Comments
  IRange range = sheet.Range["A6"];
  range.AddComment().RichText.Text = "RichText";
  IRichTextString richText = range.Comment.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Color = ExcelKnownColors.Red;
  richText.SetFont(0, 3, redFont);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Comments";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Add Rich Text Comments
  IRange range = sheet.Range["A6"];
  range.AddComment().RichText.Text = "RichText";
  IRichTextString richText = range.Comment.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Color = ExcelKnownColors.Red;
  richText.SetFont(0, 3, redFont);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Comments.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Add Rich Text Comments
  IRange range = sheet.Range["A6"];
  range.AddComment().RichText.Text = "RichText";
  IRichTextString richText = range.Comment.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Color = ExcelKnownColors.Red;
  richText.SetFont(0, 3, redFont);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Comments.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Comments.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add comment in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Comment).

You can also fill the comments with various types of fills by using the **IFill** interface. Following code example illustrates how to fill the comment shape with a TwoColor gradient.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Accessing existing comment
  ICommentShape shape = sheet.Range["A1"].Comment;

  //Format the comment
  shape.Fill.TwoColorGradient();
  shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal;
  shape.Fill.GradientColorType = ExcelGradientColor.TwoColor;
  shape.Fill.ForeColorIndex = ExcelKnownColors.Red;
  shape.Fill.BackColorIndex = ExcelKnownColors.White;

  workbook.SaveAs("FormatComments.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Adding comments to a cell
  sheet.Range("A1").AddComment().Text = "Comments"

  'Accessing existing comment
  Dim shape As ICommentShape = sheet.Range("A1").Comment

  'Format the comment
  shape.Fill.TwoColorGradient()
  shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal
  shape.Fill.GradientColorType = ExcelGradientColor.TwoColor
  shape.Fill.ForeColorIndex = ExcelKnownColors.Red
  shape.Fill.BackColorIndex = ExcelKnownColors.White

  workbook.SaveAs("FormatComments.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Accessing existing comment
  ICommentShape shape = sheet.Range["A1"].Comment;

  //Format the comment
  shape.Fill.TwoColorGradient();
  shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal;
  shape.Fill.GradientColorType = ExcelGradientColor.TwoColor;
  shape.Fill.ForeColorIndex = ExcelKnownColors.Red;
  shape.Fill.BackColorIndex = ExcelKnownColors.White;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "FormatComments";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Accessing existing comment
  ICommentShape shape = sheet.Range["A1"].Comment;

  //Format the comment
  shape.Fill.TwoColorGradient();
  shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal;
  shape.Fill.GradientColorType = ExcelGradientColor.TwoColor;
  shape.Fill.ForeColorIndex = ExcelKnownColors.Red;
  shape.Fill.BackColorIndex = ExcelKnownColors.White;

  //Saving the workbook as stream
  FileStream stream = new FileStream("FormatComments.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Adding comments to a cell
  sheet.Range["A1"].AddComment().Text = "Comments";

  //Accessing existing comment
  ICommentShape shape = sheet.Range["A1"].Comment;

  //Format the comment
  shape.Fill.TwoColorGradient();
  shape.Fill.GradientStyle = ExcelGradientStyle.Horizontal;
  shape.Fill.GradientColorType = ExcelGradientColor.TwoColor;
  shape.Fill.ForeColorIndex = ExcelKnownColors.Red;
  shape.Fill.BackColorIndex = ExcelKnownColors.White;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("FormatComments.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("FormatComments.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to fill comment in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Fill%20Comment).

### Show or Hide Excel Comments

Comments in an Excel document can be shown or hidden using **IsVisible** property. The following code example illustrates this.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding comments in the worksheet
  worksheet.Range["E5"].AddComment();
  worksheet.Range["E15"].AddComment();

  //Adding text in comments
  worksheet.Comments[0].Text = "Comment1";
  worksheet.Comments[1].Text = "Comment2";

  //Show comment
  worksheet.Comments[0].IsVisible = true;
  //Hide comment
  worksheet.Comments[1].IsVisible = false;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding comments in the worksheet
  worksheet.Range("E5").AddComment()
  worksheet.Range("E15").AddComment()

  'Adding text in comments
  worksheet.Comments(0).Text = "Comment1"
  worksheet.Comments(1).Text = "Comment2"

  'Show comment
  worksheet.Comments(0).IsVisible = True
  'Hide comment
  worksheet.Comments(1).IsVisible = False

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding comments in the worksheet
  worksheet.Range["E5"].AddComment();
  worksheet.Range["E15"].AddComment();

  //Adding text in comments
  worksheet.Comments[0].Text = "Comment1";
  worksheet.Comments[1].Text = "Comment2";

  //Show comment
  worksheet.Comments[0].IsVisible = true;
  //Hide comment
  worksheet.Comments[1].IsVisible = false;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding comments in the worksheet
  worksheet.Range["E5"].AddComment();
  worksheet.Range["E15"].AddComment();

  //Adding text in comments
  worksheet.Comments[0].Text = "Comment1";
  worksheet.Comments[1].Text = "Comment2";

  //Show comment
  worksheet.Comments[0].IsVisible = true;
  //Hide comment
  worksheet.Comments[1].IsVisible = false;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding comments in the worksheet
  worksheet.Range["E5"].AddComment();
  worksheet.Range["E15"].AddComment();

  //Adding text in comments
  worksheet.Comments[0].Text = "Comment1";
  worksheet.Comments[1].Text = "Comment2";

  //Show comment
  worksheet.Comments[0].IsVisible = true;
  //Hide comment
  worksheet.Comments[1].IsVisible = false;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to show or hide comment in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Show%20or%20Hide%20Comment).

Following code snippets illustrates how to remove all the comments in existing worksheet.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Comments.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Remove all the comments in worksheet
  sheet.Comments.Clear();

  workbook.Version = ExcelVersion.Excel2013;
  workbook.SaveAs("RemoveComments.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Comments.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Remove all the comments in worksheet
  sheet.Comments.Clear()

  workbook.Version = ExcelVersion.Excel2013
  workbook.SaveAs("RemoveComments.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Remove all the comments in worksheet
  worksheet.Comments.Clear();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "RemoveComments";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Excel2013;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Comments.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Remove all the comments in worksheet
  worksheet.Comments.Clear();

  //Saving the workbook as stream
  FileStream stream = new FileStream("RemoveComments.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Excel2013;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Comments.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Remove all the comments in worksheet
  worksheet.Comments.Clear();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Excel2013;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("RemoveComments.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("RemoveComments.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to remove comment in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Remove%20Comments). 

## AutoShapes

The **IShape** interface represents an [AutoShape](https://support.office.com/en-ca/article/Add-change-or-delete-shapes-4f7931c3-7794-440e-820e-9469ad756f05) in an Excel workbook. 

To learn more about various AutoShape types supported in XlsIO, refer to the **AutoShapeType** enumeration in API section.

The following code example illustrates how to insert and format AutoShapes.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding an AutoShape
  IShape shape1 = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192);
  IShape shape2 = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192);

  //Set the value inside the shape
  shape1.TextFrame.TextRange.Text = "AutoShape";

  //Format the shape
  shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue;
  shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered;

  //Read an AutoShape
  shape1 = worksheet.Shapes[0];
  shape1.TextFrame.TextRange.Text = "RoundedRectangle";

  //Remove an AutoShape
  shape2 = worksheet.Shapes[1];
  shape2.Remove();

  workbook.SaveAs("Autoshapes.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding an AutoShape
  Dim shape1 As IShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192)
  Dim shape2 As IShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192)

  'Set the value inside the shape.
  shape1.TextFrame.TextRange.Text = "AutoShape"

  'Format the shape
  shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue
  shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered

  'Read an AutoShape
  shape1 = worksheet.Shapes(0)
  shape1.TextFrame.TextRange.Text = "RoundedRectangle"

  'Remove an AutoShape
  shape2 = worksheet.Shapes(1)
  shape2.Remove()

  workbook.SaveAs("Autoshapes.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding an AutoShape
  IShape shape1 = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192);
  IShape shape2 = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192);

  //Set the value inside the shape
  shape1.TextFrame.TextRange.Text = "AutoShape";

  //Format the shape
  shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue;
  shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered;

  //Read an AutoShape
  shape1 = worksheet.Shapes[0];
  shape1.TextFrame.TextRange.Text = "RoundedRectangle";

  //Remove an AutoShape
  shape2 = worksheet.Shapes[1];
  shape2.Remove();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "AutoShapes";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding an AutoShape
  IShape shape1 = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192);
  IShape shape2 = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192);

  //Set the value inside the shape
  shape1.TextFrame.TextRange.Text = "AutoShape";

  //Format the shape
  shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue;
  shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered;

  //Read an AutoShape
  shape1 = worksheet.Shapes[0];
  shape1.TextFrame.TextRange.Text = "RoundedRectangle";

  //Remove an AutoShape
  shape2 = worksheet.Shapes[1];
  shape2.Remove();

  //Saving the workbook as stream
  FileStream stream = new FileStream("AutoShapes.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding an AutoShape
  IShape shape1 = worksheet.Shapes.AddAutoShapes(AutoShapeType.RoundedRectangle, 2, 7, 60, 192);
  IShape shape2 = worksheet.Shapes.AddAutoShapes(AutoShapeType.CircularArrow, 8, 7, 60, 192);

  //Set the value inside the shape
  shape1.TextFrame.TextRange.Text = "AutoShape";

  //Format the shape
  shape1.Fill.ForeColorIndex = ExcelKnownColors.Light_blue;
  shape1.TextFrame.VerticalAlignment = ExcelVerticalAlignment.MiddleCentered;

  //Read an AutoShape
  shape1 = worksheet.Shapes[0];
  shape1.TextFrame.TextRange.Text = "RoundedRectangle";

  //Remove an AutoShape
  shape2 = worksheet.Shapes[1];
  shape2.Remove();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("AutoShapes.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("AutoShapes.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add AutoShapes in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/AutoShapes). 

## Group Shapes

Group shape can be used to work with multiple shapes at a single instant. 
For example, you can change positions, size or set colors for all shapes at the same time through a single group shape.

### Create Group Shapes

The shapes in the worksheet can be grouped into a single shape by creating group shape in XlsIO using IGroupShape interface. 

The following code example illustrates how to create a group shape.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("GroupShape.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Select the shapes you want to group	

IShape[] groupItems = new IShape[] { shapes[0], shapes[1] };

// Group the selected shapes

IGroupShape GroupShape = shapes.Group(groupItems);

workbook.SaveAs("GroupShape.xlsx");

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("GroupShape.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)
	
Dim shapes As IShapes = worksheet.Shapes

' Select the shapes you want to group	

Dim groupItems As IShape() = New IShape() {shapes(0), shapes(1)}

' Group the selected shapes

Dim GroupShape As IGroupShape = shapes.Group(groupItems)
	
workbook.SaveAs("GroupShape.xlsx")
	
workbook.Close()
	
excelEngine.Dispose()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();

openPicker.SuggestedStartLocation = PickerLocationId.Desktop;

openPicker.FileTypeFilter.Add(".xlsx");

openPicker.FileTypeFilter.Add(".xls");

StorageFile openFile = await openPicker.PickSingleFileAsync();

//Opens the workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Select the shapes you want to group	

IShape[] groupItems = new IShape[] { shapes[0], shapes[1] };

// Group the selected shapes

IGroupShape GroupShape = shapes.Group(groupItems);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "GroupShape";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

FileStream inputStream = new FileStream("GroupShape.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(inputStream);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Select the shapes you want to group	

IShape[] groupItems = new IShape[] { shapes[0], shapes[1] };

// Group the selected shapes

IGroupShape GroupShape = shapes.Group(groupItems);

FileStream file = new FileStream("GroupShape.xlsx", FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(file);

file.Dispose();

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream("GroupShape.xlsx");

IWorkbook workbook = application.Workbooks.Open(fileStream);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Select the shapes you want to group	

IShape[] groupItems = new IShape[] { shapes[0], shapes[1] };

// Group the selected shapes

IGroupShape GroupShape = shapes.Group(groupItems);

workbook.SaveAs("GroupShape.xlsx");

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

stream.Position = 0;

//Save the document as file and view the saved document

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
  Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("GroupShape.xlsx", "application/msexcel", stream);
}
else
{
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("GroupShape.xlsx", "application/msexcel", stream);
}

excelEngine.Dispose();

{% endhighlight %}

{% endtabs %}  

A complete working example to group shapes in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Group%20Shapes). 

### Ungroup shapes

Group shape can be ungrouped, and its inner shapes are added to worksheet as an individual shape. 

The following code example illustrates how to ungroup the shape.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("GroupShape.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape

shapes.Ungroup(shapes[0] as IGroupShape);

workbook.SaveAs("GroupShape.xlsx");

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("GroupShape.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)
	
Dim shapes As IShapes = worksheet.Shapes

' Ungroup the selected specified group shape

shapes.Ungroup(TryCast(shapes(0), IGroupShape))
	
workbook.SaveAs("GroupShape.xlsx")
	
workbook.Close()
	
excelEngine.Dispose()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();

openPicker.SuggestedStartLocation = PickerLocationId.Desktop;

openPicker.FileTypeFilter.Add(".xlsx");

openPicker.FileTypeFilter.Add(".xls");

StorageFile openFile = await openPicker.PickSingleFileAsync();

//Opens the workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape

shapes.Ungroup(shapes[0] as IGroupShape);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "GroupShape";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

FileStream inputStream = new FileStream("GroupShape.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(inputStream);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape

shapes.Ungroup(shapes[0] as IGroupShape);

FileStream file = new FileStream("GroupShape.xlsx", FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(file);

file.Dispose();

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream("GroupShape.xlsx");

IWorkbook workbook = application.Workbooks.Open(fileStream);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape

shapes.Ungroup(shapes[0] as IGroupShape);

workbook.SaveAs("GroupShape.xlsx");

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

stream.Position = 0;

//Save the document as file and view the saved document

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
  Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("GroupShape.xlsx", "application/msexcel", stream);
}
else
{
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("GroupShape.xlsx", "application/msexcel", stream);
}

excelEngine.Dispose();

{% endhighlight %}

{% endtabs %} 

A complete working example to ungroup shapes in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Ungroup%20Shapes). 

### Ungroup all shapes

When ungrouping the group shape, its immediate inner shapes only be ungrouped. Ungroup the group shape and its all the inner shapes can be possible in XlsIO. 
In Ungroup method, “isAll” boolean value indicates whether the group inner shape will be grouped or not. 

The following code example illustrates how to ungroup the group shape and its inner shapes.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("GroupShape.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape and its inner shapes by specifying isAll property

shapes.Ungroup(shapes[0] as IGroupShape, true);

workbook.SaveAs("GroupShape.xlsx");

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("GroupShape.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)
	
Dim shapes As IShapes = worksheet.Shapes

' Ungroup the selected specified group shape and its inner shapes by specifying isAll property

shapes.Ungroup(TryCast(shapes(0), IGroupShape), True)
	
workbook.SaveAs("GroupShape.xlsx")
	
workbook.Close()
	
excelEngine.Dispose()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();

openPicker.SuggestedStartLocation = PickerLocationId.Desktop;

openPicker.FileTypeFilter.Add(".xlsx");

openPicker.FileTypeFilter.Add(".xls");

StorageFile openFile = await openPicker.PickSingleFileAsync();

//Opens the workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape and its inner shapes by specifying isAll property

shapes.Ungroup(shapes[0] as IGroupShape, true);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "GroupShape";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

FileStream inputStream = new FileStream("GroupShape.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(inputStream);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape and its inner shapes by specifying isAll property

shapes.Ungroup(shapes[0] as IGroupShape, true);

FileStream file = new FileStream("GroupShape.xlsx", FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(file);

file.Dispose();

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

Stream fileStream = assembly.GetManifestResourceStream("GroupShape.xlsx");

IWorkbook workbook = application.Workbooks.Open(fileStream);

IWorksheet worksheet = workbook.Worksheets[0];

IShapes shapes = worksheet.Shapes;

// Ungroup the selected specified group shape and its inner shapes by specifying isAll property

shapes.Ungroup(shapes[0] as IGroupShape, true);

workbook.SaveAs("GroupShape.xlsx");

MemoryStream stream = new MemoryStream();

workbook.SaveAs(stream);

workbook.Close();

stream.Position = 0;

//Save the document as file and view the saved document

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
  Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("GroupShape.xlsx", "application/msexcel", stream);
}
else
{
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("GroupShape.xlsx", "application/msexcel", stream);
}

excelEngine.Dispose();

{% endhighlight %}

{% endtabs %} 

A complete working example to ungroup all shapes in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Excel%20Shapes/Ungroup%20All%20Shapes). 

## OLE Objects 

**IOleObject** object represents an [OLE Object](https://support.office.com/en-US/article/Create-change-or-delete-an-OLE-object-F767F0F1-4170-4850-9B96-0B6C07EC6EA4) in a worksheet. 

N> XlsIO supports OLE Objects for XLSX format in Windows, ASP.NET, and WPF platforms only.

**OLE** **Objects** **and** **Linking** **Types**

XlsIO supports two types of association of the objects:

* Linked objects
* Embedded objects 

**1****.** **Linked** **Objects** 

Linked objects remains as a separate files. When the file is opened in another machine, then the linked object should be in the same location as created.

The following sample code illustrates how to link an OLE Object to an Excel document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  Image image = Image.FromFile("image.png");
  //Select the object, image for the display icon and the type of the OLEObject to insert
  IOleObject ole2 = sheet.OleObjects.Add("Document.docx", image, OleLinkType.Link);

  workbook.SaveAs("LinkedObjects.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  Dim image As Image = Image.FromFile("image.png")
  'Select the object, image for the display icon and the type of the OLEObject to insert
  Dim ole2 As IOleObject = sheet.OleObjects.Add("Document.docx", image, OleLinkType.Link)

  workbook.SaveAs("LinkedObjects.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream imageStream = assembly.GetManifestResourceStream("UWP.Data.image.png");
  //Get image from stream
  Syncfusion.XlsIO.Image image = Syncfusion.XlsIO.Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject = worksheet.OleObjects.AddLink(@"..\..\Data\Document.docx", image);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "LinkedObjects";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create image stream
  FileStream imageStream = new FileStream("image.png", FileMode.Open);
  //Get image from stream
  Image image = Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject = worksheet.OleObjects.AddLink(@"..\..\Data\Document.docx", image);

  //Saving the workbook as stream
  FileStream stream = new FileStream("LinkedObjects.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream imageStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Image.png");
  //Get image from stream
  Syncfusion.Drawing.Image image = Syncfusion.Drawing.Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject = worksheet.OleObjects.AddLink(@"..\..\Data\Document.docx", image);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("LinkedObjects.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("LinkedObjects.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

**2****.** **Embedded** **Objects**  

Embedded objects are stored in the document. When the file is opened in another machine, the embedded object can be viewed without having access to the original data.

The following sample code illustrates how to embed an OLE Object to an Excel document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  Image image = Image.FromFile("image.png");
  // Select the object, image for the display icon and the type of the OLEObject to insert
  IOleObject ole1 = sheet.OleObjects.Add("Test.pptx", image, OleLinkType.Embed);

  workbook.SaveAs("EmbeddedObjects.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  Dim image As Image = Image.FromFile("image.png")
  'Select the object, image for the display icon and the type of the OLEObject to insert
  Dim ole1 As IOleObject = sheet.OleObjects.Add("Test.pptx", image, OleLinkType.Embed)

  workbook.SaveAs("EmbeddedObjects.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("UWP.Data.Test.pptx");
  Stream imageStream = assembly.GetManifestResourceStream("UWP.Data.image.png");

  //Get image from stream
  Syncfusion.XlsIO.Image image = Syncfusion.XlsIO.Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject = worksheet.OleObjects.Add(inputStream, image, OleObjectType.PowerPointPresentation);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "EmbeddedObjects";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create file stream and image stream
  FileStream inputStream = new FileStream("Test.pptx", FileMode.Open);
  FileStream imageStream = new FileStream("image.png", FileMode.Open);

  //Get image from stream
  Image image = Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject = worksheet.OleObjects.Add(inputStream, image, OleObjectType.PowerPointPresentation);

  //Saving the workbook as stream
  FileStream stream = new FileStream("EmbeddedObjects.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Test.pptx");
  Stream imageStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Image.png");
  //Get image from stream
  Syncfusion.Drawing.Image image = Syncfusion.Drawing.Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject = worksheet.OleObjects.Add(inputStream, image, OleObjectType.PowerPointPresentation);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("EmbeddedObjects.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("EmbeddedObjects.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

The following code example illustrates how to insert and manipulate OLEObjects with their properties. 

To learn more about OLEObjects, refer to the **IOleObjects** in API section.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Icon image
  Image image = Image.FromFile("Images.png");

  //Select the object, image for the display icon and the type of the OLEObject to insert
  IOleObject oleObject1 = sheet.OleObjects.Add("Employee.docx", image, OleLinkType.Embed);

  //Select the object, image for the display icon and the type of the OLEObject to insert
  IOleObject oleObject2 = sheet.OleObjects.Add("Customer.docx", image, OleLinkType.Embed);

  //Displays image as icon
  oleObject1.DisplayAsIcon = true;

  //Set the location of the OleObject
  oleObject1.Location = sheet["K8"];

  //Reads icon as a image
  Image image1 = oleObject1.Picture;

  //Reads OleObject as a IPictureShape
  IPictureShape shape = oleObject1.Shape;

  //Set the size of the OleObject
  oleObject1.Size = new Size(30, 30);

  //Remove OleObjects
  oleObject2 = sheet.OleObjects[1];
  oleObject2.Shape.Remove();

  workbook.SaveAs("OleObjects.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Icon image
  Dim image As Image = Image.FromFile("Images.png")

  'Select the object, image for the display icon and the type of the OLEObject to insert
  Dim oleObject1 As IOleObject = sheet.OleObjects.Add("Employee.docx", image, OleLinkType.Embed)

  'Select the object, image for the display icon and the type of the OLEObject to insert
  Dim oleObject2 As IOleObject = sheet.OleObjects.Add("Customer.docx", image, OleLinkType.Embed)

  'Displays image as icon
  oleObject1.DisplayAsIcon = True

  'Set the location of the OleObject
  oleObject1.Location = sheet("K8")

  'Reads icon as a image
  Dim image1 As Image = oleObject1.Picture

  'Reads OleObject as a IPictureShape
  Dim shape As IPictureShape = oleObject1.Shape

  'Set the size of the OleObject
  oleObject1.Size = New Size(30, 30)

  'Remove OleObjects
  oleObject2 = sheet.OleObjects(1)
  oleObject2.Shape.Remove()

  workbook.SaveAs("OleObjects.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream1 = assembly.GetManifestResourceStream("UWP.Data.Employee.docx");
  Stream inputStream2 = assembly.GetManifestResourceStream("UWP.Data.Customer.docx");
  Stream imageStream = assembly.GetManifestResourceStream("UWP.Data.Images.png");

  //Get image from stream
  Syncfusion.XlsIO.Image image = Syncfusion.XlsIO.Image.FromStream(imageStream);
  
  //Add ole object
  IOleObject oleObject1 = worksheet.OleObjects.Add(inputStream1, image, OleObjectType.WordDocument);
  IOleObject oleObject2 = worksheet.OleObjects.Add(inputStream2, image, OleObjectType.WordDocument);

  //Displays image as icon
  oleObject1.DisplayAsIcon = true;

  //Set the location of the OleObject
  oleObject1.Location = worksheet["K8"];

  //Reads icon as a image
  Syncfusion.XlsIO.Image image1 = oleObject1.Picture;

  //Reads OleObject as a IPictureShape
  IPictureShape shape = oleObject1.Shape;

  //Set the size of the OleObject
  oleObject1.Size = new Size(30, 30);

  //Remove OleObjects
  oleObject2 = worksheet.OleObjects[1];
  oleObject2.Shape.Remove();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "OleObjects";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create file stream and image stream
  FileStream inputStream1 = new FileStream("Employee.docx", FileMode.Open);
  FileStream inputStream2 = new FileStream("Customer.docx", FileMode.Open);
  FileStream imageStream = new FileStream("Images.png", FileMode.Open);

  //Get image from stream
  Image image = Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject1 = worksheet.OleObjects.Add(inputStream1, image, OleObjectType.WordDocument);
  IOleObject oleObject2 = worksheet.OleObjects.Add(inputStream2, image, OleObjectType.WordDocument);

  //Displays image as icon
  oleObject1.DisplayAsIcon = true;

  //Set the location of the OleObject
  oleObject1.Location = worksheet["K8"];

  //Reads icon as a image
  Image image1 = oleObject1.Picture;

  //Reads OleObject as a IPictureShape
  IPictureShape shape = oleObject1.Shape;

  //Set the size of the OleObject
  oleObject1.Size = new Size(30, 30);

  //Remove OleObjects
  oleObject2 = worksheet.OleObjects[1];
  oleObject2.Shape.Remove();

  //Saving the workbook as stream
  FileStream stream = new FileStream("OleObjects.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream1 = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Employee.docx");
  Stream inputStream2 = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Customer.docx");
  Stream imageStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Images.png");
  //Get image from stream
  Syncfusion.Drawing.Image image = Syncfusion.Drawing.Image.FromStream(imageStream);

  //Add ole object
  IOleObject oleObject1 = worksheet.OleObjects.Add(inputStream1, image, OleObjectType.WordDocument);
  IOleObject oleObject2 = worksheet.OleObjects.Add(inputStream2, image, OleObjectType.WordDocument);

  //Displays image as icon
  oleObject1.DisplayAsIcon = true;

  //Set the location of the OleObject
  oleObject1.Location = worksheet["K8"];

  //Reads icon as a image
  Syncfusion.Drawing.Image image1 = oleObject1.Picture;

  //Reads OleObject as a IPictureShape
  IPictureShape shape = oleObject1.Shape;

  //Set the size of the OleObject
  oleObject1.Size = new Syncfusion.Drawing.Size(30, 30);

  //Remove OleObjects
  oleObject2 = worksheet.OleObjects[1];
  oleObject2.Shape.Remove();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("OleObjects.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("OleObjects.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  


