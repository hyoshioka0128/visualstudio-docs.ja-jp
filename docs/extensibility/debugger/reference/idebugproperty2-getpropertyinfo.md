---
title: 'IDebugProperty2:: GetPropertyInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetPropertyInfo
helpviewer_keywords:
- IDebugProperty2::GetPropertyInfo
ms.assetid: 39d6e942-df72-4c84-a5d9-a386d112714c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6ec1c3e29e0dbb6ca069dec696e6645a159ec7e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721365"
---
# <a name="idebugproperty2getpropertyinfo"></a>IDebugProperty2::GetPropertyInfo
プロパティを記述する [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPropertyInfo ( 
   DEBUGPROP_INFO_FLAGS dwFields,
   DWORD                nRadix,
   DWORD                dwTimeout,
   IDebugReference2**   rgpArgs,
   DWORD                dwArgCount,
   DEBUG_PROPERTY_INFO* pPropertyInfo
);
```

```cpp
int GetPropertyInfo ( 
   enum_DEBUGPROP_INFO_FLAGS dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_PROPERTY_INFO[]     pPropertyInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
から構造体に入力するフィールドを指定する、 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 列挙型の値の組み合わせ `pPropertyInfo` 。

`nRadix`\
から数値情報の書式設定で使用される基数。

`dwTimeout`\
からこのメソッドから制御が戻るまでに待機する最大時間をミリ秒単位で指定します。 `INFINITE`無期限に待機するには、を使用します。

`rgpArgs`\
[入力、出力]将来使用するために予約されています。を null 値に設定します。

`dwArgCount`\
から将来使用するために予約されています。を0に設定します。

`pPropertyInfo`\
入出力プロパティの説明が入力されている [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
