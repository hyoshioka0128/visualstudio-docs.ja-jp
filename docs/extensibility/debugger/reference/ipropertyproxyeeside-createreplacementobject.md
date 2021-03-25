---
description: 式エバリュエーター (EE) に固有のデータオブジェクトのコピーを作成します。
title: 'IPropertyProxyEESide:: CreateReplacementObject |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::CreateReplacementObject
helpviewer_keywords:
- IPropertyProxyEESide::CreateReplacementObject
ms.assetid: 0cfe79b8-c3f1-48b0-a225-e39dee2c92fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 460052ceb9f2f90a5123f4cc646682919f96dc94
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082583"
---
# <a name="ipropertyproxyeesidecreatereplacementobject"></a>IPropertyProxyEESide::CreateReplacementObject
式エバリュエーター (EE) に固有のデータオブジェクトのコピーを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateReplacementObject(
   IEEDataStorage*  dataIn,
   IEEDataStorage** dataOut
);
```

```csharp
int CreateReplacementObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataIn`\
からコピーされるデータを保持する [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクト。

`dataOut`\
入出力新しいオブジェクトを返し `IEEDataStorage` ます。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドには、バイト配列を表す [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトが指定されています。 この受信データオブジェクトは、通常、EE によって実装されていません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装されます。これにより、EE は `IEEDataStorage` 任意のクラスで必要なインターフェイスを実装できます。

 受信オブジェクトによって提供されるデータは、 `IEEDataStorage` 送信オブジェクトのデータと同じである必要があることに注意してください `IEEDataStorage` 。

## <a name="see-also"></a>こちらもご覧ください
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
