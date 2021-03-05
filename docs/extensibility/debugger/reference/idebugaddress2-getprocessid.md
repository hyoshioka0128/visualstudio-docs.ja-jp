---
description: この IDebugAddress2 インターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。
title: 'IDebugAddress2:: GetProcessID |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2::GetProcessID
helpviewer_keywords:
- IDebugAddress2::GetProcessID method
ms.assetid: 2c18889d-074a-4b95-87b4-bf1a067f44ed
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eeae55e91df8dac3fb176952a352df642facb055
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154952"
---
# <a name="idebugaddress2getprocessid"></a>IDebugAddress2::GetProcessID
この [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md) インターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProcessID (
   DWORD* pProcID
);
```

```csharp
int GetProcessID (
   out uint pProcID
);
```

## <a name="parameters"></a>パラメーター
`pProcID`\
入出力プロセス ID。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)
