---
title: BUILT_TYPE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 885f17b0841a39672c87be5bc7c947b2e0d9c7e0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737704"
---
# <a name="built_type"></a>BUILT_TYPE
この構造体は、メタデータから取得したフィールド型に関する情報を指定します。

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
シンボルの元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

`guidModule`\
このフィールドを含むモジュールの GUID。

`pUnderlyingField`\
この構築フィールドに関連付けられている基になるフィールドを識別する[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクト。

## <a name="remarks"></a>Remarks
この構造体は、構造体`dwKind`のフィールドが[(dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)列挙体の値)`TYPE_INFO`に`TYPE_KIND_BUILT`設定されている場合[、TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)構造体の共用体の一部として表示されます。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
