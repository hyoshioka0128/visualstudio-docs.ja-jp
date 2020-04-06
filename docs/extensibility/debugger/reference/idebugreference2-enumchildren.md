---
title: を参照します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::EnumChildren
helpviewer_keywords:
- IDebugReference2::EnumChildren
ms.assetid: 35b3c2f3-69f4-4013-b555-f847221f62e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 96b2fec782ce88dfb2200df35f56b35b304beda5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720625"
---
# <a name="idebugreference2enumchildren"></a>IDebugReference2::EnumChildren
参照の選択された子の一覧を取得します。 将来利用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumChildren ( 
   DEBUGREF_INFO_FLAGS        dwFields,
   DWORD                      dwRadix,
   DBG_ATTRIB_FLAGS           dwAttribFilter,
   LPCOLESTR                  pszNameFilter,
   DWORD                      dwTimeout,
   IEnumDebugReferenceInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGREF_INFO_FLAGS     dwFields,
   uint                         dwRadix,
   enum_DBG_ATTRIB_FLAGS        dwAttribFilter,
   string                       pszNameFilter,
   uint                         dwTimeout,
   out IEnumDebugReferenceInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[in]列挙された[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体のフィールドを指定する[DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)列挙体のフラグの組み合わせ。

`dwRadix`\
[in]数値情報の書式設定に使用する基数。

`dwAttribFilter`\
[in]列挙する構造体を選択する[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)`pszNameFilter`パラメーターと組み合わせてフィルターとして使用されるDBG_ATTRIB_FLAGS列挙体のフラグの組み合わせ。

`pszNameFilter`\
[in]列挙する構造体を選択するためにパラメーターと組み合わせて使用されるフィルターを`dwAttribFilter`指定する文字列 ("MyX" など)。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間 (ミリ秒単位)。 無期限`INFINITE`に待機するために使用します。

`ppEnum`\
[アウト]要求された[子](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)プロパティの一覧を含むオブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
