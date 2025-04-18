Represents storage objects that reside in NTFS, FAT32, ExFAT, UDF, ReFS, SMB, and CSVFS.
Almost all of features are provided by Windows API.

## Initialization

```c#
public interface IWindowsStorable {} :  IStorable, IDisposable /* and some base abstraction layer interfaces */ {}
public abstract class WindowsStorable : IWindowsStorable {}
public class WindowsFile :              WindowsStorable, IFile {}
public class WindowsFolder :            WindowsStorable, IFolder {}
```

```c#
// See the next code block for what parameters to be input.
new WindowsFile(/* parameters */);
new WindowsFolder(/* parameters */);
```

If the path you're having isn't obvious whether it's a file or a folder, you can use NativeStorable.Parse() static method instead of respective constructors, which, in fact, also use this method internally. The parsing method only can parse back paths returned from shell item name methods with SHGDN_FORPARSING, and some display paths that the File Explorer's path box can parse.

```c#
// Shell namespace with known folder ID (you can prepend "Shell:" optionally)
WindowsStorable.TryCreate(/* Guid */ PInvoke.FOLDERID_ComputerFolder);
WindowsStorable.TryCreate(@"::{679F85CB-0220-4080-B29B-5540CC05AAB6}");
WindowsStorable.TryCreate(@"::{031E4825-7B94-4DC3-B131-E946B44C8DD5}\Documents.library-ms");

// Known folder names (if the former is input, it would be converted into canocical name first and then parsed)
WindowsStorable.TryCreate(@"This PC");          // Display name of a known folder
WindowsStorable.TryCreate(@"MyComputerFolder"); // Canonical name of a known folder

// LFS (local file system)
WindowsStorable.TryCreate(@"C:\Windows");
WindowsStorable.TryCreate(@"C:\Windows\notepad.exe");

// UNC
WindowsStorable.TryCreate(@"\\?\C:\Window");
WindowsStorable.TryCreate(@"\\?\C:\Windows\notepad.exe");
```

## Usage

### Locatability

**Parsabe string path**

What this returns can be parsed back through WindowsStorable.Parse and so can be used as a handy locatable object.

```c#
var pathStr = WindowsStorableHelper.GetDisplayName(storable, SHGDN.SHGDN_FORPARSING);
```

**IShellItem instance**

This provides a pointer to unmanaged COM onjects, lifecycle of which must not be managed in any other places than IWindowsStorable.Dispose.

```c#
ComPtr<IShellItem> pShellItem = file.GetUnmanagedRef();
```

### Children enumeration

Utilizes IShellFolder::EnumObjects() and IAsyncEnumerable to yield an item for each.

```c#
await (var child in folder.GetChildrenAsync())
{
    // Do something
}
```

### File system operations

Utilizes legacy Win32 API for objects reside in LFS and Windows Shell API only for objects reside in shell namespace.

Here's the implementation example of Copy operation:

```c#
public IAsyncOperationWithProgress<StorageOperationResult,uint> CopyAsync(
    IStorable target,
    IModifiableStorable destination,
    StorageOperationFlags flags,
    CancellationToken token);
```

For more detailed info, visit [the storage operations]()
