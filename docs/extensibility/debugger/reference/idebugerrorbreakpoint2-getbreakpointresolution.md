---
description: エラーを説明するブレークポイントエラーの解決方法を取得します。
title: 'IDebugErrorBreakpoint2:: GetBreakpointResolution |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpoint2::GetBreakpointResolution
helpviewer_keywords:
- IDebugErrorBreakpoint2::GetBreakpointResolution
ms.assetid: 1c2324ed-2a11-4e63-8f3a-f420c7a4018b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b6d7aea0c0ff9cbacf4085203a8908d30628bacf
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153184"
---
# <a name="idebugerrorbreakpoint2getbreakpointresolution"></a>IDebugErrorBreakpoint2::GetBreakpointResolution
エラーを説明するブレークポイントエラーの解決方法を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBreakpointResolution( 
   IDebugErrorBreakpointResolution2** ppErrorResolution
);
```

```csharp
int GetBreakpointResolution( 
   out IDebugErrorBreakpointResolution2 ppErrorResolution
);
```

## <a name="parameters"></a>パラメーター
`ppErrorResolution`\
入出力エラーを説明する [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
