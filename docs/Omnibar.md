## Definition

```c#
public partial class Omnibar : Control {}
public partial class OmnibarInputBox : Control {}
```

## Usage

```xml
<controls:Omnibar ActiveMode="{x:Bind ViewModel.CurrentActiveMode, Mode=OneWay}">

    <!--  Path  -->
    <controls:OmnibarMode
        HideContentOnInactive="True"
        Text="{x:Bind ViewModel.PathText, Mode=TwoWay}">

        <controls:OmnibarMode.IconOnActive>
            <controls:ThemedIcon Style="{StaticResource App.ThemedIcons.Path}" IsFilled="True" />
        </controls:OmnibarMode.IconOnActive>
        <controls:OmnibarMode.IconOnInactive>
            <controls:ThemedIcon Style="{StaticResource App.ThemedIcons.Path}" />
        </controls:OmnibarMode.IconOnInactive>
        <controls:OmnibarMode.SuggestionItemTemplate>
            <DataTemplate x:DataType="item:OmnibarSuggestionItem">
                ...
            </DataTemplate>
        </controls:OmnibarMode.SuggestionItemTemplate>

    </controls:OmnibarMode>

    <!--  Palette  -->
    <controls:OmnibarMode
        HideContentOnInactive="True"
        Text="{x:Bind ViewModel.PaletteText, Mode=TwoWay}">

        <controls:OmnibarMode.IconOnActive>
            <controls:ThemedIcon Style="{StaticResource App.ThemedIcons.Palette}" IsFilled="True" />
        </controls:OmnibarMode.IconOnActive>
        <controls:OmnibarMode.IconOnInactive>
            <controls:ThemedIcon Style="{StaticResource App.ThemedIcons.Palette}" />
        </controls:OmnibarMode.IconOnInactive>
        <controls:OmnibarMode.SuggestionItemTemplate>
            <DataTemplate x:DataType="item:OmnibarSuggestionItem">
                ...
            </DataTemplate>
        </controls:OmnibarMode.SuggestionItemTemplate>

    </controls:OmnibarMode>

    <!--  Search  -->
    <controls:OmnibarMode
        HideContentOnInactive="False"
        Text="{x:Bind ViewModel.SearchText, Mode=TwoWay}"
        Tokens="{x:Bind ViewModel.SearchTokens, Mode=TwoWay}">

        <controls:OmnibarMode.IconOnActive>
            <controls:ThemedIcon Style="{StaticResource App.ThemedIcons.Search}" IsFilled="True" />
        </controls:OmnibarMode.IconOnActive>
        <controls:OmnibarMode.IconOnInactive>
            <controls:ThemedIcon Style="{StaticResource App.ThemedIcons.Search}" />
        </controls:OmnibarMode.IconOnInactive>
        <controls:OmnibarMode.SuggestionItemTemplate>
            <DataTemplate x:DataType="item:OmnibarSuggestionItem">
                ...
            </DataTemplate>
        </controls:OmnibarMode.SuggestionItemTemplate>

        <controls:OmnibarMode.Footer>
            <Button ... /> <!--  Search Options  -->
        </controls:OmnibarMode.Footer>

    </controls:OmnibarMode>

</controls:Omnibar>

<controls:BreadcrumbBar
    ItemsSource="{x:Bind ViewModel.Breadcrumbs, Mode=TwoWay}" />
```

## Implementation

**Omnibar**

```c#
[GDP] public require partial FrameworkElement Header { get; set; }
[GDP] public require partial FrameworkElement Footer { get; set; }
[GDP] public require partial IList<OmnibarMode> Modes { get; set; }
[GDP] public require partial OmnibarMode? ActiveMode { get; set; }
[GDP] public require partial FrameworkElement ContentOnInactive { get; set; }
```

**OmnibarInputBox**

```c#
[GDP] public require partial bool KeepInactiveOnUnfocused { get; set; }
[GDP] public require partial bool IsActive { get; set; }
[GDP] public require partial FrameworkElement Footer { get; set; }
[GDP] public require partial FrameworkElement IconOnActive { get; set; }
[GDP] public require partial FrameworkElement IconOnInactive { get; set; }
[GDP] public require partial DataTemplate SuggestionItemTemplate { get; set; }
[GDP] public require partial string Text { get; set; }
[GDP] public require partial IList<RichToken> Tokens { get; set; }
```