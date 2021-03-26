---
description: このオブジェクトに格納されているバイト数を返します。
title: 'IEEDataStorage:: GetSize |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetSize
helpviewer_keywords:
- IEEDataStorage::GetSize
ms.assetid: 33d232c4-1239-4abc-922b-e1bc5b908169
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 632d2adeaca976d0bb3fdfbe1b88571e337e02dd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083532"
---
# <a name="ieedatastoragegetsize"></a>IEEDataStorage::GetSize
このオブジェクトに格納されているバイト数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize(
   ULONG* size
);
```

```csharp
int GetSize(
   out uint size
);
```

## <a name="parameters"></a>パラメーター
`size`\
入出力このオブジェクトに格納されているバイト数。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 実際のデータバイトを取得するには、 [GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md) メソッドを使用します。

## <a name="see-also"></a>こちらもご覧ください
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)
