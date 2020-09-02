---
title: IDebugEngine2::D estroyProgram |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce139dd22361d9914693cbe8ad723656ab7d4f26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731110"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
指定されたプログラムが atypically に終了したこと、および DE がプログラムへのすべての参照をクリーンアップしてプログラム破棄イベントを送信する必要があることをデバッグエンジン (DE) に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT DestroyProgram( 
   IDebugProgram2* pProgram
);
```

```cpp
int DestroyProgram( 
   IDebugProgram2 pProgram
);
```

## <a name="parameters"></a>パラメーター
`pProgram`\
からAtypically によって終了されたプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドが呼び出された後、DE は、 [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) イベントをセッションデバッグマネージャー (SDM) に返します。

 このメソッドは実装されていません (を返し `E_NOTIMPL` ます)。これは、デバッグ中のプログラムと同じプロセスで DE が実行された場合です。 このメソッドは、DE が SDM と同じプロセスで実行される場合にのみ実装されます。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
