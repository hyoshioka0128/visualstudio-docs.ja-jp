---
title: 置換オブジェクトの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::CreateReplacementObject
helpviewer_keywords:
- IPropertyProxyEESide::CreateReplacementObject
ms.assetid: 0cfe79b8-c3f1-48b0-a225-e39dee2c92fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f449a505c56c180f1bab021007f1b635a2461996
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715036"
---
# <a name="ipropertyproxyeesidecreatereplacementobject"></a>IPropertyProxyEESide::CreateReplacementObject
式エバリュエーター (EE) に固有のデータ オブジェクトのコピーを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateReplacementObject(
   IEEDataStorage*  dataIn,
   IEEDataStorage** dataOut
);
```

```csharp
int CreateReplacementObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataIn`\
[in]コピーするデータを保持する[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)オブジェクト。

`dataOut`\
[アウト]新しい`IEEDataStorage`オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドには、バイト配列を表す[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)オブジェクトが与えられます。 この受信データ オブジェクトは、通常 EE によって実装されません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装され、EE が任意`IEEDataStorage`のクラスにインターフェイスを実装できるようにします。

 受信`IEEDataStorage`オブジェクトから提供されるデータは、出力`IEEDataStorage`オブジェクト内の同じデータである必要があります。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
