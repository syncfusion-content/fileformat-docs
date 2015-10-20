## Working with Barcode

Essential PDF provides support to add barcodes to the PDF document. The following barcode types are supported.

* 10 one-dimensional barcodes including Code 39 and Code 32 barcodes.
* 2 two-dimensional barcodes such as QR and DataMatrix barcode
### Adding a one dimensional barcode to the PDF document


The below code snippet shows how to add Code39 barcode to a PDF document.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creating new PDF Document<br/><br/>PdfDocument doc = new PdfDocument();<br/><br/>//Adding new page to PDF document<br/><br/>PdfPage page = doc.Pages.Add();<br/><br/>//Drawing Code39 barcode <br/><br/>PdfCode39Barcode barcode = new PdfCode39Barcode(); <br/><br/>//Setting height of the barcode <br/><br/>barcode.BarHeight = 45; <br/><br/>barcode.Text = "CODE39$"; <br/><br/>//Printing barcode on to the Pdf. <br/><br/>barcode.Draw(page, new PointF(25, 70 ));<br/><br/>//Saving the Document<br/><br/>doc.Save("CODE39.pdf");<br/><br/></td></tr>
</table>


<table>
<tr>
<td>
**[****VB****]**<br/><br/>'Creating new PDF Document<br/><br/>Dim doc As New PdfDocument()<br/><br/>'Adding new page to PDF document<br/><br/>Dim page As PdfPage = doc.Pages.Add()<br/><br/>'Drawing Code39 barcode <br/><br/>Dim barcode As New PdfCode39Barcode()<br/><br/>'Setting height of the barcode <br/><br/>barcode.BarHeight = 45<br/><br/>barcode.Text = "CODE39$"<br/><br/>'Printing barcode on to the Pdf. <br/><br/>barcode.Draw(page, New PointF(25, 70))<br/><br/>'Saving the Document<br/><br/>doc.Save("CODE39.pdf")           <br/><br/><br/><br/></td></tr>
</table>


### Adding a two dimensional barcode to a PDF document

The below code snippet shows how to add a QR code to the PDF document.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Drawing QR Barcode<br/><br/>PdfQRBarcode barcode = new PdfQRBarcode();<br/><br/>//Set Error Correction Level<br/><br/>barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High;<br/><br/>//Set XDimension<br/><br/>barcode.XDimension = 3;<br/><br/>barcode.Text = "http://www.syncfusion.com";<br/><br/>//Creating new PDF Document<br/><br/>PdfDocument doc = new PdfDocument();<br/><br/>//Adding new page to PDF document<br/><br/>PdfPage page = doc.Pages.Add();<br/><br/>//Printing barcode on to the Pdf. <br/><br/>barcode.Draw(page, new PointF(25, 70));<br/><br/>//Saving the Document<br/><br/>doc.Save("QRBarcode.pdf");<br/><br/></td></tr>
</table>


<table>
<tr>
<td>
**[****VB****]**<br/><br/>'Drawing QR Barcode<br/><br/>Dim barcode As New PdfQRBarcode()<br/><br/>'Set Error Correction Level<br/><br/>barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High<br/><br/>'Set XDimension<br/><br/>barcode.XDimension = 3<br/><br/>barcode.Text = "http://www.syncfusion.com"<br/><br/>'Creating new PDF Document<br/><br/>Dim doc As New PdfDocument()<br/><br/>'Adding new page to PDF document<br/><br/>Dim page As PdfPage = doc.Pages.Add()<br/><br/>'Printing barcode on to the Pdf. <br/><br/>barcode.Draw(page, New PointF(25, 70))<br/><br/>'Saving the Document<br/><br/>doc.Save("QRBarcode.pdf")<br/><br/><br/><br/><br/><br/></td></tr>
</table>


### Customizing the barcode appearance

The height of the barcode can be changed using the **BarHeight** property. The equivalent property to change the block size for two dimensional barcode is **XDimension**. You can also customize the barcode color by changing the DarkBarColor and LightBarColor properties.

**Note****:** This color customization is possible only for one dimensional barcodes and it is not supported for two dimensional barcodes.

### Supported barcode types

The following table contains the supported types and associated valid characters.

<table>
<tr>
<td>
**Symbol**<br/><br/></td><td>
**Supported** **characters**<br/><br/></td><td>
**Length**<br/><br/></td></tr>
<tr>
<td>
{{'[QR Code](https://en.wikipedia.org/wiki/QR_code#"")'| markdownify }}<br/><br/></td><td>
[0–9]; [A–Z (upper-case only)]; [space $ % * + - . / , :]; [Shift JIS characters]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[DataMatrix](https://en.wikipedia.org/wiki/Data_Matrix#"")'| markdownify }}<br/><br/></td><td>
All ASCII characters<br/><br/></td><td>
<br/><br/></td></tr>
<tr>
<td>
{{'[Code 39](https://en.wikipedia.org/wiki/Code_39#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [- . $ / + % SPACE]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 39 Extended](https://en.wikipedia.org/wiki/Code_39#Full_ASCII_Code_39"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [a-z]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 11](https://en.wikipedia.org/wiki/Code_11#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [-]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Codabar](https://en.wikipedia.org/wiki/Codabar#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [- $ : / . +]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
Code 32<br/><br/></td><td>
[0-9]<br/><br/></td><td>
8<br/><br/></td></tr>
<tr>
<td>
{{'[Code 93](https://en.wikipedia.org/wiki/Code_93#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [- . $ / + % SPACE]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 93 Extended](https://en.wikipedia.org/wiki/Code_93#Full_ASCII_Code_93"")'| markdownify }}<br/><br/></td><td>
All 128 ASCII characters<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 128A](https://en.wikipedia.org/wiki/Code_128#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [NUL (0x00) SOH (0x01) STX (0x02) ETX (0x03) EOT(0x04) ENQ (0x05) ACK (0x06) BEL (0x07) BS (0x08) HT (0x09) LF (0x0A) VT(0x0B) FF (0x0C) CR (0x0D) SO (0x0E) SI (0x0F) DLE (0x10) DC1 (0x11) DC2(0x12) DC3 (0x13) DC4 (0x14) NAK (0x15) SYN (0x16) ETB (0x17) CAN(0x18) EM (0x19) SUB (0x1A) ESC (0x1B) FS (0x1C) GS (0x1D) RS (0x1E) US(0x1F) SPACE (0x20)]; [" ! # $ % & ' ( ) * + , - . / ; < = > ? @ [ / ]^ _ ]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 128B](https://en.wikipedia.org/wiki/Code_128#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [a-z]; [SPACE (0x20) ! " # $ % & ' ( ) * + , - . / :; < = > ? @ [ / ]^ _ ` { | } ~ DEL (•) ]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 128C](https://en.wikipedia.org/wiki/Code_128#"")'| markdownify }}<br/><br/></td><td>
ASCII 00-99(encodes each two digit with one code)<br/><br/></td><td>
variable<br/><br/></td></tr>
</table>
