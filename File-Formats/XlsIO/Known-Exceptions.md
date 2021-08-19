---
title: Known exceptions thrown in XlsIO | Syncfusion
description: Learn here all about the Known exceptions thrown in the Syncfusion's Excel (XlsIO) Library and more.
platform: file-formats
control: XlsIO
documentation: UG
---
# Known Exceptions Details in Excel Library

The list of known exceptions thrown in Essential XlsIO is listed below.

## ApplicationException

<table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td>
      Workbook
    </td>
    <td>
       "Workbook was not created from file." + " That is why workbook file not specified." + " You must use SaveAs method instead."
    </td>
    <td>
      The file name cannot be empty
    </td>
  </tr>
  <tr>
    <td ROWSPAN="4">
      Worksheet
    </td>
    <td>
       "Can't deselect all worksheets."
    </td>
    <td>
      Can't deselect all worksheets
    </td>
  </tr>
  <tr>
    <td>
       "Can't find data for MSODrawing"
    </td>
    <td>
      The value of current mso index cannot greater than array drawings count
    </td>
  </tr>
  <tr>
    <td>
       "Sheet is already protected, before use unprotect method"
    </td>
    <td>
      The property is true the sheet is already protected
    </td>
  </tr>
  <tr>
    <td>
      "You cannot use this command on a protected sheet
    </td>
    <td>
      The condition is false you cannot use this command on protected sheet
    </td>
  </tr>
</table>
 
## ArgumentException
 
 <table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td>
      Pictures
    </td>
    <td>
      string cannot be empty.
    </td>
    <td>
      Valid filename of the image must be provided.
    </td>
  </tr>
  <tr>
    <td ROWSPAN="14">
      Shape
    </td>
    <td>
      From center style support only var_1 or var_2
    </td>
    <td>
      From center style support only var_1 or var_2
    </td>
  </tr>
  <tr>
    <td>
      strName cannot be null or empty.
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      strShapeName - string cannot be empty.
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      The rotation value should be between -3600 and 3600
    </td>
    <td>
      The rotation value should be between -3600 and 3600
    </td>
  </tr>
  <tr>
    <td>
      Name cannot be null or empty
    </td>
    <td>
      Name of the UserPicture cannot be empty.
    </td>
  </tr>
  <tr>
    <td>
      Path cannot be null or empty
    </td>
    <td>
      Path of the UserPicture cannot be null or empty.
    </td>
  </tr>
  <tr>
    <td>
      Path cannot be null or empty
    </td>
    <td>
      Path of the UserTexture cannot be empty.
    </td>
  </tr>
  <tr>
    <td>
      Shape name cannot be null.
    </td>
    <td>
      Valid name is not found for the shape.
    </td>
  </tr>
  <tr>
    <td>
      The specified value is out of range
    </td>
    <td>
      TextureHorizontalScale must be &gt;= 21475.
    </td>
  </tr>
  <tr>
    <td>
       The specified value is out of range
    </td>
    <td>
      TextureOffsetX must be &gt;= 169056.
    </td>
  </tr>
  <tr>
    <td>
       The specified value is out of range
    </td>
    <td>
      TextureOffsetY must be &gt;= 169056.
    </td>
  </tr>
  <tr>
    <td>
       The specified value is out of range
    </td>
    <td>
      TextureVerticalScale must be &gt;= 21475.
    </td>
  </tr>
  <tr>
    <td>
      This method supports only preset textured
    </td>
    <td>
      Custom gradient texture does not support.
    </td>
  </tr>
  <tr>
    <td>
      TransparencyColor
    </td>
    <td>
      The TransparencyFrom on shape should not be less than 0 and greater than 1.
    </td>
  </tr>
  <tr>
    <td>
      TextBox
    </td>
    <td>
      "Reference is not valid
    </td>
    <td>
      The value of the string index 0 is equal to "=" the reference is not valid
    </td>
  </tr>
  <tr>
    <td ROWSPAN="12">
      Workbook
    </td>
    <td>
       "Can't refer to external worksheets"
    </td>
    <td>
      Cannot refer to external workbook
    </td>
  </tr>
  <tr>
    <td>
       "FileName cannot be empty."
    </td>
    <td>
      The file name cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "fileName"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "name"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "Names array must contain at least one name."
    </td>
    <td>
      Names array must contain at least one name
    </td>
  </tr>
  <tr>
    <td>
      "separator"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "strFileName - string cannot be empty."
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "strName - string cannot be empty"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "strSheetName"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "Workbook is protected and password wasn't specified."
    </td>
    <td>
      Workbook is protected and password wasn't specified
    </td>
  </tr>
  <tr>
    <td>
      "Contains invalid characters
    </td>
    <td>
      Contains invalid characters
    </td>
  </tr>
  <tr>
    <td>
      "FileName cannot be empty.
    </td>
    <td>
      The file name cannot be empty
    </td>
  </tr>
  <tr>
    <td ROWSPAN="18">
      Worksheet
    </td>
    <td>
       "arrDataColumns can't be empty"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "Cannot sets formula value in cell that doesn't contain formula"
    </td>
    <td>
      Cannot sets formula value in cell that doesn't contain formula
    </td>
  </tr>
  <tr>
    <td>
       "Can't insert column"
    </td>
    <td>
      Cannot insert column given condition is false
    </td>
  </tr>
  <tr>
    <td>
       "Can't insert row"
    </td>
    <td>
      Cannot insert row given condition is true
    </td>
  </tr>
  <tr>
    <td>
       "cellFormat"
    </td>
    <td>
      The array extend formats count is not less than cell format index value
    </td>
  </tr>
  <tr>
    <td>
       "defaultStyle"
    </td>
    <td>
      The XF index value is not equal to minimum value of the integer
    </td>
  </tr>
  <tr>
    <td>
       "Each range argument should contain a single cell"
    </td>
    <td>
      Each range argument should contain a single cell
    </td>
  </tr>
  <tr>
    <td>
       "FileName cannot be empty."
    </td>
    <td>
      File name cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "Image Path doesn't exist"
    </td>
    <td>
      Image path does not exist
    </td>
  </tr>
  <tr>
    <td>
       "Ranges do not fit each other"
    </td>
    <td>
      The Ranges do not fit each other
    </td>
  </tr>
  <tr>
    <td>
       "separator"
    </td>
    <td>
      String cannot be null or empty
    </td>
  </tr>
  <tr>
    <td>
       "strName - string cannot be empty."
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "Workbook at least must contains one worksheet. You cannot remove last worksheet.", "sheet"
    </td>
    <td>
      Workbook at least must contain one worksheet. You cannot remove last worksheet
    </td>
  </tr>
  <tr>
    <td>
       "Workbook must contains at least one worksheet. You cannot remove last worksheet.", "sheet"
    </td>
    <td>
      Workbook must contain at least one worksheet. You cannot remove last worksheet
    </td>
  </tr>
  <tr>
    <td>
      "Invalid column index.
    </td>
    <td>
      The column index is not less than 0 and greater than 0x3fff
    </td>
  </tr>
  <tr>
    <td>
      "Invalid row index.
    </td>
    <td>
      The row index is not less than 0 and greater than 0xfffff
    </td>
  </tr>
  <tr>
    <td>
      "separator
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      Sheet Name is InValid
    </td>
    <td>
      Sheet Name is InValid
    </td>
  </tr>
</table>

## ArgumentNullException

<table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td ROWSPAN="4">
      Workbook
    </td>
    <td>
       "Name can't be NULL."
    </td>
    <td>
      Name can't be NULL
    </td>
  </tr>
  <tr>
    <td>
       "separator"
    </td>
    <td>
      The string cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "styleIndexes"
    </td>
    <td>
      The style index is not equal to null
    </td>
  </tr>
  <tr>
    <td>
      "password
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td ROWSPAN="5">
      Worksheet
    </td>
    <td>
       "Conditions"
    </td>
    <td>
      The condition property is not null and CFExRecords property is not equal to null
    </td>
  </tr>
  <tr>
    <td>
       "firstColumn"
    </td>
    <td>
      The column index value is not equal to 0 and greater than book maximum column count
    </td>
  </tr>
  <tr>
    <td>
       "password"
    </td>
    <td>
      The string cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "separator"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      "dataSource
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
</table>
	
## ArgumentOutOfRangeException

<table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td ROWSPAN="3">
      PageSetup
    </td>
    <td>
      Parts array must have only three elements.
    </td>
    <td>
      The header/footer string should have 3 parts.
    </td>
  </tr>
  <tr>
    <td>
      The string is too long. Reduce the number of characters used.
    </td>
    <td>
      The header/footer value exceeds the characters limit.
    </td>
  </tr>
  <tr>
    <td>
      Zoom value must be between 10 and 400 percent.
    </td>
    <td>
      The zoom value in page setup should me within the given limit.
    </td>
  </tr>
  <tr>
    <td ROWSPAN="21">
      Shape
    </td>
    <td>
      BottomRowOffset
    </td>
    <td>
      The BottomRowOffset should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      Height
    </td>
    <td>
      The Height should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      iColumn1
    </td>
    <td>
      The column should not be less than 1 and greater than maximum column count.
    </td>
  </tr>
  <tr>
    <td>
      iColumn2
    </td>
    <td>
      The column should not be less than 1 and greater than maximum column count.
    </td>
  </tr>
  <tr>
    <td>
      iPixels
    </td>
    <td>
      The pixels should not be less than 0 and greater than row height.
    </td>
  </tr>
  <tr>
    <td>
      Can't be less than zero.
    </td>
    <td>
      The iPixels should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      iRow1
    </td>
    <td>
      The row value should not be less than 1 and greater than maximum row count.
    </td>
  </tr>
  <tr>
    <td>
      iRow2
    </td>
    <td>
      The row value should not less than 1 and greater than maximum row count.
    </td>
  </tr>
  <tr>
    <td>
      LeftColumnOffset
    </td>
    <td>
      The LeftColumnOffset should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      RightColumnOffset
    </td>
    <td>
      The RightColumnOffset should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      scaleHeight
    </td>
    <td>
      The ScaleHeight should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      scaleWidth
    </td>
    <td>
      The ScaleWidth should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      TopRowOffset
    </td>
    <td>
      The TopRowOffset should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      Value
    </td>
    <td>
      The Transparency should not be less than 0 and greater than 1.
    </td>
  </tr>
  <tr>
    <td>
      Weight
    </td>
    <td>
      The Weight should not be less than 0 and greater than maximum line weight value.
    </td>
  </tr>
  <tr>
    <td>
      Width
    </td>
    <td>
      The Width should not be less than 0.
    </td>
  </tr>
  <tr>
    <td>
      iPixels can't be less than zero.
    </td>
    <td>
      The iPixels should not be less than 0
    </td>
  </tr>
  <tr>
    <td>
      Gradient degree is out of range
    </td>
    <td>
      The gradient range should not be less than -1 and greater than 1.
    </td>
  </tr>
  <tr>
    <td>
      Transparency
    </td>
    <td>
      The Transparency on shape should not be less than 0 and greater than 1.
    </td>
  </tr>
  <tr>
    <td>
      TransparencyFrom
    </td>
    <td>
      The TransparencyFrom value on shape should not be less than 0 and greater than 1.
    </td>
  </tr>
  <tr>
    <td>
      TransparencyTo
    </td>
    <td>
      The TransparencyTo value on shape should not be less than 0 and greater than 1.
    </td>
  </tr>
  <tr>
    <td ROWSPAN="17">
      Workbook
    </td>
    <td>
       "ActiveSheetIndex"
    </td>
    <td>
      The sheet value is not less than 0 and greater than list object count
    </td>
  </tr>
  <tr>
    <td>
       "Array cannot contain more than 4 selection records"
    </td>
    <td>
      Array cannot contain more than 4 selection records
    </td>
  </tr>
  <tr>
    <td>
       "DisplayedTab", "Displayed tab must be greater than zero and less than Worksheets count"
    </td>
    <td>
      Displayed tab must be greater than zero and less than Worksheets count
    </td>
  </tr>
  <tr>
    <td>
       "fileName"
    </td>
    <td>
      The file name cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "fullName"
    </td>
    <td>
      String cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "index"
    </td>
    <td>
      Value cannot be less than 0 and greater than Count
    </td>
  </tr>
  <tr>
    <td>
       "index", "Index cannot be less than 0 and larger than Palette colors array size."
    </td>
    <td>
      Index cannot be less than 0 and larger than Palette colors array size
    </td>
  </tr>
  <tr>
    <td>
       "index", "Value cannot be less than 0 and greater than Count - 1."
    </td>
    <td>
      Value cannot be less than 0 and greater than Count - 1
    </td>
  </tr>
  <tr>
    <td>
       "iRef"
    </td>
    <td>
      The reference index value is not less than or equal to  extern sheet reference and less than 0;
    </td>
  </tr>
  <tr>
    <td>
       "iReferenceIndex", "Value cannot be less than 0 and greater than arrRefs.Count - 1"
    </td>
    <td>
      Value cannot be less than 0 and greater than arrRefs.Count - 1
    </td>
  </tr>
  <tr>
    <td>
       "iStartIndex"
    </td>
    <td>
      The start index value is not less than stro0 and greater than color count
    </td>
  </tr>
  <tr>
    <td>
       "maxCount"
    </td>
    <td>
      The XF index value is not less than or equal to 0
    </td>
  </tr>
  <tr>
    <td>
       "PasswordToOpen", "Password too long. Maximum password length is 15 characters."
    </td>
    <td>
      Password too long. Maximum password length is 15 characters
    </td>
  </tr>
  <tr>
    <td>
       "referenceIndex", "Value cannot be less than 0 and greater than arrRefs.Count - 1"
    </td>
    <td>
      Value cannot be less than 0 and greater than arrRefs.Count - 1
    </td>
  </tr>
  <tr>
    <td>
       "sheetsQuantity", "Quantity of worksheets must be greater than zero."
    </td>
    <td>
      Quantity of worksheets must be greater than zero
    </td>
  </tr>
  <tr>
    <td>
      string.Format( "index is {0}, Count is {1}", index, List.Count)
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td>
      string.Format("index is {0}, Count is {1}", index, count)
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td ROWSPAN="51">
      Worksheet
    </td>
    <td>
       "Apostrophe can't be used as first and/or last character of the worksheet's name."
    </td>
    <td>
      Apostrophe can't be used as first and/or last character of the worksheet's name
    </td>
  </tr>
  <tr>
    <td>
       "Chart index"
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td>
       "column index"
    </td>
    <td>
      The column index value is not equal to 0 and greater than book maximum column count
    </td>
  </tr>
  <tr>
    <td>
       "Column", "Column index cannot be larger then 256 or less then one"
    </td>
    <td>
      Column index cannot be larger than 256 or less than one
    </td>
  </tr>
  <tr>
    <td>
       "columnIndex", "Value cannot be less than 0 and greater than 255"
    </td>
    <td>
      Value cannot be less than 0 and greater than 255
    </td>
  </tr>
  <tr>
    <td>
       "count"
    </td>
    <td>
      The count is not less than 0
    </td>
  </tr>
  <tr>
    <td>
       "drawingItemName"
    </td>
    <td>
      The string name cannot be empty
    </td>
  </tr>
  <tr>
    <td>
       "firstColumn"
    </td>
    <td>
      The column index value is not equal to 0 and greater than book maximum column count
    </td>
  </tr>
  <tr>
    <td>
       "firstRow"
    </td>
    <td>
      The row index value is not equal to 0 and greater than book maximum rows count
    </td>
  </tr>
  <tr>
    <td>
       "iColumn can't be less than 1"
    </td>
    <td>
      iColumn can't be less than 1
    </td>
  </tr>
  <tr>
    <td>
       "iColumnCount", "Value cannot be less 1 and greater than max column index"
    </td>
    <td>
      Value cannot be less 1 and greater than max column index
    </td>
  </tr>
  <tr>
    <td>
       "iColumnIndex", "Column index is out of range."
    </td>
    <td>
      Column index is out of range
    </td>
  </tr>
  <tr>
    <td>
       "iColumnIndex", "Value cannot be less 1 and greater than max column index."
    </td>
    <td>
      Value cannot be less 1 and greater than max column index.
    </td>
  </tr>
  <tr>
    <td>
       "iColumnIndex", "Value cannot be less than 1 and greater than m_book.MaxColumnCount."
    </td>
    <td>
      Value cannot be less than 1 and greater than m_book.MaxColumnCount
    </td>
  </tr>
  <tr>
    <td>
       "iCondFmtPos"
    </td>
    <td>
       The index value is not less than 0
    </td>
  </tr>
  <tr>
    <td>
       "iCustomPropertyPos"
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td>
       "iDValPos"
    </td>
    <td>
      The integer value is not less than 0
    </td>
  </tr>
  <tr>
    <td>
       "index &lt; 0"
    </td>
    <td>
      The index value is not less than 0
    </td>
  </tr>
  <tr>
    <td>
       "index"
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td>
       "index", "Value cannot be less than 0 and greater than Count - 1."
    </td>
    <td>
      Value cannot be less than 0 and greater than Count - 1
    </td>
  </tr>
  <tr>
    <td>
       "iNewIndex"
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td>
       "iOldIndex"
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
  <tr>
    <td>
       "iRowIndex"
    </td>
    <td>
      The row index value is not equal to 0 and greater than book maximum rows count
    </td>
  </tr>
  <tr>
    <td>
       "iRowIndex", "Value cannot be less 1 and greater than max row index."
    </td>
    <td>
      Value cannot be less 1 and greater than max row index
    </td>
  </tr>
  <tr>
    <td>
       "iRowIndex", "Value cannot be less than 1 and greater than m_book.MaxColumnCount."
    </td>
    <td>
      Value cannot be less than 1 and greater than m_book.MaxColumnCount
    </td>
  </tr>
  <tr>
    <td>
       "iSSTIndex"
    </td>
    <td>
      The shared string index value is not less than 0 or greater than book inner shared string count
    </td>
  </tr>
  <tr>
    <td>
       "iStartIndex"
    </td>
    <td>
      The index value is not less than 0
    </td>
  </tr>
  <tr>
    <td>
       "Length of the password can't be more than " + DEF_MAX_PASSWORDLEN
    </td>
    <td>
      The password length value is greater than default maximum password length
    </td>
  </tr>
  <tr>
    <td>
       "maxCount"
    </td>
    <td>
      The index value is not less than or equal to 0
    </td>
  </tr>
  <tr>
    <td>
       "range"
    </td>
    <td>
      The range of the row and column is not equal to range of the last column and last row
    </td>
  </tr>
  <tr>
    <td>
       "rowIndex"
    </td>
    <td>
      The row index value is not less than 1 and greater than book maximum count
    </td>
  </tr>
  <tr>
    <td>
       "Standard Row Height"
    </td>
    <td>
      The standard row height value is not less than 0
    </td>
  </tr>
  <tr>
    <td>
       "Text value cannot be null or empty"
    </td>
    <td>
      Text value cannot be null or empty
    </td>
  </tr>
  <tr>
    <td>
       "Text value cannot be null or empty. First symbol must be '#'"
    </td>
    <td>
      Text value cannot be null or empty. First symbol must be '#'
    </td>
  </tr>
  <tr>
    <td>
       "Text value cannot be null or empty. First symbol of formula cannot be '='"
    </td>
    <td>
      Text value cannot be null or empty. First symbol of formula cannot be '='
    </td>
  </tr>
  <tr>
    <td>
       "Value cannot be less 1 and greater than max column index."
    </td>
    <td>
      Value cannot be less 1 and greater than maximum column index
    </td>
  </tr>
  <tr>
    <td>
       "Value does not valid error string."
    </td>
    <td>
      Given value does not contains dictionary
    </td>
  </tr>
  <tr>
    <td>
       "Worksheets collection does not contain specified worksheet."
    </td>
    <td>
      Worksheets collection does not contain specified worksheet
    </td>
  </tr>
  <tr>
    <td>
       "Zoom", "Zoom must be in range from 10 till 400."
    </td>
    <td>
      Zoom must be in range from 10 till 400.
    </td>
  </tr>
  <tr>
    <td>
       strParentItemName
    </td>
    <td>
      The string name cannot be empty
    </td>
  </tr>
  <tr>
    <td>
      Column value cannot be less than 0 and greater than 255
    </td>
    <td>
      Value cannot be less than 0 and greater than 255
    </td>
  </tr>
  <tr>
    <td>
      End Row Index cannot be greater than max row index
    </td>
    <td>
      Value cannot be greater than max row index
    </td>
  </tr>
  <tr>
    <td>
      firstColumn
    </td>
    <td>
      The column index value is not equal to 0 and greater than book maximum column count
    </td>
  </tr>
  <tr>
    <td>
      firstRow
    </td>
    <td>
      The row index value is not equal to 0 and greater than book maximum rows count
    </td>
  </tr>
  <tr>
    <td>
      Length of the password can't be more than password length
    </td>
    <td>
      The password length value is greater than default maximum password length
    </td>
  </tr>
  <tr>
    <td>
      Row Index value cannot be less than 1 and greater than max row index
    </td>
    <td>
      The row index value is not equal to 0 and greater than book maximum rows count
    </td>
  </tr>
  <tr>
    <td>
      Standard Column Width.
    </td>
    <td>
      The standard column width value is not less than 0 and greater than default maximum column width
    </td>
  </tr>
  <tr>
    <td>
      Value cannot be less 1 and greater than max column index.
    </td>
    <td>
      Value cannot be less 1 and greater than max column index
    </td>
  </tr>
  <tr>
    <td>
      Value cannot be less 1 and greater than max row index.
    </td>
    <td>
      Value cannot be less 1 and greater than max row index
    </td>
  </tr>
  <tr>
    <td>
      Value must be 0 to 3
    </td>
    <td>
      Value must be 0 to 3
    </td>
  </tr>
  <tr>
    <td>
      string.Format("index is {0}, Count is {1}", index, List.Count)
    </td>
    <td>
      Index value is not less than 0 and not greater than equal to list count
    </td>
  </tr>
</table>	

## ExcelWorkbookNotSavedException

 <table>
   <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
   <tr>
     <td>
       Workbook
     </td>
     <td>
       "Object cannot be disposed." + " Save workbook or set property ThrowNotSavedOnDestroy to false.
     </td>
     <td>
       Save workbook or set property ThrowNotSavedOnDestroy to false
     </td>
   </tr>
 </table>
 
## FileNotFoundException
 
<table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td>
      Shape
    </td>
    <td>
      File represents by current path doesn't exist
    </td>
    <td>
      File represents by current path doesn't exist.
    </td>
  </tr>
  <tr>
    <td ROWSPAN="2">
      Workbook
    </td>
    <td>
       "File could not be found. Please verify the file path."
    </td>
    <td>
      "File could not be found.
    </td>
  </tr>
  <tr>
    <td>
      string.Format("File {0} could not be found. Please verify the file path.", filename)
    </td>
    <td>
      The file name is not there in given file path the exception will throw
    </td>
  </tr>
</table>

## InvalidRangeException

<table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td>
      Worksheet
    </td>
    <td>
      Can't copy to destination range
    </td>
    <td>
      The destination array formula not separator the cannot copy to destination range
    </td>
  </tr>
</table>

## NotSupportedException

<table>
  <tr>
    <td>
      {{'**Class**'| markdownify }}
    </td>
    <td>
      {{'**Message**'| markdownify }}
    </td>
    <td>
      {{'**Reason**'| markdownify }}
    </td>
  </tr>
  <tr>
    <td ROWSPAN="11">
      Shape
    </td>
    <td>
      This property can be set only when Gradient Style is selected.
    </td>
    <td>
      This property can be set only when Gradient Style is selected.
    </td>
  </tr>
  <tr>
    <td>
      This property supports only if pattern style is checked
    </td>
    <td>
      This property supports only if pattern style is checked.
    </td>
  </tr>
  <tr>
    <td>
      This property supports only if pattern style is checked
    </td>
    <td>
      This property supports only if texture style is checked.
    </td>
  </tr>
  <tr>
    <td>
      This property support only if defined user texture of picture
    </td>
    <td>
      This property support only if defined user texture of picture.
    </td>
  </tr>
  <tr>
    <td>
       "This property supports only if Checked Solid style."
    </td>
    <td>
      This property supports only if Solid style is checked
    </td>
  </tr>
  <tr>
    <td>
       "This shape doesn't support fill properties."
    </td>
    <td>
      The m_bSupportOption is false the fill format not supported
    </td>
  </tr>
  <tr>
    <td>
       "This shape doesn't support line properties."
    </td>
    <td>
      The m_bSupportOption is false the line format not supported
    </td>
  </tr>
  <tr>
    <td>
      HyperLink
    </td>
    <td>
      The shape is not equal to AutoShape, picture, textbox does not supported in hyperlink
    </td>
  </tr>
  <tr>
    <td>
      This property supported only if checked preset color type
    </td>
    <td>
      Supports only Excel gradient preset.
    </td>
  </tr>
  <tr>
    <td>
      This property supports only if checked one color gradient
    </td>
    <td>
      Supports only Excel gradient preset.
    </td>
  </tr>
  <tr>
    <td>
      This variant doesn't support center shading style.
    </td>
    <td>
      The shape object doesn't support center shading style.
    </td>
  </tr>
  <tr>
    <td ROWSPAN="3">
      Workbook
    </td>
    <td>
       "Name of worksheet must be unique in a workbook."
    </td>
    <td>
      Name of worksheet must be unique in a workbook
    </td>
  </tr>
  <tr>
    <td>
       "Not supported encryption type."
    </td>
    <td>
      This property is not supported for encryption type
    </td>
  </tr>
  <tr>
    <td>
       "Weak encryption algorithm is not supported."
    </td>
    <td>
      Weak encryption algorithm is not supported.
    </td>
  </tr>
  <tr>
    <td>
      Worksheet
    </td>
    <td>
      Name of worksheet must be unique in a workbook
    </td>
    <td>
      Name of worksheet must be unique in a workbook
    </td>
  </tr>
</table>