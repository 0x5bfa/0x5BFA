## Definition

This user control contains multiple folder views and displays one of them at a time and manages backward/forward navigation stack. Since this is a *browsable* view within Files app, this control also inherits IAppBrowsable interface to provide i.e. display path, thumbnail, etc.

```c#
public sealed partial class FolderBrowser : UserControl, IAppBrowsable, IDisposable {}
```

## Usage

**Display a folder view**

```c#
// Instantiating with various types of folders
var browser = FolderBrowser() { Folder = new HomeFolder() };
browser =     FolderBrowser() { Folder = new WindowsFolder("Shell:ThisPC") }; // parse-able paths only
browser =     FolderBrowser() { Folder = new TagsFolder(tagId) };

// Add a new tab with a new browser instance
App.GetCurrentWindow().AddNewTab(browser, focus: true);

// Add a new pane with a new browser instance
App.GetCurrentWindow().GetCurrentTab().AddNewPane(browser, focus: true);
```

**Navigate back/forward/up**

```c#
public record struct FolderBrowserNavigationStack(BitmapImage thumbnail, string displayPath, string parsablePath);

// In FolderBrowser class
public readonly ObservableCollection<FolderBrowserNavigationStack> BackwardNavigationStack { get; }
public readonly ObservableCollection<FolderBrowserNavigationStack> ForwardNavigationStack { get; }
public FolderBrowserNavigationStack CurrentNavigation { get; }
```

```c#
var browser = App.GetCurrentWindow().GetCurrentTab().GetCurrentPane() as FolderBrowser;

if (browser.CanNavigateBack())
    browser.NavigateBack();

if (browser.CanNavigateUp())
    browser.NavigateUp();
```

## Working with views

```c#
public FolderBrowser()
{
    // Subscribe events from various views
    DetailsFolderView.Loading += DetailsFolderView_Loading;
    DetailsFolderView.ColumnAdded += DetailsFolderView_ColumnAdded;
    TreeFolderView.Loading += TreeFolderView_Loading;
}

public void DetailsFolderView_Loading(object? sender, DetailsViewLoadingEventArgs e)
{
    if (e.RootFolder is null)
        rerun;

    // Set row data to each storable
    foreach (var child in e.Children)
    {
        var rowData = ...();
        e.Database[child] = rowData;
    }
}

public void DetailsFolderView_ColumnAdded(object? sender, DetailsViewColumnAddedEventArgs e)
{
    if (e.RootFolder is null || e.ColumnAdded is not IDetailsFolderViewColumn newColumn)
        return;

    FolderSettingsHelper.AddNewColumnAt(e.RootFolder, newColumn.Id, newColumn.Index, newColumn.Width);
}

public void TreeFolderView_Loading(object? sender, TreeViewFolderLoadingEventArgs e)
{
    if (e.RootFolder is null)
        rerun;

    // Set bool value if folder should be expanded or not to each folder
    foreach (var folder in e.Folders)
    {
        var expanded = ...();
        e.Database[folder] = expanded;
    }

    e.Handled = true;
}
```
