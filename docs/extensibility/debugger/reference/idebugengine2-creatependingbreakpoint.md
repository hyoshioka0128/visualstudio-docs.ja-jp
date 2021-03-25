---
description: デバッグエンジン (DE) に保留中のブレークポイントを作成します。
title: 'IDebugEngine2:: CreatePendingBreakpoint ポイント |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa06a4c88afecfebbd0b1258d7f1830dfdaad5ac
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093874"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
デバッグエンジン (DE) に保留中のブレークポイントを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreatePendingBreakpoint(
    IDebugBreakpointRequest2*  pBPRequest,
    IDebugPendingBreakpoint2** ppPendingBP
);
```

```csharp
int CreatePendingBreakpoint(
    IDebugBreakpointRequest2     pBPRequest,
    out IDebugPendingBreakpoint2 ppPendingBP
);
```

## <a name="parameters"></a>パラメーター
`pBPRequest`\
から作成する保留中のブレークポイントを記述する [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) オブジェクト。

`ppPendingBP`\
入出力保留中のブレークポイントを表す [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 パラメーター `E_FAIL` `pBPRequest` `pBPRequest` が無効または不完全である場合、パラメーターがの DE でサポートされているどの言語とも一致しない場合、は通常、を返します。

## <a name="remarks"></a>注釈
保留中のブレークポイントは、基本的に、ブレークポイントをコードにバインドするために必要なすべての情報のコレクションです。 このメソッドから返された保留中のブレークポイントは、 [バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) メソッドが呼び出されるまでコードにバインドされません。

ユーザーが設定した保留中のブレークポイントごとに、セッションデバッグマネージャー (SDM) は、アタッチされた各 DE 内でこのメソッドを呼び出します。 その DE で実行されているプログラムに対してブレークポイントが有効であることを確認するのは、DE です。

ユーザーがコード行にブレークポイントを設定すると、このコードに対応するドキュメント内の最も近い行にブレークポイントが自由にバインドされます。 これにより、ユーザーは、複数行のステートメントの最初の行にブレークポイントを設定できますが、最後の行にバインドします (すべてのコードがデバッグ情報に含まれます)。

## <a name="example"></a>例
次の例は、単純なオブジェクトに対してこのメソッドを実装する方法を示して `CProgram` います。 の DE 実装では、 `IDebugEngine2::CreatePendingBreakpoint` 各プログラムでこのメソッドの実装に対するすべての呼び出しを転送できます。

```
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)
{
    // Create and initialize the CPendingBreakpoint object.
    CComObject<CPendingBreakpoint> *pPending;
    CComObject<CPendingBreakpoint>::CreateInstance(&pPending);
    pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);
    return pPending->QueryInterface(ppPendingBP);
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [束縛](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
