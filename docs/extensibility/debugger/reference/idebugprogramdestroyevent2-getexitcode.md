---
title: 'IDebugProgramDestroyEvent2:: GetExitCode |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramDestroyEvent2::GetExitCode
helpviewer_keywords:
- IDebugProgramDestroyEvent2::GetExitCode
ms.assetid: 7f540cf6-e2d1-42b0-913e-a26d654b7659
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cc887cdcd2975bdfb4042acb1831a7482baa52c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722599"
---
# <a name="idebugprogramdestroyevent2getexitcode"></a>IDebugProgramDestroyEvent2::GetExitCode
プログラムの終了コードを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExitCode( 
   DWORD* pdwExit
);
```

```csharp
int GetExitCode( 
   out uint pdwExit
);
```

## <a name="parameters"></a>パラメーター
`pdwExit`\
入出力プログラムの終了コードを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
