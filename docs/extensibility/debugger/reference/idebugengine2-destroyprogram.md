---
title: IDebugEngine2::Dエストロイプログラム |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731110"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
指定されたプログラムが異常終了し、DE がプログラムへのすべての参照をクリーンアップし、プログラム破棄イベントを送信する必要があることをデバッグ エンジン (DE) に通知します。

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
[in]非定型終了されたプログラムを表す[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドが呼び出された後、DE は、その後、セッション デバッグ マネージャー (SDM) に[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)イベントを送信します。

 DE がデバッグ中のプログラムと`E_NOTIMPL`同じプロセスで実行されている場合、このメソッドは実装されません (戻り値)。 このメソッドは、DE が SDM と同じプロセスで実行される場合にのみ実装されます。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
