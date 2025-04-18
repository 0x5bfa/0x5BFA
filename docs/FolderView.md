## Definition

```c#
public partial interface IFolderView : Control {}
```

## Usage

```c#

```

## Implementation

```xml
<!--  Default template  -->
<Grid>

    <SemanticZoom>
        <SemanticZoom.ZoomedInView>
            <ListView x:Name="ZoomedInListView" />
        </SemanticZoom.ZoomedInView>
        <SemanticZoom.ZoomedOutView>
            <ListView x:Name="ZoomedOutListView" />
        </SemanticZoom.ZoomedOutView>
    </SemanticZoom>

    <TextBlock Margin="0,120,0,0" Text="{x:Bind EmptyText, Mode=OneWay}" />

    <TeachingTip CloseButtonContent="" PreferredPlacement="Auto" Subtitle="" />

    <Canvas>
        <RectanglarSelectionVisual Target="{x:Bind ZoomedInListView}" />
    </Canvas>

</Grid>
```

```c#
// Properties
[GDP] public /**/ RootFolder { get; set; }
[GDP] public /**/ Items { get; set; }
[GDP] public /**/ SelectedItems { get; set; }
[GDP] public /**/ ThumbnailSize { get; set; }
[GDP] public /**/ Spacing { get; set; }
[GDP] public /**/ GroupById { get; set; }
[GDP] public /**/ SortById { get; set; }
[GDP] public /**/ SortDirection { get; set; }

// Methods
public bool ScrollTo(IStorable storable);
public bool ScrollTo(char c);
public bool ScrollToTop();
public bool ScrollToBottom();
public bool FocusSelectedItems();
public bool SelectItem(IStorable storable);
public bool DeselectedItem(IStorable storable);
public bool StartRenaming();
public bool ReloadThumbnail();

// Events
public event ItemDoubleClicked;
public event ItemClicked;
public event ItemMiddleClicked;
public event ItemRightClicked;
```
