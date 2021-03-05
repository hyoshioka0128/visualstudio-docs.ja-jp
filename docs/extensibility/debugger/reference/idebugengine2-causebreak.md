---
description: は、このデバッグエンジン (DE) によってデバッグされているすべてのプログラムが、次にそのスレッドの実行を試行したときに実行を停止することを要求します。
title: 'IDebugEngine2:: CauseBreak |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CauseBreak
helpviewer_keywords:
- IDebugEngine2::CauseBreak
ms.assetid: 17fe4698-b04e-4798-8412-80e0da60c387
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 344ca2e9e9758aaca5a2c1e6784a36467abde73c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162707"
---
# <a name="idebugengine2causebreak"></a>IDebugEngine2::CauseBreak
は、このデバッグエンジン (DE) によってデバッグされているすべてのプログラムが、次にそのスレッドの実行を試行したときに実行を停止することを要求します。

## <a name="syntax"></a>構文

```cpp
HRESULT CauseBreak( 
   void 
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは非同期です。 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) イベントは、このメソッドが呼び出された後にプログラムが次に実行を試行したときに送信されます。

## <a name="see-also"></a>関連項目
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
