---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 62be3ce13ecbc3180cf2bbcce26b04f3d79edb1a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731154"
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
