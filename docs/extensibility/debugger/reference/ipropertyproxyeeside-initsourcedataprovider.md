---
description: このオブジェクトのソースデータを初期化し、初期データを格納しているオブジェクトを返します。
title: 'IPropertyProxyEESide:: InitSourceDataProvider |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
helpviewer_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
ms.assetid: 5156f593-5052-4e3a-9d02-081916fb342d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd1040c6269b9d394e6f0968f595c71cf1576135
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224123"
---
# <a name="ipropertyproxyeesideinitsourcedataprovider"></a>IPropertyProxyEESide::InitSourceDataProvider
このオブジェクトのソースデータを初期化し、初期データを格納しているオブジェクトを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT InitSourceDataProvider(
   IEEDataStorage** dataOut
);
```

```csharp
int InitSourceDataProvider(
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataOut`\
入出力 [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、オブジェクトのデータに対して [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスを返すことができるように、オブジェクトを初期化するために必要なものをすべて実行します。 これにより、オブジェクトのデータを表示したり、許可されている場合は型ビジュアライザーによって変更したりできます。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
