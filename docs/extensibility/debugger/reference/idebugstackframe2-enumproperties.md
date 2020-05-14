---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f822f20cf4fb7a6fd5aa71b9cc1ec26bcd90e234
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719902"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
ローカル変数など、スタック フレームに関連付けられているプロパティの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumProperties ( 
   DEBUGPROP_INFO_FLAGS      dwFieldSpec,
   UINT                      nRadix,
   REFIID                    refiid,
   DWORD                     dwTimeout,
   ULONG*                    pcelt,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumProperties ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFieldSpec,
   uint                        nRadix,
   ref Guid                    refiid,
   uint                        dwTimeout,
   out uint                    pcelt,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFieldSpec`\
[in]列挙された[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体内のどのフィールドに入力するかを指定する[、DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)列挙体のフラグの組み合わせ。

`nRadix`\
[in]数値情報の書式設定に使用する基数。

`refiid`\
[in]列挙する[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造を選択するために使用されるフィルターの GUID ( など`guidFilterLocals`)

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間 (ミリ秒単位)。 無期限`INFINITE`に待機するために使用します。

`pcelt`\
[アウト]列挙されたプロパティの数を返します。 これは[、GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)メソッドを呼び出すのと同じです。

`ppEnum`\
[アウト]目的の[プロパティ](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)の一覧を含むオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドでは、1 回の呼び出しですべての選択したプロパティを取得できるため[、GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)メソッドと[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)メソッドを順次呼び出すよりも高速です。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
