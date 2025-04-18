## Definition

This storable is specifically implemented for Files App in order to show combined/summarized storage data on Home page in Files App.

```c#
public partial class HomeFolder : IStorable {}
```

## Usage

```c#
var folder = new HomeFolder();
var pinnedFolders = folder.GetPinnedFolders();
```

## Implementation

```c#
public IAsyncEnumerable<IStorable> GetPinnedFolders();
public IAsyncEnumerable<IStorable> GetPinnedFiles();

public IAsyncEnumerable<IStorable> GetRecentFoldersAsync();
public IAsyncEnumerable<IStorable> GetRecentFilesAsync();

public IAsyncEnumerable<IStorable> GetDrivesAsync();
public IAsyncEnumerable<IStorable> GetCloudDrivesAsync();
public IAsyncEnumerable<IStorable> GetNetworkDrivesAsync();

public IAsyncEnumerable<IStorable> GetFileTagsAsync();
```