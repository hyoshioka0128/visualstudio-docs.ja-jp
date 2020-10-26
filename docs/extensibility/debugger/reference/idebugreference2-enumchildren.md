---
title: 'IDebugReference2:: EnumChildren |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80720625"
---
# <a name="idebugreference2enumchildren"></a>IDebugReference2::EnumChildren
参照の選択された子のリストを取得します。 将来使用するために予約されています。

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
から列挙された[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体に格納されるフィールドを指定する、 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)列挙のフラグの組み合わせ。

`dwRadix`\
から数値情報の書式設定に使用される基数。

`dwAttribFilter`\
から列挙する構造を選択するためのパラメーターと組み合わせてフィルターとして使用される、 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙のフラグの組み合わせ `pszNameFilter` 。

`pszNameFilter`\
から `dwAttribFilter` 列挙する構造体を選択するためにパラメーターと組み合わせて使用される、"MyX" などのフィルターを指定する文字列。

`dwTimeout`\
からこのメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 `INFINITE`無期限に待機するには、を使用します。

`ppEnum`\
入出力要求された子プロパティのリストを格納している [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
