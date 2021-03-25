---
description: このメソッドは、プログラムからエイリアスの一覧を取得します。
title: 'IDebugBinder3:: GetAllAliases |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetAllAliases
helpviewer_keywords:
- IDebugBinder3::GetAllAliases method
ms.assetid: 1f9ab2ee-2ab3-4a61-8b99-95dd7fdf3511
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04e4f9887ff8cfa68ad4fd4b09d160e3ec2d1eaf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085170"
---
# <a name="idebugbinder3getallaliases"></a>IDebugBinder3::GetAllAliases
このメソッドは、プログラムからエイリアスの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAllAliases(
   UINT          uRequest,
   IDebugAlias** ppAliases,
   UINT*         puFetched
);
```

```csharp
int GetAllAliases(
   uint          uRequest,
   IDebugAlias[] ppAliases,
   out uint      puFetched
);
```

## <a name="parameters"></a>パラメーター
`uRequest`\
から返されるエイリアスの最大数 (に渡される配列の長さを指定し `ppAliases` ます)。

`ppAliases`\
[入力、出力]エイリアスを格納する配列 (これが null 値で、 `uRequest` が0の場合、返される可能性がある別名の数はによって返され `puFetched` ます)。

`puFetched`\
入出力取得されたエイリアスの数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
