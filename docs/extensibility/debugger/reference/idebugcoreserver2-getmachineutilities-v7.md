---
description: このメソッドは、サーバーのマシンユーティリティを取得します。
title: 'IDebugCoreServer2:: GetMachineUtilities_V7 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bc58f41d9cca98f6c15c164ed4acb941345627e5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154770"
---
# <a name="idebugcoreserver2getmachineutilities_v7"></a>IDebugCoreServer2::GetMachineUtilities_V7
このメソッドは、サーバーのマシンユーティリティを取得します。

> [!NOTE]
> このメソッドは互換性のために残されています。使用しないでください ( [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] `E_NOTIMPL` このメソッドが呼び出された場合は、常にを返します)。 この情報は、履歴上の理由で保持されます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMachineUtilities_V7(
   IDebugMDMUtil2_V7** ppUtil
);
```

```csharp
int GetMachineUtilities_V7(
   out IDebugMDMUtil2_V7 ppUtil
);
```

## <a name="parameters"></a>パラメーター
`ppUtil`\
入出力 `IDebugMDMUtil2_V7` コンピューターユーティリティ情報を表すインターフェイスを返します。

## <a name="return-value"></a>戻り値
 は常にを返し `E_NOTIMPL` ます。これは、メソッドが実装されていないことを示します。

## <a name="remarks"></a>解説
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]`E_NOTIMPL`このメソッドが呼び出された場合は、常にを返します。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
