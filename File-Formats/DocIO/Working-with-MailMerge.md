---
title: Working with MailMerge | Syncfusion
description: This section illustrates how to merge the data from data source to a Word document
platform: file-formats
control: DocIO
documentation: UG
---
# Mail merge

Mail merge is a process of merging data from data source to a Word template document. `WMergeField` class provides support to bind template document and data source. `WMergeField` instance is replaced with the actual data retrieved from data source for the given merge field name in a template document.

The following data sources are supported by Essential DocIO for performing Mail merge.

* String Arrays
* ADO.NET objects
* Dynamic objects
* Business objects

You can create a template document with Merge fields by using the Microsoft Word. The following screenshot shows how to insert a merge filed in the Word document by using the Microsoft Word.

![Word template document](MailMerge_images/MailMerge_img1.png)


You need to add a prefix (“Image:”) to the merge field name for merging an image in the place of a merge field.

For example: The merge field name should be like “Image:Photo” (<<Image:MergeFieldName>>)

## Simple Mail merge

The `MailMerge` class provides various overloads for `Execute` method to perform Mail merge from various data sources. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/simple-mail-merge#). 

## Performing Mail merge for a group

You can perform Mail merge and append multiple records from data source within a specified region to a template document For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/group-mail-merge#).

## Performing Nested Mail merge for group

You can perform nested Mail merge with relational or hierarchical data source and independent data tables in a template document.

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/Nested-group-Mail-merge#).

## Performing Mail merge with dynamic objects

Essential DocIO allows you to perform Mail merge with the dynamic objects. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/nested-group-mail-merge#performing-mail-merge-with-dynamic-objects).

## Performing Mail merge with business objects

You can perform Mail merge with business objects in a template document. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/group-mail-merge#performing-mail-merge-with-business-objects).

## Performing Nested Mail merge with relational data objects

Essential DocIO supports to perform nested Mail merge with implicit relational data objects without any explicit relational commands by using the `ExecuteNestedGroup` overload method.

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/nested-group-mail-merge#performing-nested-mail-merge-with-relational-data-objects).

## Event support for Mail merge

The `MailMerge` class provides event support to customize the document contents and merging image data during the Mail merge process. The following events are supported by Essential DocIO in Mail merge process.

* `MergeField` - occurs during Mail merge when a Mail merge field except image Mail merge field is encountered in the document

* `MergeImageField` - occurs during Mail merge when a image Mail merge field is encountered in the document

* `BeforeClearField` - occurs during Mail merge when a unmerged field is encountered in the document

* `BeforeClearGroupField` - occurs during Mail merge when a unmerged group field is encountered in the document

### MergeField Event

You can customize the document contents while executing Mail merge for merge field except image Mail merge field using `MergeField` event. For further information kindly refer[here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#mergefield-event).

### MergeImageField Event

You can customize the Mail merge images in Word document during mail merge process using `MergeImageField` event. For further information kindly refer[here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#mergeimagefield-event).

### BeforeClearField Event

Essential DocIO allows you to identify unmerged field in the Word document using `BeforeClearField` event during Mail merge process. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#beforeclearfield-event).

### BeforeClearGroupField Event

You can identify the unmerged group field in the Word document using `BeforeClearGroupField` event during Mail merge process. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/event-support-for-mail-merge#beforecleargroupfield-event).

## Mail merge options

The `MailMerge` class allows you to customize the Mail merge process with the following options.

### Field Mapping

The `MailMerge` class can automatically maps the merge field names with data source column names during Mail merge process. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#field-mapping).

### Retrieving the merge field names

You can retrieve the merge field names and also group merge fields in the Word document. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#retrieving-the-merge-field-names).

### Removing empty paragraphs

The `MailMerge` class allows to remove the empty paragraphs when the paragraph has a merge field item without any data during Mail merge process.

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#removing-empty-paragraphs).

### Removing empty merge fields

Essential DocIO removes or keeps the unmerged merge fields in the output document based on the ClearFields property on each mail merge execution.

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#removing-empty-merge-fields).

### Restart numbering in lists

You can  restart the list numbering in a Word documents while performing mail merge and merging multiple Word documents. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/mail-merge-options#restart-numbering-in-lists).