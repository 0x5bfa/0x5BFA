## Definition

```c#
public partial class DataGrid : Control {}
```

## Usage

```xml
<DataGrid>

</DataGrid>
```

## Implementation

- Alternate row brush
- (Frozen column/row)
- Auto generation of columns
- Ability to resize
- Ability to reorder
- Ability to sort
- Ability to group
- Ability to select a cell


# Preface

While we have implemented TextBlocks and respective bindable string properties, it's almost impossible and not an effective way to create numerous numbers of columns that are provided by the Windows properties system. I propose these controls as below to support semi-permanent column generation. This way enables us to add as many columns in our backend as possible, without altering UI.

# Usage scenarios

Either way, you can create a custom column control and its default style deriving from `DataTableColumn` when necessary; for example, we can create `DataTableFileTagsColumn` to list tags that are tagged on an storage item. For more info, see "custom implementations" section.

## Dynamic columns & cells

This is useful when the columns have to be obtained at runtime or the number of columns is too numerous to create bindable source properties.

```xml
<ListView.Header>
    <DataTableHeader
        x:Name="DetailsViewDataTableHeader"
        AutoGenerateCells="True"
        CanResize="True"
        CanReorder="True"
        CanSort="True"
        Resized="DetailsViewDataTableHeader_Resized"
        Reordered="DetailsViewDataTableHeader_Reordered"
        Columns="{x:Bind ViewModel.VisibleColumns Mode=OneWay}"
        SortedColumn="{x:Bind ViewModel.SortedColumn Mode=TwoWay}"
        ContextFlyout="{x:Bind ViewModel.AvailableColumnsFlyout Mode=OneWay}" />
</ListView.Header>

<ListView.ItemTemplate>
    <DataTemplate>
        <DataTableRow />
    </DataTemplate>
</ListView.ItemTemplate>
```

## Hardcoded columns & cells

This is useful when the number of columns are small or limited.

```xml
<ListView.Header>
    <DataTableHeader
        x:Name="AdvancedAccessControlDataTableHeader"
        AutoGenerateCells="False"
        CanResize="True"
        CanReorder="False"
        CanSort="False"
        Resized="AdvancedAccessControlDataTableHeader_Resized"
        Reordered="AdvancedAccessControlDataTableHeader_Reordered">
        <DataTableHeader.Columns>
            <DataTableImageColumn CanResize="False"    DefaultWidth="16"  Source="{Binding Principal.Image}" />
            <DataTableTextColumn Name="Type"           DefaultWidth="60"  Source="{Binding TypeHumanized}" />
            <DataTableTextColumn Name="Principal"      DefaultWidth="200" Source="{Binding Principal.Name}" />
            <DataTableTextColumn Name="Access"         DefaultWidth="160" Source="{Binding AccessControlHumanized}" />
            <DataTableTextColumn Name="Inherited from" DefaultWidth="70"  Source="{Binding InheritanceSourceHumanized}" />
            <DataTableTextColumn Name="Applies to"     DefaultWidth="70"  Source="{Binding InheritanceHumanized}" />
        </DataTableHeader.Columns>
    </DataTableHeader>
</ListView.Header>

<ListView.ItemTemplate>
    <DataTemplate x:DataType="data:AccessControlItem">
        <DataTableRow />
    </DataTemplate>
</ListView.ItemTemplate>
```

# Built-in implementations

```c#
public partial class DataTableHeader : Grid {}
```
```c#
public partial class DataTableColumn : Control {}
public partial class DataTableImageColumn : DataTableColumn {}
public partial class DataTableTextColumn : DataTableColumn {}

// We might want to create more in-box controls here when necessary.
```
```c#
public partial class DataTableRow : StackPanel {}
```
```c#
public partial class DataTableCell : Control {}
```

# Custom implementations

While DataTable of WCT 7.x provides DataTableTemplateColumn for custom use cases, we can't provide that because we are going to support a collection of columns from view model to provide generative columns. Thus, I propose to let control users to create a custom column control. Here's an example.

```c#
public partial DataTableFileTagsColumn : DataTableColumn {}
```
```xml
<Style TargetType="controls:DataTableFileTagsColumn">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="controls:DataTableFileTagsColumn">
                <FileTags CanAddNewTag="False" />
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```
```xml
<!--  This means the column is hardcoded but you can also add the column to a collection and bind it to Columns property.  -->
<DataTableHeader.Columns>
    <DataTableFileTagsColumn Name="File tags" Source="{Binding FileTags}" />
</DataTableHeader.Columns>
```