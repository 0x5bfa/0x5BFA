## Definition

```c#
public partial class FilePreviewPresenter : Control {}
```

## Usage

```xml
<controls:FilePreviewPresenter ItemsSource="{x:Bind SelectedItems, Mode=OneWay}" />
```

## Implementation

```xml
<DataTemplate TargetType="controls:FilePreviewPresenter">
    <ContentPresenter Content="" /> <!--  Presenter  -->
</DataTemplate>
```
```c#
[GDP] public required partial object ItemsSource { get; set; }
[GDP] public          partial bool   IsPresenterRendered { get; }

public event EventHandler IsPresenterRendered;
public event EventHandler IsPresenterRenderingFailed;

public virtual partial void OnFilePropertyChanged(object oldValue, object newValue)
{
    if (newValue is not IEnumerable<IStorable> storables)
        return;

    var type = this.GetPreviewPresenterType(storables);

    FrameworkElement? presenter = type switch
    {
        PreviewPresenterType.Combined when this.TryCreatePresenterForCombinedFiles(newValue, out presenter) => presenter,
        PreviewPresenterType.PDF when this.TryCreatePresenterForPdfFile(newValue, out presenter) => presenter,
        PreviewPresenterType.HTML when this.TryCreatePresenterForHtmlFile(newValue, out presenter) => presenter,
        PreviewPresenterType.Image when this.TryCreatePresenterForImageFile(newValue, out presenter) => presenter,
        PreviewPresenterType.Video when this.TryCreatePresenterForVideoFile(newValue, out presenter) => presenter,
        PreviewPresenterType.Markdown when this.TryCreatePresenterForMarkdownFile(newValue, out presenter) => presenter,
#if WINDOWS
        _ when this.TryCreatePresenterForShellFile(newValue, out presenter) => presenter,
#endif
        _ => null,
    };

    if (presenter is null)
    {
        IsPresenterRenderingFailed?.Invoke(this, null);
    }
    else
    {
        UpdatePreviewPresenter(presenter);
        IsPresenterRendered?.Invoke(this, null);
    }
}
```

## Extendability

If you want to use your own custom previewer for a certain file type, you can override the previewer update method as below.

```c#
public override void OnItemsSourcePropertyChanged(object oldValue, object newValue)
{
    if (isAdobeIllustratorFile && this.TryCreatePresenterForAIFile(storables, out var presenter))
    {
        UpdatePreviewPresenter(presenter);
        IsPresenterRendered?.Invoke(this, null);
        return;
    }

    base.OnFilePropertyChanged(oldValue, newValue);
}
```