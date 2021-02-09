---
title: DEBUG_CUSTOM_VIEWER |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_CUSTOM_VIEWER
helpviewer_keywords:
- DEBUG_CUSTOM_VIEWER structure
ms.assetid: 8e0ef3f0-0107-48e8-a037-6e52b4c4ed9d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6fa8e8d9e07510a10b1b32534f3323dab4c84a22
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899102"
---
# <a name="debug_custom_viewer"></a>DEBUG_CUSTOM_VIEWER
カスタムビューアーまたは型ビジュアライザーを識別する構造体。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDEBUG_CUSTOM_VIEWER {
    DWORD dwID;
    BSTR  bstrMenuName;
    BSTR  bstrDescription;
    GUID  guidLang;
    GUID  guidVendor;
    BSTR  bstrMetric;
} DEBUG_CUSTOM_VIEWER;
```

```csharp
public struct DEBUG_CUSTOM_VIEWER {
    public uint   dwID;
    public string bstrMenuName;
    public string bstrDescription;
    public Guid   guidLang;
    public Guid   guidVendor;
    public string bstrMetric;
};
```

## <a name="members"></a>メンバー
`dwID`\
1つのユーザーによって実装された複数のビューアーまたはビジュアライザーを区別する ID `GUID` 。

`bstrMenuName`\
ドロップダウンメニューに表示されるテキスト。

`bstrDescription`\
カスタムビューアーまたは型ビジュアライザーの説明。使用されていない場合は、null 値を指定する必要があります。

`guidLang`\
式エバリュエーターを提供するの言語。

`guidVendor`\
式エバリュエーターを提供するのベンダ。

`bstrMetric`\
カスタムビューアーまたは型ビジュアライザーが格納されるメトリック `CLSID` 。

## <a name="remarks"></a>解説
この構造体のリストは、 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) メソッドの呼び出し (および拡張による [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) メソッド) によって返されます。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
