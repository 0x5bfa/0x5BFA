## Overview

There're 5 ways to execute querying storage objects:

Interface|Accessibility|Remarks
---|---|---
`IDesktopSearch`|Windows XP onwards (WDS 2.x)|Deprecated.
`ISearchQueryHelper` + OLE DB|Windows XP onwards (WDS 3.x)|Deprecated.
`ISearchQueryHelper` + ADO (ActiveX Data Objects)|Windows XP onwards (WDS 3.x)|Deprecated.
`ISearchFolderItemFactory`|Windows 7 onwards (Shell API)|Preferred.
`Windows.Storage.Search`|Windows 10 (Build 10240) onwards (WinRT API)|Preferred.

We're going to query storage objects with various query syntaxes in C# but more native-like using `ISearchFolderItemFactory`, like how File Explorer executes file search.

## Initialization

```c#
ComPtr<IShellItemArray> pSearchScope = ...; // Represents `FOLDERID_DocumentsLibrary`, for example.

ComPtr<ISearchFolderItemFactory> pSearchFolderItemFactory = default;
pSearchFolderItemFactory.CoCreateInstance(CLSCTX.CLSCTX_INPROC_SERVER);

pSearchFolderItemFactory.Get()->SetScope(pSearchScope.Get());
pSearchFolderItemFactory.Get()->SetDisplayName("Search Results");
```

## Set query object from AQS or NQS string

```c#
ComPtr<IQueryParserManager> pQueryParserManager = default;
ComPtr<IQueryParser> pQueryParser = default;
ComPtr<ICondition> pCondition = default;

pQueryParserManager.CoCreateInstance(CLSCTX.CLSCTX_INPROC_SERVER);
pQueryParserManager.Get()->CreateLoadedParser("SystemIndex", LOCALE_USER_DEFAULT, IID.IID_IQueryParser, pQueryParser.GetAddressOf());
pQueryParser.Get()->Parse(L"name:example AND size:>100", null, pCondition.GetAddressOf());

pSearchFolderItemFactory.Get()->SetCondition(pCondition.Get());
```

## Enumerate results

```c#
ComPtr<IShellItem> pSearchResultsFolder = default;
ComPtr<IEnumIDList> pEnumIDList = default;
ComPtr<ITEMIDLIST> pSearchResultsChildPidl = default;
ComPtr<IShellItem> pSearchResultaChildItem = default;

pSearchFolderItemFactory.Get()->GetShellItem(IID.IID_IShellItem, pSearchResultsFolder.GetAddressOf());

pSearchResultsFolder.Get()->EnumObjects(null, 0, pEnumIDList.GetAddressOf());

while (pEnumIDList.Next(1, pSearchResultsChild.GetAddressOf(), null))
{
    // Enumerate children
    PInvoke.SHCreateItemWithParent(null, pSearchResultsFolder, IID.IID_IShellItem, pSearchResultaChildItem.GetAddressOf());
}
```

## AQS

### Leaf types

Name|Syntax|Description
---|---|---
CT_AND_CONDITION|`AND`|Indicates that the values of the subterms are combined by "AND".
CT_OR_CONDITION|`OR`|Indicates that the values of the subterms are combined by "OR".
CT_NOT_CONDITION|`NOT`|Indicates a "NOT" comparison of subterms.
CT_LEAF_CONDITION|N/A|Indicates that the node is a comparison between a property and a constant value using a CONDITION_OPERATION.

### Parameters

> [!CRITICAL]
> Needs thorough research, how the locale issue can be resolved?

Canonical or mnemonic names of properties on Windows Property System.

### Operators

Definition|Symbol|Description
---|---|---
COP_EQUAL|`=`|The value of the property and the value of the constant must be equal.
COP_NOTEQUAL|`≠`, `-`, `<>`, `NOT`, `- -`|The value of the property and the value of the constant must not be equal.
COP_LESSTHAN|`<`|The value of the property must be less than the value of the constant.
COP_GREATERTHAN|`>`|The value of the property must be greater than the value of the constant.
COP_LESSTHANOREQUAL|`<=`|The value of the property must be less than or equal to the value of the constant.
COP_GREATERTHANOREQUAL|`>=`|The value of the property must be greater than or equal to the value of the constant.
COP_VALUE_STARTSWITH|`~<`|The value of the property must begin with the value of the constant.
COP_VALUE_ENDSWITH|`~>`|The value of the property must end with the value of the constant.
COP_VALUE_CONTAINS|`~=`, `~~`|The value of the property must contain the value of the constant.
COP_VALUE_NOTCONTAINS|`~!`|The value of the property must not contain the value of the constant.
COP_DOSWILDCARDS|`~`|The value of the property must match the value of the constant, where '?' matches any single character and '*' matches any sequence of characters.
COP_WORD_EQUAL|`$=`, `$$`|The value of the property must contain a word that is the value of the constant.
COP_WORD_STARTSWITH|`$<`|The value of the property must contain a word that begins with the value of the constant.
COP_APPLICATION_SPECIFIC|N/A|The application is free to interpret this in any suitable way.

### Value types

Name|Example|Description
---|---|---
string|`auto`, `"auto"`
integer|`5678`|
floating point number|`5678.1234`|
boolean|`System.StructuredQueryType.Boolean#True`|
empty square brackets|`[]`|
absolute date|`1/26/2010`, `10/15/2002 19:00`|
relative date|`System.StructuredQueryType.DateTime#Today`|
span|`5kb..10kb`|

### Scopes