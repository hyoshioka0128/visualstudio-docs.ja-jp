---
description: このメソッドは、ポート供給元がデバッガーの呼び出し間でポートを (ディスクに書き込むことによって) 永続化できるかどうかを決定します。
title: 'IDebugPortSupplier3:: CanPersistPorts |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 092f6e372d8f98e731ad90a7d261fe015d019656
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172010"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
このメソッドは、ポート供給元がデバッガーの呼び出し間でポートを (ディスクに書き込むことによって) 永続化できるかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanPersistPorts();
```

```csharp
int CanPersistPorts();
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 `S_OK` ポートを永続化できる場合は `S_FALSE` 。ポートを永続化できない場合は。

## <a name="remarks"></a>解説
 ポートの供給元がポートを永続化できる場合は、破棄されたときに、再度インスタンス化されたときに再読み込みする必要があります。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
