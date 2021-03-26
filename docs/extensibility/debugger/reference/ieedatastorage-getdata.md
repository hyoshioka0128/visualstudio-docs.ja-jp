---
description: オブジェクトから指定されたバイト数を取得します。
title: 'IEEDataStorage:: GetData |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 218ffea2d35f34768550938e8bdc4c087bb3a2cf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083545"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
オブジェクトから指定されたバイト数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetData(
   ULONG  dataSize,
   ULONG* sizeGotten,
   BYTE*  data
);
```

```csharp
int GetData(
   uint     dataSize,
   out uint sizeGotten,
   byte[]   data
);
```

## <a name="parameters"></a>パラメーター
`dataSize`\
から取得するバイト数。配列は、 `data` 少なくともこのバイト数を保持する必要があります。

`sizeGotten`\
入出力実際に取得されたバイト数を返します。

`data`\
[入力、出力]要求されたデータを格納する配列。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、取得プロセスでバイトをスキップする方法がないため、すべてのデータバイトをローカル配列に取得することをお勧めします。 この場合、パラメーターは `dataSize` [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) メソッドによって返される値である必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
