# Migrate WCT from 7.x to 8.x

Bla bla bla.

## Compatibility

❌: Discontinued
✅: Already ported
🧪: Experimenting
⚡️: Newly introduced
♻️: Internal implementation has been changed
⚠️: Not yet ported

### Animations

Name|Status|Remarks
---|:-:|---
AnimationBuilder|✅|
AnimationSet|✅|
ImplicitAnimationSet|✅|
Lottie API|✅|Ported to [the new Lottie package](https://www.nuget.org/packages/CommunityToolkit.WinUI.Lottie) in 8.0.
...||

### Controls

Name|Status|Remarks
---|:-:|---
AdaptiveGridView|❌|Superseded by [UniformGridLayout](https://learn.microsoft.com/en-us/windows/apps/design/controls/items-repeater#uniformgridlayout) for [ItemsRepeater](https://learn.microsoft.com/en-us/windows/apps/design/controls/items-repeater) in WinUI.
BladeView|⚠️|For more info, visit [the tracking ticket](https://github.com/CommunityToolkit/Windows/issues/89).
CameraPreview|✅|Ported to [CameraPreview](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/camerapreview/) in 8.0.
Carousel|⚠️|
ColorPicker|✅|Ported to [ColorPicker](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/colorpicker/) in 8.1.
ConstrainedBox|✅|Ported to [ConstrainedBox](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/constrainedbox) in 8.0.
ContentSizer|⚡️|Newly introduced to 8.0.
DataGrid|❌|Since the loc of this control reached approximately 30k, we're working on a lightweight control, DataTable, in WCT Labs.
DockPanel|✅|Ported to [DockPanel](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/dockpanel) in 8.0.
DropShadowPanel|❌|Superseded by AttachedCardShadow or AttachedDropShadow.
Expander|❌|Superseded by [Expander](https://learn.microsoft.com/en-us/windows/apps/design/controls/expander) in WinUI.
Eyedropper|⚠️|
GridSplitter|♻️|Ported to [GridSplitter](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/sizers/gridsplitter) in 8.0.
HamburgerMenu|❌|Superseded by [NavigationView](https://learn.microsoft.com/en-us/windows/apps/design/controls/navigationview) in WinUI.
HeaderedContentControl|✅|Ported to [HeaderedContentControl](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/headeredcontrols/headeredcontentcontrol) in 8.0.
HeaderedItemsControl|✅|Ported to [HeaderedItemsControl](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/headeredcontrols/headereditemscontrol) in 8.0.
HeaderedTextBlock|❌|Superseded by HeaderedContentControl.
HeaderedTreeView|⚡️|Newly introduced to 8.0.
ImageCropper|✅|Ported to [ImageCropper](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/imagecropper/) in 8.0.
ImageEx|⚠️|
InAppNotification|❌|Superseded by the StackedNotificationsBehavior in our Behaviors package to build on top of the platform InfoBar control.
InfiniteCanvas|⚠️|
LayoutTransformControl|✅|Ported to [LayoutTransformControl](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/layouttransformcontrol/) in 8.0.
Loading|⚠️|
MarkdownTextBlock|♻️|Since the parser of markdown was our own implementation and it was hard for us to maintain, we decided to discontinue the support of this control from 7.x. One of the community members has implemented a new MarkdownTextBlock that utilizes Markdig parser in Labs.
Menu|❌|Superseded by [MenuBar](https://learn.microsoft.com/en-us/windows/apps/design/controls/menus) in WinUI.
ListDetailsView|⚠️|
MetadataControl|✅|Ported to [MetadataControl](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/metadatacontrol/) in 8.0.
OrbitView|⚠️|
PropertySizer|⚡️|Newly introduced to 8.0.
PullToRefreshListView|❌|Superseded by [RefreshContainer](https://learn.microsoft.com/en-us/windows/apps/design/controls/pull-to-refresh) in WinUI.
RadialGauge|✅|Ported to [RadialGauge](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/radialgauge/) in 8.0. in 8.0.
RadialProgressBar|❌|Superseded by ProgressBar in WinUI.
RangeSelector|✅|Ported to [RangeSelector](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/rangeselector/) in 8.0.
RemoteDevicePicker|⚠️|
RichSuggestBox|✅|Ported to [RichSuggestBox](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/richsuggestbox/) in 8.0.
RotatorTile|⚠️|
ScrollHeader|❌|Superseded by FadeHeaderBehavior, QuickReturnHeaderBehavior, or StickyHeaderBehavior.
Segmented|⚡️|Newly introduced to 8.0.
SettingsCard|⚡️|Newly introduced to 8.0.
SettingsExpander|⚡️|Newly introduced to 8.0.
SlidableListItem|❌|Superseded by [SwipeControl](https://learn.microsoft.com/en-us/windows/apps/design/controls/swipe) in WinUI.
StaggeredLayout|✅|Ported to [StaggeredLayout](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/staggeredlayout) in 8.0.
StaggeredPanel|✅|Ported to [StaggeredPanel](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/staggeredpanel) in 8.0.
SwitchPresenter|♻️|Superseded by a new implementation, namely [SwitchPresenter](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/switchpresenter) v2.
TabbedCommandBar|✅|Ported to [TabbedCommandBar](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/tabbedcommandbar/) in 8.1.
TabView|❌|Superseded by [TabView](https://learn.microsoft.com/en-us/windows/apps/design/controls/tab-view) in WinUI.
TextToolbar|⚠️|
TileControl|⚠️|
TokenizingTextBox|✅|Ported to [TokenizingTextBox](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/tokenizingtextbox/) in 8.0.
UniformGrid|✅|Ported to [UniformGrid](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/uniformgrid) in 8.0.
WrapLayout|✅|Ported to [WrapLayout](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/wraplayout) in 8.0.
WrapPanel|✅|Ported to [WrapPanel](https://learn.microsoft.com/en-us/dotnet/communitytoolkit/windows/primitives/wrappanel) in 8.0.

## Converters

Name|Status|Remarks
---|:-:|---
BoolNegationConverter|✅|
BoolToObjectConverter|✅|
BoolToVisibilityConverter|✅|
CollectionVisibilityConverter|✅|
ColorToDisplayNameConverter|✅|
DoubleToObjectConverter|✅|
DoubleToVisibilityConverter|✅|
EmptyCollectionToObjectConverter|✅|
EmptyObjectToObjectConverter|✅|
EmptyStringToObjectConverte|✅|
FileSizeToFriendlyStringConverter|✅|
FormatStringConverter|❌|
ResourceNameToResourceStringConverter|✅|
StringFormatConverter|✅|
StringVisibilityConverter|✅|
TaskResultConverter|✅|
TypeToObjectConverter|✅|
VisibilityToBoolConverte|✅|
