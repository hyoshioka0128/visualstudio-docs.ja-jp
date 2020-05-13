---
title: データストレージ::取得データ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 62a1295aeb2a6afad51dee0f1015e3ab01d13fbb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718214"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
オブジェクトから指定したバイト数を取得します。

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
[in]取得するバイト数 (配列は`data`少なくともこのバイト数を保持する必要があります)。

`sizeGotten`\
[アウト]実際に取得されたバイト数を返します。

`data`\
[イン、アウト]要求されたデータを入力する配列。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドの推奨用途は、取得プロセスでバイトをスキップする方法がないため、すべてのデータバイトをローカル配列に取得することです。 この場合、パラメーター`dataSize`は[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)メソッドによって返される値である必要があります。

## <a name="see-also"></a>関連項目
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
