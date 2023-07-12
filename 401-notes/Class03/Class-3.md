# System.IO


## File and Directory Interactions

- Use the `File` class for static methods related to file operations, such as creating, copying, deleting, moving, and opening files.
- Use the `FileInfo` class for instance methods related to file operations.
- Use the `Directory` class for static methods related to directory operations, such as creating, moving, and enumerating through directories and subdirectories.
- Use the `DirectoryInfo` class for instance methods related to directory operations.
- The `Path` class provides methods and properties for working with directory strings in a cross-platform manner.

## Streams

- Use the `FileStream` class for reading from and writing to a file.
- The `MemoryStream` class allows reading from and writing to memory as a backing store.
- The `BufferedStream` class improves the performance of read and write operations.
- The `NetworkStream` class enables reading from and writing to network sockets.
- The `PipeStream` class is used for reading from and writing to anonymous and named pipes.
- The `CryptoStream` class allows linking data streams to cryptographic transformations.

## Readers and Writers

- The `BinaryReader` and `BinaryWriter` classes are used for reading and writing primitive data types as binary values.
- Use the `StreamReader` and `StreamWriter` classes for reading and writing characters by using an encoding value to convert between characters and bytes.
- The `StringReader` and `StringWriter` classes are useful for reading and writing characters to and from strings.
- The abstract classes `TextReader` and `TextWriter` serve as base classes for other readers and writers that work with characters and strings.

## Asynchronous I/O Operations

- Use the asynchronous members that contain "Async" in their names, such as `ReadAsync` and `WriteAsync`, for performing asynchronous I/O operations.
- Asynchronous I/O operations help in keeping the application responsive while performing resource-intensive tasks.
- Use the `async` and `await` keywords to work with asynchronous methods.

## Compression

- The `System.IO.Compression` namespace contains types for compressing and decompressing files and streams.
- Use the `ZipArchive`, `ZipArchiveEntry`, and `ZipFile` classes for working with zip archives.
- The `DeflateStream` class is used for compressing and decompressing streams using the Deflate algorithm.
- The `GZipStream` class is used for compressing and decompressing streams in gzip data format.

## Isolated Storage

- Isolated storage provides a mechanism for storing data in a controlled and isolated manner.
- Use the `IsolatedStorage` class as the base class for isolated storage implementations.
- The `IsolatedStorageFile` class provides an isolated storage area that contains files and directories.
- The `IsolatedStorageFileStream` class exposes a file within isolated storage.

## I/O Operations in Windows Store Apps

- For Windows 8.x Store apps, use the types in the `Windows.Storage` namespace for file and storage operations.
- Types like `File`, `FileInfo`, `Directory`, and `DirectoryInfo` from `System.IO` are not available in Windows 8.x Store apps.
- Asynchronous methods should be used to prevent blocking the UI thread in Windows 8.x Store apps.

## I/O and Security

- When using the `System.IO` namespace, follow the operating system security requirements, such as access control lists (ACLs), to control access to files and directories.
- Default security policies prevent Internet or intranet applications from accessing files on the user's computer.
- Handle security appropriately when working with streams and avoid passing streams to less-trusted code or application domains.

## "How to" Guide

These code snippets demonstrate how to perform various file and directory operations, work with streams, readers, writers, perform asynchronous I/O operations, and perform file compression and decompression using the classes provided in the `System.IO` and `System.IO.Compression` namespaces.

### File and Directory Interactions

#### Creating a file:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
File.Create(filePath);
```

#### Copying a file:

```csharp
using System.IO;

string sourceFilePath = "path/to/source.txt";
string destinationFilePath = "path/to/destination.txt";
File.Copy(sourceFilePath, destinationFilePath);
```

#### Deleting a file:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
File.Delete(filePath);
```

#### Moving a file:

```csharp
using System.IO;

string sourceFilePath = "path/to/source.txt";
string destinationFilePath = "path/to/destination.txt";
File.Move(sourceFilePath, destinationFilePath);
```

#### Creating a directory:

```csharp
using System.IO;

string directoryPath = "path/to/directory";
Directory.CreateDirectory(directoryPath);
```

#### Moving a directory:

```csharp
using System.IO;

string sourceDirectoryPath = "path/to/source";
string destinationDirectoryPath = "path/to/destination";
Directory.Move(sourceDirectoryPath, destinationDirectoryPath);
```

#### Enumerating files in a directory:

```csharp
using System.IO;

string directoryPath = "path/to/directory";
string[] files = Directory.GetFiles(directoryPath);
foreach (string file in files)
{
    Console.WriteLine(file);
}
```

#### Enumerating directories in a directory:

```csharp
using System.IO;

string directoryPath = "path/to/directory";
string[] directories = Directory.GetDirectories(directoryPath);
foreach (string directory in directories)
{
    Console.WriteLine(directory);
}
```

### Streams

#### Reading from a file stream:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
using (FileStream fileStream = new FileStream(filePath, FileMode.Open))
{
    byte[] buffer = new byte[1024];
    int bytesRead = fileStream.Read(buffer, 0, buffer.Length);
    // Process the read data
}
```

#### Writing to a file stream:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
using (FileStream fileStream = new FileStream(filePath, FileMode.Append))
{
    byte[] data = Encoding.UTF8.GetBytes("Hello, world!");
    fileStream.Write(data, 0, data.Length);
}
```

#### Reading from a memory stream:

```csharp
using System.IO;

byte[] buffer = Encoding.UTF8.GetBytes("Hello, world!");
using (MemoryStream memoryStream = new MemoryStream(buffer))
{
    byte[] readBuffer = new byte[1024];
    int bytesRead = memoryStream.Read(readBuffer, 0, readBuffer.Length);
    // Process the read data
}
```

#### Writing to a memory stream:

```csharp
using System.IO;

using (MemoryStream memoryStream = new MemoryStream())
{
    byte[] data = Encoding.UTF8.GetBytes("Hello, world!");
    memoryStream.Write(data, 0, data.Length);

    // Reset the position to the beginning of the stream
    memoryStream.Position = 0;

    // Read the data from the memory stream
    byte[] readBuffer = new byte[1024];
    int bytesRead = memoryStream.Read(readBuffer, 0, readBuffer.Length);
    // Process the read data
}
```

### Readers and Writers

#### Reading from a file using `StreamReader`:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
using (StreamReader reader = new StreamReader(filePath))
{
    string line;
    while ((line = reader.ReadLine()) != null)
    {
        Console.WriteLine(line);
    }
}
```

#### Writing to a file using `StreamWriter`:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
using (StreamWriter writer = new StreamWriter(filePath))
{
    writer.WriteLine("Hello, world!");
}
```

#### Reading from a string using `StringReader`:

```csharp
using System.IO;

string input = "Hello, world!";
using (StringReader reader = new StringReader(input))
{
    string line = reader.ReadLine();
    Console.WriteLine(line);
}
```

#### Writing to a string using `StringWriter`:

```csharp
using System.IO;

using (StringWriter writer = new StringWriter())
{
    writer.WriteLine("Hello, world!");

    // Get the written content as a string
    string output = writer.ToString();
    Console.WriteLine(output);
}
```

### Asynchronous I/O Operations

#### Reading from a file asynchronously:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
using (FileStream fileStream = new FileStream(filePath, FileMode.Open))
{
    byte[] buffer = new byte[1024];
    int bytesRead = await fileStream.ReadAsync(buffer, 0, buffer.Length);
    // Process the read data
}
```

#### Writing to a file asynchronously:

```csharp
using System.IO;

string filePath = "path/to/file.txt";
using (FileStream fileStream = new FileStream(filePath, FileMode.Append))
{
    byte[] data = Encoding.UTF8.GetBytes("Hello, world!");
    await fileStream.WriteAsync(data, 0, data.Length);
}
```

### Compression

#### Compressing a file using `GZipStream`:

```csharp
using System.IO.Compression;

string sourceFilePath = "path/to/source.txt";
string compressedFilePath = "path/to/compressed.gz";
using (FileStream sourceFileStream = File.OpenRead(sourceFilePath))
using (FileStream compressedFileStream = File.Create(compressedFilePath))
using (GZipStream compressionStream = new GZipStream(compressedFileStream, CompressionMode.Compress))
{
    sourceFileStream.CopyTo(compressionStream);
}
```

#### Decompressing a file using `GZipStream`:

```csharp
using System.IO.Compression;

string compressedFilePath = "path/to/compressed.gz";
string decompressedFilePath = "path/to/decompressed.txt";
using (FileStream compressedFileStream = File.OpenRead(compressedFilePath))
using (FileStream decompressedFileStream = File.Create(decompressedFilePath))
using (GZipStream decompressionStream = new GZipStream(compressedFileStream, CompressionMode.Decompress))
{
    decompressionStream.CopyTo(decompressedFileStream);
}
```

## How to write text to a file?

These examples demonstrate different approaches to write text to a file synchronously and asynchronously using `StreamWriter` and `File` class methods. They provide flexibility in terms of creating new files, appending to existing files, and using different techniques to write text to a file in a .NET application.

#### Synchronously write text with StreamWriter:


In this example, we use the `StreamWriter` class to write text to a new file synchronously. First, we define an array of strings called `lines` containing the lines of text we want to write to the file. Then, we specify the path where we want to create the file using the `Environment.GetFolderPath` method to get the Documents path. Inside the `using` statement, we instantiate a `StreamWriter` and pass the file path to its constructor. The `StreamWriter` object automatically flushes and closes the stream when the `using` block is exited. Finally, we iterate over each line in the `lines` array and use the `WriteLine` method of the `StreamWriter` to write each line to the file.



```csharp
using System;
using System.IO;

string[] lines = { "First line", "Second line", "Third line" };
string docPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

using (StreamWriter outputFile = new StreamWriter(Path.Combine(docPath, "WriteLines.txt")))
{
    foreach (string line in lines)
        outputFile.WriteLine(line);
}
```

#### Synchronously append text with StreamWriter:

In this example, we continue from the previous example and demonstrate how to use `StreamWriter` to append text to an existing file. We use the same `StreamWriter` approach as before, but this time we pass `true` as the second argument to the `StreamWriter` constructor. This enables appending mode, which means that if the file already exists, the new content will be appended to the end of the file instead of overwriting it.

```csharp
using System;
using System.IO;

string docPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

using (StreamWriter outputFile = new StreamWriter(Path.Combine(docPath, "WriteLines.txt"), true))
{
    outputFile.WriteLine("Fourth Line");
}
```

#### Asynchronously write text with StreamWriter:

In this example, we demonstrate how to use `StreamWriter` to write text to a new file asynchronously. To use asynchronous methods, the containing method (in this case, `Main`) must be declared with the `async` keyword. We specify the file path using the `Environment.GetFolderPath` method, and then instantiate a `StreamWriter` object as before. However, this time we use the `WriteAsync` method instead of `Write` to write the text asynchronously. The `await` keyword is used to await the completion of the asynchronous write operation.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;

string docPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

async Task Main()
{
    using (StreamWriter outputFile = new StreamWriter(Path.Combine(docPath, "WriteTextAsync.txt")))
    {
        await outputFile.WriteAsync("This is a sentence.");
    }
}
```

#### Write and append text with the File class:

In this example, we show an alternative approach using the `File` class to write and append text to a file. First, we define a string variable called `text` containing the initial line of text. We use the `Environment.GetFolderPath` method to specify the file path, and then use the `WriteAllText` method of the `File` class to write the `text` to a new file. This method automatically creates the file if it doesn't exist and overwrites it if it does. Next, we define an array of strings called `lines` with additional lines of text. We use the `AppendAllLines` method of the `File` class to append each line in the `lines` array to the existing file. This method automatically appends the lines without overwriting the existing content.


```csharp
using System;
using System.IO;

string text = "First line" + Environment.NewLine;
string docPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

File.WriteAllText(Path.Combine(docPath, "WriteFile.txt"), text);

string[] lines = { "New line 1", "New line 2" };
File.AppendAllLines(Path.Combine(docPath, "WriteFile.txt"), lines);
```

These code snippets demonstrate how to write text to a file synchronously and asynchronously using `StreamWriter` or `File` class methods. The examples show how to write text to a new file, append text to an existing file, and use different techniques for writing text to a file in a .NET app.

## How to: Read and write to a newly created data file

The following example demonstrates how to create a new data file, write data to it using `BinaryWriter`, and read the data from it using `BinaryReader`.

1. First, check if the file already exists using `File.Exists` method. If it exists, display a message and exit.
2. Create a new file stream using `FileStream` with `FileMode.CreateNew` to create a new file. If you want to overwrite the file if it already exists, use `FileMode.Create` instead.
3. Create a `BinaryWriter` object and wrap it in a `using` statement to ensure proper disposal after use.
4. Use a loop to write the desired data to the file using the `Write` method of `BinaryWriter`.
5. Close the `BinaryWriter` and `FileStream`.
6. Open the file again using `FileStream` with `FileMode.Open` and `FileAccess.Read`.
7. Create a `BinaryReader` object and wrap it in a `using` statement.
8. Use a loop to read the data from the file using the `ReadInt32` method of `BinaryReader`.
9. Process the read data as desired.

```csharp
using System;
using System.IO;

class MyStream
{
    private const string FILE_NAME = "Test.data";

    public static void Main()
    {
        if (File.Exists(FILE_NAME))
        {
            Console.WriteLine($"{FILE_NAME} already exists!");
            return;
        }

        using (FileStream fs = new FileStream(FILE_NAME, FileMode.CreateNew))
        {
            using (BinaryWriter w = new BinaryWriter(fs))
            {
                for (int i = 0; i < 11; i++)
                {
                    w.Write(i);
                }
            }
        }

        using (FileStream fs = new FileStream(FILE_NAME, FileMode.Open, FileAccess.Read))
        {
            using (BinaryReader r = new BinaryReader(fs))
            {
                for (int i = 0; i < 11; i++)
                {
                    Console.WriteLine(r.ReadInt32());
                }
            }
        }
    }
}
```