---
description: この構造体は、メタデータから取得されたフィールド型に関する情報を指定します。
title: BUILT_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd9f5984861b0f56e4a46b4f793a38bbb3bafa60
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170986"
---
# <a name="built_type"></a>BUILT_TYPE
この構造体は、メタデータから取得されたフィールド型に関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTYPE_BUILT {
    ULONG32      ulAppDomainID;
    GUID         guidModule;
    IDebugField* pUnderlyingField;
} BUILT_TYPE;
```

```csharp
public struct BUILT_TYPE {
    public uint        ulAppDomainID;
    public Guid        guidModule;
    public IDebugField pUnderlyingField;
};
```

## <a name="members"></a>メンバー
`ulAppDomainID`\
シンボルの取得元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

`guidModule`\
このフィールドを含むモジュールの GUID。

`pUnderlyingField`\
この構築されたフィールドに関連付けられている基になるフィールドを識別する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクト。

## <a name="remarks"></a>解説
この構造体は、構造体のフィールドがに設定されている場合に、 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体の共用体の一部として表示され `dwKind` `TYPE_INFO` `TYPE_KIND_BUILT` ます ( [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値)。

## <a name="requirements"></a>必要条件
ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
