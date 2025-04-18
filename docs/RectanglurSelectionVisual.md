## Definition

This represents a dynamic rectangle that is resized and supports multiple ItemsControl instances to dynamically select items as mouse cursor moves.

```c#
public partial class RectabglurSelectionVisual : Canvas {}
```

## Usage

```c#
private IEnumerable<ItemsControl> _Targets;
public IEnumerable<ItemsControl> Targets { get; set; }

public HomeFolderView()
{
    Targets =
    [
        QuickAccessFolderView.ItemsControl,
        DrivesFolderView.ItemsControl,
        FileTagsFolderView.ItemsControl,
        RecentFilesFolderView.ItemsControl,
    ];
}
```
```xml
<RectabglurSelectionVisual
    Targets="{x:Bind ItemsControls, Mode=OneWay}" />
```

## Implementation


```c#
[GDP] public /**/ IEnumerable<ItemsControl> Targets { get; set; }
[GDP] public /**/ Brush RectanglurBorderBrush { get; set; }
[GDP] public /**/ Brush RectanglurBackgroundBrush { get; set; }
[GDP] public /**/ BackgroundOpacity { get; set; }
```
