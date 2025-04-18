## Trigger the context menu


![Image](https://i.sstatic.net/r7Z0N.png)

1. Register your app with `RegisterDragDrop`.
2. In the `IDropTarget.Drop` method:
    1. Obtain the `IShellFolder` interface for the drop path.
    2. Get the `IDropTarget` interface from this folder.
    3. Forward the `IDataObject` to the `DragEnter` and `Drop` methods.
    4. The `Drop` method will display the correct context menu.

```c#
void InvokeDragAndDropRMenu(IDropTarget* pDropTarget, IDataObject* pData, DWORD dwKeys, POINTL point, DWORD* pdwEffect)
{
    ComPtr<IShellFolder> pShellFolder = default;
    ComPtr<IDropTarget> pFolderDropTarget = default;

    hr = GetShellFolder(pszPath, pShellFolder.GetAddressOf());
    hr = pShellFolder.Get()->CreateViewObject(pShellFolder, &IID_IDropTarget, pFolderDropTarget.GetAddressOf());
    hr = pFolderDropTarget.Get()->DragEnter(pFolderDropTarget, pData, PInvoke.MK_RBUTTON, point, pdwEffect);
    hr = pFolderDropTarget.Get()->Drop(pFolderDropTarget, pData, PInvoke.MK_RBUTTON, point, pdwEffect);
}
```

## Mechanism



## References

- https://stackoverflow.com/q/78243894/16694806
- https://devblogs.microsoft.com/oldnewthing/20040831-00/?p=38003