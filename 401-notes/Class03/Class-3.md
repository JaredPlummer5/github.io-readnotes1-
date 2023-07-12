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

