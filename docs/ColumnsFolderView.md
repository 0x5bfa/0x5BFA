## Implementation

```xml
<UserControl ...>

    <Grid x:Name="ColumnsGrid" />

</UserControl>
```

```c#
public IReadonlyCollection<IColumnFolderView> Columns { get; }
public event NewColumnAdded;

public ColumnsFolderView()
{
    InitializeComponents();

    // Add the first column
    AddColumn(CurrentRootFolder);
}

private void AddColumn(IFolder folder)
{
    if (ColumnsGrid.Children.Count != 0)
    {
        // Add a sizer
    }

    // Add a column
}

private void ColumnFolderView_SelectionChanged(object? sender, SelectionChangedEventArgs e)
{
    if (...)
        return;

    AddColumn(...);
}
```

## Manipulation in FolderBrowser

```c#
private void ColumnsFolderView_ColumnAdded(object? sender, ColumnsFolderViewColumnAddedEventArgs e)
{
    if (e.Column is {} column)
    {
        // Adjust width based on the user settings
    }
}
```
