---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e96db32d7ba5a01f89530623c949500a265cdb60
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723100"
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
