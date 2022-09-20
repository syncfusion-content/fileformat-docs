---
title: Zip all files in subfolders using Syncfusion's Compression |Syncfusion
description: This page illustrates with an example to zip all the files in subfolders using the Syncfusion.Compression.Zip namespace.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to zip all the files in subfolders using Syncfusion's Compression?

You can compress and decompress the files with our Compression library. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

using Syncfusion.Compression.Zip;

class Program
    {
        private static List<DirectoryInfo> arrOfItems = new List<DirectoryInfo>();
        private static ZipArchive zipArchive = new ZipArchive();
        private static string folderPath = "ZipFiles";

        private static void SubFoldersFiles(string path)

        {

            DirectoryInfo dInfo = new DirectoryInfo(path);

            foreach (DirectoryInfo d in dInfo.GetDirectories())

            {

                SubFoldersFiles(d.FullName);

                arrOfItems.Add(d);

            }

        }

        // Zip and save the file.

        private static void ZipAndSave()

        {

            SubFoldersFiles(folderPath);

            if (Directory.Exists(folderPath))

            {

                AddRootFiles();

                AddSubFoldersFiles();

                // Saving zipped file.

                zipArchive.Save("UnzippedFile.zip");

                zipArchive.Close();

                Console.WriteLine("Files Zipped successfully!");

            }

        }

        private static void AddRootFiles()

        {

            string fileName = "";

            foreach (string rootFiles in Directory.GetFiles(folderPath))

            {

                //Creating the stream from file

                FileStream stream = new FileStream(rootFiles, FileMode.Open, FileAccess.ReadWrite);

                //Getting the File Name alone and ignoring the directory path

                fileName = Path.GetFileName(rootFiles);

                FileAttributes attribute = File.GetAttributes(rootFiles);

                zipArchive.AddItem(fileName, stream, false, attribute);

            }

        }

        private static void AddSubFoldersFiles()

        {

            foreach (DirectoryInfo dInfo in arrOfItems)

            {

                FileInfo[] fInfo = dInfo.GetFiles();

                string mainDirectoryPath = Path.GetFullPath(folderPath);

                foreach (FileInfo file in fInfo)

                {

                    //Get the File name with its current folder and ignoring the Main Directory

                    string fileName = file.FullName.Replace(mainDirectoryPath, "");

                    //Read the file stream by its Full name

                    FileStream stream = new FileStream(file.FullName, FileMode.Open, FileAccess.ReadWrite);

                    FileAttributes attributes = File.GetAttributes(file.FullName);

                    //Add the item to the zip Archive

                    zipArchive.AddItem(fileName, stream, true, attributes);

                }

            }

        }

        //Unzipping the Folder

        private static void UnZipFiles()

        {

            ZipArchive zip = new ZipArchive();

            string path = "UnZippedFile";

            zip.Open("UnzippedFile.zip");

            if (!Directory.Exists(path))

                Directory.CreateDirectory(path);

            //Saving the contents of zip file to disk.

            for (int i = 0; i < zip.Count; i++)

            {

                ZipArchiveItem item = zip[i];

                string itemName = path + item.ItemName;

                //checking whether the item is root file

                if (itemName.Contains("/"))

                {

                    itemName = itemName.Replace("/", "\\");

                }

                //Check whether the Directory is present or not

                if (!Directory.Exists(itemName) || itemName.Contains("\\"))

                {

                    int index = itemName.LastIndexOf("\\");

                    string directoryPath = itemName.Remove(index, itemName.Length - index);

                    Directory.CreateDirectory(directoryPath);

                }

                FileStream fileStream = new FileStream(itemName, FileMode.OpenOrCreate, FileAccess.ReadWrite);

                MemoryStream memoryStream = item.DataStream as MemoryStream;

                memoryStream.WriteTo(fileStream);

                fileStream.Flush();

                fileStream.Close();

            }

            Console.WriteLine("File has been Unzipped");

        }


        static void Main(string[] args)
        {
            ZipAndSave();
            UnZipFiles();
        }
    }



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Imports Syncfusion.Compression.Zip

Class Program
	Private Shared arrOfItems As New List(Of DirectoryInfo)()
	Private Shared zipArchive As New ZipArchive()
	Private Shared folderPath As String = "ZipFiles"

	Private Shared Sub SubFoldersFiles(path As String)


		Dim dInfo As New DirectoryInfo(path)

		For Each d As DirectoryInfo In dInfo.GetDirectories()


			SubFoldersFiles(d.FullName)


			arrOfItems.Add(d)
		Next

	End Sub

	' Zip and save the file.

	Private Shared Sub ZipAndSave()


		SubFoldersFiles(folderPath)

		If Directory.Exists(folderPath) Then


			AddRootFiles()

			AddSubFoldersFiles()

			' Saving zipped file.

			zipArchive.Save("UnzippedFile.zip")

			zipArchive.Close()


			Console.WriteLine("Files Zipped successfully!")
		End If

	End Sub

	Private Shared Sub AddRootFiles()


		Dim fileName As String = ""

		For Each rootFiles As String In Directory.GetFiles(folderPath)


			'Creating the stream from file

			Dim stream As New FileStream(rootFiles, FileMode.Open, FileAccess.ReadWrite)

			'Getting the File Name alone and ignoring the directory path

			fileName = Path.GetFileName(rootFiles)

			Dim attribute As FileAttributes = File.GetAttributes(rootFiles)


			zipArchive.AddItem(fileName, stream, False, attribute)
		Next

	End Sub

	Private Shared Sub AddSubFoldersFiles()


		For Each dInfo As DirectoryInfo In arrOfItems


			Dim fInfo As FileInfo() = dInfo.GetFiles()

			Dim mainDirectoryPath As String = Path.GetFullPath(folderPath)

			For Each file__1 As FileInfo In fInfo


				'Get the File name with its current folder and ignoring the Main Directory

				Dim fileName As String = file__1.FullName.Replace(mainDirectoryPath, "")

				'Read the file stream by its Full name

				Dim stream As New FileStream(file__1.FullName, FileMode.Open, FileAccess.ReadWrite)

				Dim attributes As FileAttributes = File.GetAttributes(file__1.FullName)

				'Add the item to the zip Archive


				zipArchive.AddItem(fileName, stream, True, attributes)

			Next
		Next

	End Sub

	'Unzipping the Folder

	Private Shared Sub UnZipFiles()


		Dim zip As New ZipArchive()

		Dim path As String = "UnZippedFile"

		zip.Open("UnzippedFile.zip")

		If Not Directory.Exists(path) Then

			Directory.CreateDirectory(path)
		End If

		'Saving the contents of zip file to disk.

		For i As Integer = 0 To zip.Count - 1


			Dim item As ZipArchiveItem = zip(i)

			Dim itemName As String = path + item.ItemName

			'checking whether the item is root file

			If itemName.Contains("/") Then



				itemName = itemName.Replace("/", "\")
			End If

			'Check whether the Directory is present or not

			If Not Directory.Exists(itemName) OrElse itemName.Contains("\") Then


				Dim index As Integer = itemName.LastIndexOf("\")

				Dim directoryPath As String = itemName.Remove(index, itemName.Length - index)


				Directory.CreateDirectory(directoryPath)
			End If

			Dim fileStream As New FileStream(itemName, FileMode.OpenOrCreate, FileAccess.ReadWrite)

			Dim memoryStream As MemoryStream = TryCast(item.DataStream, MemoryStream)

			memoryStream.WriteTo(fileStream)

			fileStream.Flush()


			fileStream.Close()
		Next

		Console.WriteLine("File has been Unzipped")

	End Sub


	Private Shared Sub Main(args As String())
		ZipAndSave()
		UnZipFiles()
	End Sub
End Class



{% endhighlight %}

  {% endtabs %}  

## See Also

* [How to zip files using the Syncfusion.Compression.Zip namespace?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-zip-files-using-the-syncfusion-compression-zip-namespace)
* [How to protect the zip files using Syncfusion.Compression.Base?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-protect-the-zip-files-using-syncfusion-compression-base)
* [How to un-protect the zip files using Syncfusion.Compression.Base?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-un-protect-the-zip-files-using-syncfusion-compression-base)
* [How to merge excel files from more than one workbook to a single file?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-merge-excel-files-from-more-than-one-workbook-to-a-single-file)
