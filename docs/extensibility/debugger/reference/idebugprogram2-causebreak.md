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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef10a714b6e65b40edb83cb0547ae1a28720d328
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166035"
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

## <a name="remarks"></a>解説
 このメソッドが呼び出された後、プログラムが次にコードを実行しようとすると、 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) イベントが送信されます。

 このメソッドは、プログラムが停止するのを待たずにすぐに制御を返すという点で非同期です。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
