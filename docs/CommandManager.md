## Overview

## Usage

### Initialization

```c#
// FolderBrowser would initialize 
CommandManager.Initialize(CommandExecutionContexts.Browser);

// MainPageViewModel would initialize
CommandManager.Initialize(CommandExecutionContexts.Sidebar);

// MainPageViewModel would initialize
CommandManager.Initialize(CommandExecutionContexts.Tabs);
```

### Usage

Here's an example for Browser contextual command manager.

```c#
// MainPageViewModel
[ObservableObject]
[AlsoNotifyPropertyFor(nameof(CurrentFolderBrowser)]
public partial ITab SelectedTab { get; set; }

public FolderBrowser? CurrentFolderBrowser
    => SelectedTab.SelectedPane as FolderBrowser;
```

Using this for Omnibar, for example. But there's a fairly possibility that we'd wrap this into a user control for the sake of the simplicity of the MainPage XAML code.

```xml
<!--  Back button inside AddressBar, for example  -->
<Button
    Command="{x:Bind FolderBrowser.CommandManager.NavigateBack, Mode=OneWay}"
    ... />
```

Some user controls would want to get the whole command manager (as in CurrentFolderBrowser.CommandManager) as below:

```xml
<uc:AddressBar
    FolderBrowser="{x:Bind ViewModel.CurrentFolderBrowser, Mode=OneWay}"
    ... />

<uc:DetailsPane
    FolderBrowser="{x:Bind ViewModel.CurrentFolderBrowser, Mode=OneWay}"
    ... />

<uc:Toolbar
    FolderBrowser="{x:Bind ViewModel.CurrentFolderBrowser, Mode=OneWay}"
    ... />

<uc:StatusBar
    FolderBrowser="{x:Bind ViewModel.CurrentFolderBrowser, Mode=OneWay}"
    ... />
```

![MainPage XAML Structure](https://github.com/user-attachments/assets/9f102ac7-f075-4478-a6d2-f9ae1a2df574)


### Executing command

```c#
// Sync
if (CommandManager.NavigateBack.CanExecute())
    CommandManager.NavigateBack.Execute();

// Sync with parameter
if (CommandManager.NavigateBack.CanExecute(parameter))
    CommandManager.NavigateBack.Execute(parameter);
```

### Creating command

```c#
[RichCommand(GearChange = [ nameof(PermanentlyDeleteAction) ])]
internal class DeleteAction : IAction
{
    // Only can executes with the Browser context
    public static CommandExecutionContexts ExecutableContexts = CommandExecutionContexts.Browser;

    public string Title => "";

    public string Description => "";

    public HotKey DefaultHotKey => new(...);

    public Task<bool> CanExecuteAsync()
    {
        // Verify the executability

        return Task.FromResult(...);
    }

    public Task ExecuteAsync(CommandExecutionContexts context, object? parameter)
    {
        if (!ExecutableContexts.HasFlag(context)
            return throw new InvalidOperarionException($"This command cannot be executed with the given context: {context}");

        // Execute...
    }
}
```

## Source generator

### RichCommandAttribute

```c#
[AttributeUsage(AttributeTargets.Class, AllowMultiple = false, Inherited = false)]
public sealed class RichCommandAttribute : Attribute {}
```

```c#
// CommandManager.g.cs
namespace global::Files.App.Data
{
    internal partial class CommandManager
    {
        private readonly FrozenDictionary<CommandCodes, IRichCommand> commands;
        private readonly FrozenDictionary<CommandCodes, IRichCommand> modifiableCommands;

        public IRichCommand NavigateBack { get; } = new ActionCommand(CommandCodes.NavigateBack, new NavigateBackAction());
...

        public bool Initialize(CommandExecutionContexts context)
        {
...

            commands =
            [
                [CommandCodes.NavigateBack] = new NavigateBackAction(),
...
            ];

...
        }
    }

    internal enum CommandCodes
    {
        NavigateBack,
...
    }
}
```

## Modifiable command

```c#
public void AppendModifiableCommands()
{
    modifiableCommands = [ ... ];
}
```