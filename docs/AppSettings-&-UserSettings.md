## Overview

```c#
public abstract class BaseJsonSettings : IDisposable, INotifyPropertyChanged {}

public static partial class AppSettings : BaseJsonSettings {}

public static partial class UserSettings : BaseJsonSettings {}
```

## Classes

### BaseJsonSettings

<details>
<summary>Code sample</summary>

```c#
using System.Text.Json;

namespace Files.App.Data.Settings;

public abstract class BaseJsonSettings : IDisposable, INotifyPropertyChanged
{
    // Fields

    private IDictionary<string, object?>? _cache;

    private IFile? _jsonFile;

    // Events

    public event JsonSerializeFailed;

    public event PropertyChangedEventHandler? PropertyChanged;

    // Methods

    public bool Initialize(IFile jsonFile)
    {
        _jsonFile = jsonFile
        if (_jsonFile is IMutableStorable mutableFile)
            mutableFile.FileUpdated += ...;
    }

    public bool ImportJson(object? jsonObject)
    {
        if (jsonObject is not IDictionary<string, object?> json)
            return false;

        return SaveJsonDeserialized(json);
    }

    public bool ExportJsonAsync(out object? jsonObject)
    {
        jsonObject = GetJsonDeserialized();

        return true;
    }

    private TValue? Get<TValue>(TValue? defaultValue, [CallerMemberName] string key = "")
    {
        if (String.IsNullOrWhiteSpace(propertyName)) return defaultValue;

        _cache ??= GetJsonDeserialized();

        if (_cache.TryGetValue(key, out var cachedValue))
        {
            return obj is JsonElement jsonElement
                ? jsonElement.Deserialize<TValue>();
                : (TValue?)obj;
        }
        else
        {
            _cache = GetJsonDeserialized();

            if (!_cache.TryAdd(key, defaultValue))
                _cache[key] = defaultValue;

            if (SaveJsonDeserialized(_cache))
                OnPropertyChanged(key);

            return defaultValue;
        }
    }

    private bool Set<TValue>(TValue? value, [CallerMemberName] string key = "")
    {
        if (String.IsNullOrWhiteSpace(key)) return false;

        _cache ??= GetJsonDeserialized();

        if (!_settingsCache.TryAdd(key, value))
        {
            bool isDifferent = _cache[key] is IEnumerable oldEnumerable && value is IEnumerable newEnumerable
                ? !oldEnumerable.Cast<object>().SequenceEqual(newEnumerable.Cast<object>())
                : value != (object?)newValue;

            if (!isDifferent)
                return false;

            _cache[key] = value;
        }

        if (!SaveJsonDeserialized(_cache))
            return false;

        OnPropertyChanged(key);
        return true;
    }

    private IDictionary<string, object?> GetJsonDeserialized()
    {
        string jsonString = string.Empty;

        if (jsonFile is IReadableStorable readable)
            jsonString = readable.Read();

        JsonSerializer.Deserialize<ConcurrentDictionary<string, object?>?>(jsonString) ? [];
    }

    private bool SaveJsonDeserialized(IDictionary<string, object?> data)
    {
        var jsonString = JsonSerializer.Serialize(obj, new() { WriteIndented = true });

        return jsonFile is IWritableStorable writable ? writable.Write(jsonString) : false;
    }

    private void OnPropertyChanged([CallerMemberName] string key = "")
    {
        PropertyChanged?.Invoke(this, new(key));
    }

    // Disposer

    public async Task DisposeAsync()
    {
        _jsonFile.DisposeAsync();
    }
}
```

</details>

### AppSettings.cs

```c#
using Files.Core;

namespace Files.App.Data.Settings;

public static partial class AppSettings : BaseJsonSettings
{
    [GeneratedSettingsProperty(DefaultValue = 0)]
    public partial uint LaunchCount { get; set; }

    [GeneratedSettingsProperty(DefaultValue = -1l)]
    public partial long ActivePid { get; set; }
}
```

### UserSettings.Appearance.cs

```c#
using Files.Core;

namespace Files.App.Data.Settings;

public static partial class UserSettings : BaseJsonSettings
{
    [GeneratedSettingsProperty(DefaultValue = 255d)]
    public partial double SidebarWidth { get; set; }

    [GeneratedSettingsProperty(DefaultValue = true)]
    public partial bool IsSidebarOpen { get; set; }

    [GeneratedSettingsProperty(DefaultValue = "Default")]
    public partial string AppThemeMode { get; set; }
}
```
