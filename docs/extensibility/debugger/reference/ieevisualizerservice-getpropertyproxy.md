---
description: このメソッドは、プロパティオブジェクトのプロキシを返します。
title: 'IEEVisualizerService:: GetPropertyProxy |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetPropertyProxy
helpviewer_keywords:
- IEEVisualizerService::GetPropertyProxy method
ms.assetid: 748750f4-76e7-4580-9da2-afba07681b37
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cbcaa460546443dcbc714a3fa72a6ebc7479dfc3
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222862"
---
# <a name="ieevisualizerservicegetpropertyproxy"></a>IEEVisualizerService::GetPropertyProxy
このメソッドは、プロパティオブジェクトのプロキシを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPropertyProxy(
   DWORD                  dwID,
   IPropertyProxyEESide** proxy
);
```

```csharp
int GetPropertyProxy(
   uint                     dwID,
   out IPropertyProxyEESide proxy
);
```

## <a name="parameters"></a>パラメーター
`dwID`\
から取得するプロパティプロキシの ID。

`proxy`\
入出力 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスに必要なプロキシが実装されています。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
- [Getpropertyproxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) は、型ビジュアライザーのサポートの一部として、このメソッドに要求を渡します。

## <a name="see-also"></a>関連項目
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)
