## Definition

```c#
public partial class SidebarView : Control {}
```

## Usage

```xml
<SidebarView
    DisplayMode=""
    IsPaneOpen=""
    OpenPaneLength=""
    SelectedItem="">

    <SidebarView.MenuItems>
        <SidebarItem Text="Home" />
        <SidebarItem Text="Pinned" SubItems="" CanBeHeader="True" />
        <SidebarItem Text="Libraries" SubItems="" CanBeHeader="True" />
        <SidebarItem Text="Drives" SubItems="" CanBeHeader="True" />
        <SidebarItem Text="Cloud drives" SubItems="" CanBeHeader="True" />
        <SidebarItem Text="Tags" SubItems="" CanBeHeader="True" />
    </SidebarView.MenuItems>

    <SidebarView.FooterItems>
        <SidebarItem Text="Settings" />
    </SidebarView.FooterItems>

    <SidebarView.Content>
        <Grid>
            <Toolbar />
            <!--  One or two FolderBrowser here  -->
            <DetailsPane />
            <TerminalView />
        </Grid>
    </SidebarView.Content>

</SidebarView>
```

## Implementation

**SidebarView**

```c#

```

**SidebarItem**

```c#
// This indicates whether the item should be styled like header.
[GDP] public /**/ ApplyHeaderStyle { get; set; }

// ...
```