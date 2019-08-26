---
title: Working with Mail merge | Word library (DocIO) | Syncfusion
description: This section illustrates about Mail merge Word document to create reports (letters, envelopes, labels, invoice, payroll) without MS Word or Office interop.
platform: file-formats
control: DocIO
documentation: UG
---
# Mail merge

Mail merge is a process of merging data from data source to a Word template document. `WMergeField` class provides support to bind template document and data source. `WMergeField` instance is replaced with the actual data retrieved from data source for the given merge field name in a template document.

The following data sources are supported by Essential DocIO for performing Mail merge:

* String Arrays
* ADO.NET objects
* Dynamic objects
* .NET objects

You can create a template document with Merge fields by using the Microsoft Word. The following screenshot shows how to insert a merge filed in the Word document by using the Microsoft Word.

![Word template document](MailMerge_images/MailMerge_img1.png)

You need to add a prefix (“Image:”) to the merge field name for merging an image in the place of a merge field.

For example: The merge field name should be like “Image:Photo” (<<Image:MergeFieldName>>)

## Simple Mail merge

The `MailMerge` class provides various overloads for `Execute` method to perform Mail merge from various data sources. For further information, click [here](https://help.syncfusion.com/file-formats/docio/simple-mail-merge). 

## Mail merge for a group

You can perform Mail merge and append multiple records from data source within a specified region to a template document For further information, click [here](https://help.syncfusion.com/file-formats/docio/group-mail-merge).

## Mail merge for nested group

You can perform nested Mail merge with relational or hierarchical data source and independent data tables in a template document.

For further information, click [here](https://help.syncfusion.com/file-formats/docio/Nested-group-Mail-merge).

## Mail merge with dynamic objects

Essential DocIO allows you to perform Mail merge with the dynamic objects. For further information, click [here](https://help.syncfusion.com/file-formats/docio/nested-group-mail-merge#performing-mail-merge-with-dynamic-objects).

## Mail merge with business objects

You can perform Mail merge with business objects in a template document. For further information, click [here](https://help.syncfusion.com/file-formats/docio/group-mail-merge#performing-mail-merge-with-business-objects).

## Nested Mail merge with relational data objects

Essential DocIO supports performing nested Mail merge with implicit relational data objects without any explicit relational commands by using the `ExecuteNestedGroup` overload method.

For further information, click [here](https://help.syncfusion.com/file-formats/docio/nested-group-mail-merge#performing-nested-mail-merge-with-relational-data-objects).

## Event support for Mail merge

The `MailMerge` class provides event support to customize the document contents and merging image data during the Mail merge process. The following events are supported by Essential DocIO in Mail merge process.

* `MergeField` - occurs during Mail merge when a Mail merge field except image Mail merge field is encountered in the document.

* `MergeImageField` - occurs during Mail merge when an image Mail merge field is encountered in the document.

* `BeforeClearField` - occurs during Mail merge when an unmerged field is encountered in the document.

* `BeforeClearGroupField` - occurs during Mail merge when an unmerged group field is encountered in the document.

### MergeField Event

You can customize the merging text during Mail merge process by using the `MergeField` event. For further information, click [here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#mergefield-event).

### MergeImageField Event

You can customize the merging image during Mail merge process by using the `MergeImageField` event. For further information, click [here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#mergeimagefield-event).

### BeforeClearField Event

You can get the unmerged fields during Mail merge process by using the `BeforeClearField` event during Mail merge process. For further information, click [here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#beforeclearfield-event).

### BeforeClearGroupField Event

You can get the unmerged groups during Mail merge process by using the `BeforeClearGroupField` event during Mail merge process. For further information, click [here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#beforecleargroupfield-event).

## Mail merge options

The `MailMerge` class allows you to customize the Mail merge process with the following options:

### Field Mapping

You can automatically map the merge field names with data source column names during Mail merge process. For further information, click [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#field-mapping).

### Retrieving the merge field names

You can retrieve the merge field names and also merge field group names in the Word document. For further information, click [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#retrieving-the-merge-field-names).

### Removing empty paragraphs

You can remove the empty paragraphs when the paragraph has a merge field item without any data during Mail merge process.

For further information, click [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#removing-empty-paragraphs).

### Removing empty merge fields

You can remove or keep the unmerged merge fields in the output document based on the `ClearFields` property on each mail merge execution.

For further information, click [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#removing-empty-merge-fields).

### Restart numbering in lists

You can restart the list numbering in a Word document during Mail merge. For further information, click [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#restart-numbering-in-lists).