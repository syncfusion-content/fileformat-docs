---
title: Working with Tables | Syncfusion
description: Learn how to create or add a table to a PDF document, apply cell style & built-in table styles, automatic pagination, customize the rows and columns, and more.
platform: file-formats
control: PDF
documentation: UG
---

# Working with .NET PDF Tables 

The Syncfusion .NET PDF library provides support for two types of [PDF table](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/pdf-tables) models, both having a different levels of customization, which is explained as follows. The two types of table models are:

1. [PdfGrid* (Recommended)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html)
2. [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html)

N> We strongly recommend to use ``PdfGrid`` for creating table in PDF document since it represents flexible grid which supports various customization of rows and columns. 

## Difference between PdfLightTable and PdfGrid

Both the [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) and [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) models are supported across all the platforms and the following table explains the level of customizations both the models provide.

<table>
    <thead>
        <tr>
            <th>
                Features
            </th>
            <th>
                PdfLightTable
            </th>
            <th>
                PdfGrid
            </th>
    </thead>
    <tbody>
        <tr>
            <td align="center" colspan="3">
                {{ '**Formatting**' | markdownify }}
            </td>
        </tr>
        <tr>
            <td>
                Row
            </td>
            <td>
                No direct API, possible through events.
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Column
            </td>
            <td>
                Yes (StringFormat)
            </td>
            <td>
                Yes (StringFormat)
            </td>
        </tr>
        <tr>
            <td>
                Cell
            </td>
            <td>
                No direct API for single cell formatting, possible through events.
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td align="center" colspan="3">
                {{ '**Others**' | markdownify }}
            </td>
        </tr>
        <tr>
            <td>
                Row span
            </td>
            <td>
                No
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Column span
            </td>
            <td>
                No direct API, possible through events.
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Nested Grid
            </td>
            <td>
                Possible through events
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Layout Events
            </td>
            <td>
                BeginCellLayout, BeginPageLayout, BeginRowLayout, EndCellLayout, EndPageLayout, EndRowLayout
            </td>
            <td>
                BeginPageLayout, EndPageLayout
            </td>
        </tr>
    </tbody>
</table>
