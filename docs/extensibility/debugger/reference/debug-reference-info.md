---
title: DEBUG_REFERENCE_INFO |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737416"
---
# <a name="debug_reference_info"></a>DEBUG_REFERENCE_INFO
参照について説明します。

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
入力するフィールドを指定する[DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)列挙体のフラグの組み合わせ。

`bstrName`\
オブジェクトのユーザー指定の名前。 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

`bstrType`\
書式設定された文字列としての参照型。

`bstrValue`\
書式設定された文字列としての参照値

`dwAttrib`\
デバッグ プロパティ属性のフラグを指定する[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)列挙体のフラグの組み合わせ。

`dwRefType`\
参照型が強いか弱いかを指定する[REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)列挙体の値。

`m_pReference`\
参照情報を指定する[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)オブジェクト。

## <a name="remarks"></a>Remarks
この構造体は[、GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)メソッドへの呼び出しに渡され、入力されます。 この構造体は、列挙子メソッドの呼び出しから返される[、IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)インターフェイスからのリストの一部としても返[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
