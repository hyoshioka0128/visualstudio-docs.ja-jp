---
description: セッションデバッグマネージャー (SDM) がプロセスをデタッチできるかどうかを決定します。
title: 'IDebugProcess2:: CanDetach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CanDetach
helpviewer_keywords:
- IDebugProcess2::CanDetach
ms.assetid: 2830f7c3-69fb-474a-97b8-5b869e38d546
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 92e876d5642cf8a4b7b60f5119839e64959f296e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151676"
---
# <a name="idebugprocess2candetach"></a>IDebugProcess2::CanDetach
セッションデバッグマネージャー (SDM) がプロセスをデタッチできるかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>戻り値
 成功した場合 `S_OK.` 、 `S_FALSE` デバッガーがプロセスからデタッチできない場合は、を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
