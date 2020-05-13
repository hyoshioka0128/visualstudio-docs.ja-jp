---
title: プロパティ 2::列挙子 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
[in]列挙された[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体内のどのフィールドに入力するかを指定する[、DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)列挙体のフラグの組み合わせ。

`dwRadix`\
[in]数値情報の書式設定に使用する基数を指定します。

`guidFilter`\
[in]列挙する子を`dwAttribFilter`選択するための パラメーター`pszNameFilter`および パラメーターで`DEBUG_PROPERTY_INFO`使用されるフィルターの GUID。 たとえば、`guidFilterLocals`ローカル変数のフィルター。

`dwAttribFilter`\
[in]列挙するオブジェクトの種類を指定する[DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)列挙体のフラグの組み合わせ。`DBG_ATTRIB_METHOD`たとえば、このプロパティの子である可能性のあるすべてのメソッドに対して指定します。 と`pszNameFilter`パラメーターと組`guidFilter`み合わせて使用されます。

`pszNameFilter`\
[in]列挙する子を選択するための パラメーター`guidFilter`および`dwAttribFilter`パラメーターで使用`DEBUG_PROPERTY_INFO`されるフィルターの名前。 たとえば、このパラメータを"MyX"という名前のすべての子に対して"MyX"フィルタに設定します。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間をミリ秒単位で指定します。 無期限`INFINITE`に待機するために使用します。

`ppEnum`\
[アウト]子プロパティ[のリスト](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)を含むオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
