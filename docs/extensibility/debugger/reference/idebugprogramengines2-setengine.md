---
description: プログラムまたはプログラムノードに、このプログラムをデバッグするために使用するデバッグエンジン (DE) を指示します。
title: 'IDebugProgramEngines2:: SetEngine |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::SetEngine
helpviewer_keywords:
- IDebugProgramEngines2::SetEngine
ms.assetid: c05857ee-89cf-455e-8f1e-300cce4a2eab
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17e990731059d4cee6e5f716c74edf93e13b87fb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161412"
---
# <a name="idebugprogramengines2setengine"></a>IDebugProgramEngines2::SetEngine
プログラムまたはプログラムノードに、このプログラムをデバッグするために使用するデバッグエンジン (DE) を指示します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetEngine( 
   REFGUID guidEngine
);
```

```csharp
int SetEngine( 
   ref Guid guidEngine
);
```

## <a name="parameters"></a>パラメーター
`guidEngine`\
からDE の GUID。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
