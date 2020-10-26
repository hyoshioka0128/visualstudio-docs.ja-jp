---
title: 'IDebugProperty2:: EnumChildren |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::EnumChildren
helpviewer_keywords:
- IDebugProperty2::EnumChildren
ms.assetid: cf79f666-65d1-417c-af7c-9271bac9a267
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d6d3908c469b489eb16e4662f7515ea624825e3b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721514"
---
# <a name="idebugproperty2enumchildren"></a>IDebugProperty2::EnumChildren
プロパティの子のリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumChildren ( 
   DEBUGPROP_INFO_FLAGS      dwFields,
   DWORD                     dwRadix,
   REFGUID                   guidFilter,
   DBG_ATTRIB_FLAGS          dwAttribFilter,
   LPCOLESTR                 pszNameFilter,
   DWORD                     dwTimeout,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFields,
   uint                        dwRadix,
   ref Guid                    guidFilter,
   uint                        dwAttribFilter,
   string                      pszNameFilter,
   uint                        dwTimeout,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
から列挙された[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体に格納されるフィールドを指定する、 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)列挙のフラグの組み合わせ。

`dwRadix`\
から数値情報の書式設定に使用する基数を指定します。

`guidFilter`\
から `dwAttribFilter` `pszNameFilter` 列挙する子を選択するために、パラメーターとパラメーターで使用されるフィルターの GUID `DEBUG_PROPERTY_INFO` 。 たとえば、 `guidFilterLocals` ローカル変数をフィルター処理します。

`dwAttribFilter`\
から列挙するオブジェクトの型を指定する、 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙体のフラグの組み合わせ `DBG_ATTRIB_METHOD` 。このプロパティの子になる可能性のあるすべてのメソッドなどがあります。 パラメーターとパラメーターを組み合わせて使用 `guidFilter` `pszNameFilter` します。

`pszNameFilter`\
から `guidFilter` `dwAttribFilter` 列挙する子を選択するために、パラメーターとパラメーターで使用されるフィルターの名前 `DEBUG_PROPERTY_INFO` 。 たとえば、"MyX" という名前のすべての子のフィルターを "MyX" に設定します。

`dwTimeout`\
からこのメソッドから制御が戻るまでに待機する最大時間をミリ秒単位で指定します。 `INFINITE`無期限に待機するには、を使用します。

`ppEnum`\
入出力子プロパティのリストを格納している [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
