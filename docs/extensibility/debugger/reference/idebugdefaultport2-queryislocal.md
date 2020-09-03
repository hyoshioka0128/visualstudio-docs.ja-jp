---
title: 'IDebugDefaultPort2:: QueryIsLocal |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::QueryIsLocal
helpviewer_keywords:
- IDebugDefaultPort2::QueryIsLocal
ms.assetid: 1a42e774-c6ed-419a-a0e3-cab5778652ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c06230f7bbd1825fe73a22f9b1fdc35aea35c499
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80732329"
---
# <a name="idebugdefaultport2queryislocal"></a>IDebugDefaultPort2::QueryIsLocal
このメソッドは、このポートがローカルコンピューター上にあるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryIsLocal(
   void
);
```

```csharp
int QueryIsLocal();
```

## <a name="return-value"></a>戻り値
 `S_OK`このポートがローカルの場合 (呼び出し元と同じコンピューター上にある場合)、または `S_FALSE` ポートが別のコンピューター上にある場合は、を返します。

## <a name="see-also"></a>関連項目
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
