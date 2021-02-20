---
title: 'IEEDataStorage:: GetData |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c0ff27438ad4a7d0106c1b452f55966dda3f7e07
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965565"
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

## <a name="remarks"></a>解説
 このメソッドは、取得プロセスでバイトをスキップする方法がないため、すべてのデータバイトをローカル配列に取得することをお勧めします。 この場合、パラメーターは `dataSize` [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) メソッドによって返される値である必要があります。

## <a name="see-also"></a>関連項目
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
