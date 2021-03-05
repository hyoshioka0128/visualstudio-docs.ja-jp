---
description: コアサーバーが実行されているコンピューターの説明を取得します。
title: 'IDebugCoreServer2:: GetMachineInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetInfo
helpviewer_keywords:
- IDebugCoreServer2::GetInfo
ms.assetid: 8fa1a1d3-9fcb-4fb3-bf4e-e7172ac08d77
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9fd7f42816ce477af4ae259adca49e8aac20137d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163214"
---
# <a name="idebugcoreserver2getmachineinfo"></a>IDebugCoreServer2::GetMachineInfo
コアサーバーが実行されているコンピューターの説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMachineInfo( 
   MACHINE_INFO_FIELDS Fields,
   MACHINE_INFO*       pMachineInfo
);
```

```csharp
int GetMachineInfo( 
   enum_ MACHINE_INFO_FIELDS  Fields,
   MACHINE_INFO[]             pMachineInfo
);
```

## <a name="parameters"></a>パラメーター
`Fields`\
からどのフィールドを入力するかを指定する、 [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md) 列挙のフラグの組み合わせ `pMachineInfo` 。

 `pMachineInfo`\

 [入力、出力]コンピューターの説明を入力した [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
