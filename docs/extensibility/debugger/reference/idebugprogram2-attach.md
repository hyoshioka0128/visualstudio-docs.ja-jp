---
title: Iデバッグプログラム2::アタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Attach
helpviewer_keywords:
- IDebugProgram2::Attach
ms.assetid: de069fbf-a565-4905-b102-f5658c55aacd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7d0b182ba7a873816e3a7aa32d39beb2c63cc5ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723137"
---
# <a name="idebugprogram2attach"></a>IDebugProgram2::Attach
プログラムにアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
[in]デバッグ イベント通知に使用する[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 次の表に、考えられるエラー コードを示します。

|[値]|説明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定されたプログラムは既にデバッガにアタッチされています。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|アタッチ処理中にセキュリティ違反が発生しました。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|デスクトップ プログラムをデバッガにアタッチすることはできません。|

## <a name="remarks"></a>Remarks
 デバッグ エンジン (DE) は、プログラムにアタッチするには、このメソッドを呼び出すことはありません。 DE がプログラムのアドレス空間で実行されている場合[、OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドが呼び出されます。 DE がセッション デバッグ マネージャー (SDM) アドレス空間で実行されている場合、[アタッチ](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドが呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
