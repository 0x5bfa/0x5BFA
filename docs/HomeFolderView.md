## Definition

This is specifically designed and implemented for Files App Home page and corresponds with HomeFolder class.

```c#
public partial class HomeFolderView : IFolderView {}
```

This view supports different inner view per group.

Group name|Default view mode
---|---
Quick access|CardFolderView
Drives|CardFolderView
Network drives|CardFolderView
Recent files|DetailsFolderView

## Usage

```c#
// General usage
var view = new HomeFolderView();

// Default FolderBrowser contains HomeFolderView
var browser = new FolderBrowser() { Folder = new HomeFolder(); };
```

## Implementation

```c#

```
