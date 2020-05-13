---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 79167b0f7e8094fabf80bb9b2d83c94ac874aa31
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714902"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
指定されたデータ オブジェクトを使用してオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータ オブジェクトを返します。

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
[in]新しいデータを含む[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)オブジェクト。

`dataOut`\
[アウト]置換されたデータ`IEEDataStorage`を含む新しいオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、実際にはオブジェクトのデータを更新します。 取得した[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)オブジェクトのデータは、受信`IEEDataStorage`オブジェクトのデータと同じである必要はありませんが、返されるオブジェクトはプロパティの現在の値を反映している必要があります。

 通常、受信データ オブジェクトは EE によって実装されません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装され、EE が任意`IEEDataStorage`のクラスにインターフェイスを実装できるようにします。

 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)メソッドは、入力データ オブジェクトに基づいてデータ オブジェクトを作成しますが、プロパティの元のデータには影響しません。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
