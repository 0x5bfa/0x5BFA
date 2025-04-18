## Definition

```c#
public partial class TerminalView : Control {}
```

## Usage

```xml
<uc:TerminalView
    CurrentSession="{x:Bind ViewModel.CurrentSession, Mode=TwoWay}"
    Sessions="{x:Bind ViewModel.Sessions, Mode=OneWa}" />
```