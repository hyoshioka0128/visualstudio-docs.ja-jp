---
description: このエイリアスを削除の対象としてマークします。
title: IDebugAlias::D ispose |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: efca2b2bedc531fa241d8cfe6cfe8cd3527a7b40
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143923"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
このエイリアスを削除の対象としてマークします。

## <a name="syntax"></a>構文

```cpp
HRESULT Dispose();
```

```csharp
int Dispose();
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドが呼び出されると、別名は使用できなくなります。

## <a name="see-also"></a>関連項目
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
