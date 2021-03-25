---
description: 次にそのスレッドの1つが実行を試行したときに、プログラムの実行を停止するように要求します。
title: 'IDebugProgram2:: CauseBreak |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::CauseBreak
helpviewer_keywords:
- IDebugProgram2::CauseBreak
ms.assetid: 07d353fc-68ab-4297-a18f-3d3c7a80e121
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64ad2a22a06cc18595aabb37e3c244c7ea0c0be1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076161"
---
# <a name="idebugprogram2causebreak"></a>IDebugProgram2::CauseBreak
次にそのスレッドの1つが実行を試行したときに、プログラムの実行を停止するように要求します。

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

## <a name="remarks"></a>注釈
 このメソッドが呼び出された後、プログラムが次にコードを実行しようとすると、 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) イベントが送信されます。

 このメソッドは、プログラムが停止するのを待たずにすぐに制御を返すという点で非同期です。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
