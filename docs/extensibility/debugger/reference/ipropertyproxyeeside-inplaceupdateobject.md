---
description: 指定されたデータオブジェクトを使用してオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータオブジェクトを返します。
title: 'IPropertyProxyEESide:: Inplace Updateobject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6fb6c098d26148db39493b25f199c6819fb81d27
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082414"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
指定されたデータオブジェクトを使用してオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータオブジェクトを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT InPlaceUpdateObject(
   [in] IEEDataStorage*   dataIn,
   [out] IEEDataStorage** dataOut
);
```

```csharp
int InPlaceUpdateObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataIn`\
から新しいデータを格納する [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクト。

`dataOut`\
入出力 `IEEDataStorage` 置き換えられたデータを格納している新しいオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、実際にオブジェクトのデータを更新します。 返された [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトのデータは、受信オブジェクトのデータと同じである必要はありません `IEEDataStorage` が、返されたオブジェクトにはプロパティの現在の値が反映されている必要があります。

 受信データオブジェクトは、通常、EE によって実装されていません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装されます。これにより、EE は `IEEDataStorage` 任意のクラスで必要なインターフェイスを実装できます。

 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)メソッドは、受信データオブジェクトに基づいてデータオブジェクトを作成しますが、プロパティの元のデータには影響しません。

## <a name="see-also"></a>こちらもご覧ください
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
