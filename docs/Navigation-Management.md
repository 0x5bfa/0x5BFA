## Definitions

```c#
[MethodImpl(MethodImplOptions.AggressiveInlining)]
IWindow GetCurrentWindow();
```
```c#
[MethodImpl(MethodImplOptions.AggressiveInlining)]
ITab GetCurrentTab();
```
```c#
[MethodImpl(MethodImplOptions.AggressiveInlining)]
IPane GetCurrentPane();
```

## Tab

```c#
// Add a new pane
App.GetCurrentWindow().AddNewTab(new WindowsFolder("C:\\Windows"), moveToNewTab: true);
```
```c#
// Get the current tab
App.GetCurrentWindow().GetCurrentTab();
```
```c#
// Close all tabs
App.GetCurrentWindow().CloseAllTabs();
```
```c#
// Save the open tabs to local
App.GetCurrentWindow().SaveTabs();
```
```c#
// Save the open tabs to local
App.GetCurrentWindow().RestoreTabs();
```

## Pane

```c#
// Add a new pane
App.GetCurrentWindow().GetCurrentTab().AddPane(new WindowsFolder("C:\\Windows"));
```
```c#
// Get the current pane
App.GetCurrentWindow().GetCurrentTab().GetCurrentPane();
```

## Shared UI objects

```c#
var pane = App.GetCurrentWindow().GetCurrentTab().GetCurrentPane();
pane.GetBrowserCommandManager();
```

## Misc

```c#
NavigationManager.OpenFileExternally();
```
