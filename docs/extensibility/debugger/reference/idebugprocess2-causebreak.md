---
description: このプロセスでコードを実行している次のプログラムが停止し、IDebugBreakEvent2 イベントオブジェクトを送信することを要求します。
title: 'IDebugProcess2:: CauseBreak |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CauseBreak
helpviewer_keywords:
- IDebugProcess2::CauseBreak
ms.assetid: efda8865-2319-4d53-90bf-6d9d74cd5195
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28a4da4c0f7e4f8770478a47a73f7567506d5ae2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161399"
---
# <a name="idebugprocess2causebreak"></a>IDebugProcess2::CauseBreak
このプロセスでコードを実行している次のプログラムが停止し、 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) イベントオブジェクトを送信することを要求します。

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

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
