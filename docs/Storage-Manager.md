## Converting string to IStorable

If you don't know what type to target to convert, this is helpful. If no suitable type found, the method throws an InvalidOperationException.

```c#
// Definition
public IStorable ToStorable(this path);

// Usage
path.ToStorable();
```

## Cnverting IStorable to various kinds of paths.

```c#
// Definition
string ToPath(
    this IWindowsStorable,
    WindowsStorablePathConversionType type);

// Usage
storable.ToPath(
    PathConversionType.Relative ||
    PathConversionType.Parseable);
```
