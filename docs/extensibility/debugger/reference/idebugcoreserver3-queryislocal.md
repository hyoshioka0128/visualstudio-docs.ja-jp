---
description: サーバーが呼び出し元に対してローカルかどうかを判断します。
title: 'IDebugCoreServer3:: QueryIsLocal |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::QueryIsLocal
helpviewer_keywords:
- IDebugCoreServer3::QueryIsLocal
ms.assetid: cca030de-f853-4ed7-b2fb-395f08a6b884
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e18074c92bdd63c1c378d71d3c84c4dde1745536
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054310"
---
# <a name="idebugcoreserver3queryislocal"></a>IDebugCoreServer3::QueryIsLocal
サーバーが呼び出し元に対してローカルかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryIsLocal(
   void
);
```

```csharp
int QueryIsLocal();
```

## <a name="return-value"></a>戻り値
 `S_OK`サーバーがローカルであることを示すには、を返します。 `S_FALSE`サーバーが msvsmon.exe のインスタンスから実行されている場合はを返します。これは通常、リモートデバッグに使用されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
