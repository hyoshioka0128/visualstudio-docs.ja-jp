---
title: DEBUG_CUSTOM_VIEWER |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_CUSTOM_VIEWER
helpviewer_keywords:
- DEBUG_CUSTOM_VIEWER structure
ms.assetid: 8e0ef3f0-0107-48e8-a037-6e52b4c4ed9d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3de9b8f7ef30cffbdd78399dc831060e413ba51b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737548"
---
# <a name="debug_custom_viewer"></a>DEBUG_CUSTOM_VIEWER
カスタム ビューアーまたは型ビジュアライザーを識別する構造体。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDEBUG_CUSTOM_VIEWER {
    DWORD dwID;
    BSTR  bstrMenuName;
    BSTR  bstrDescription;
    GUID  guidLang;
    GUID  guidVendor;
    BSTR  bstrMetric;
} DEBUG_CUSTOM_VIEWER;
```

```csharp
public struct DEBUG_CUSTOM_VIEWER {
    public uint   dwID;
    public string bstrMenuName;
    public string bstrDescription;
    public Guid   guidLang;
    public Guid   guidVendor;
    public string bstrMetric;
};
```

## <a name="members"></a>メンバー
`dwID`\
1 つ`GUID`によって実装された複数のビューアーまたはビジュアライザーを区別するための ID 。

`bstrMenuName`\
ドロップダウン メニューに表示されるテキスト。

`bstrDescription`\
カスタム ビューアーまたは型ビジュアライザーの説明 (使用しない場合は null 値である必要があります)。

`guidLang`\
提供式エバリュエーターの言語。

`guidVendor`\
提供式エバリュエーターのベンダー。

`bstrMetric`\
カスタム ビューアーまたは型ビジュアライザー`CLSID`が格納されるメトリック。

## <a name="remarks"></a>Remarks
この構造体のリストは、メソッド (および拡張によって[、GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)メソッド) の呼び[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)出しによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
