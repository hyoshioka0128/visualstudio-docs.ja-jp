---
title: DEBUG_REFERENCE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REFERENCE_INFO
helpviewer_keywords:
- DEBUG_REFERENCE_INFO structure
ms.assetid: 24b83d00-d756-42a1-8083-730f998761dc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e31205f52151679f932877c9c4fdc56907ea59e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737416"
---
# <a name="debug_reference_info"></a>DEBUG_REFERENCE_INFO
参照を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDEBUG_REFERENCE_INFO {
    DEBUGREF_INFO_FLAGS dwFields;
    BSTR                bstrName;
    BSTR                bstrType;
    BSTR                bstrValue;
    DBG_ATTRIB_FLAGS    dwAttrib;
    REFERENCE_TYPE.     dwRefType;
    IDebugReference2*   m_pReference;
} DEBUG_REFERENCE_INFO;
```

```csharp
public struct DEBUG_REFERENCE_INFO {
    public uint             dwFields;
    public string           bstrName;
    public string           bstrType;
    public string           bstrValue;
    public ulong            dwAttrib;
    public uint.            dwRefType;
    public IDebugReference2 m_pReference;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する、 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md) 列挙のフラグの組み合わせ。

`bstrName`\
[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)オブジェクトのユーザー指定の名前。

`bstrType`\
書式設定された文字列としての参照型。

`bstrValue`\
書式設定された文字列としての参照値

`dwAttrib`\
デバッグプロパティの属性のフラグを指定する、 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙型のフラグの組み合わせ。

`dwRefType`\
参照型が strong か weak かを指定する [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md) 列挙の値です。

`m_pReference`\
参照情報を指定する [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトです。

## <a name="remarks"></a>解説
この構造体は、入力される [Getreferenceinfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md) メソッドの呼び出しに渡されます。 この構造体は、 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) インターフェイスからのリストの一部としても返されます。このインターフェイスは、 [enumchildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) メソッドの呼び出しから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
