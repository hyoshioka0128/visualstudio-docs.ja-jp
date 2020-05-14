---
title: IDebugEngine2::保留中のブレークポイントを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f88cae3610487b92fed0d8390d44c55d3f536c4b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731120"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
デバッグ エンジン (DE) で保留中のブレークポイントを作成します。

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
[in]作成する保留中のブレークポイントを記述する[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)オブジェクト。

`ppPendingBP`\
[アウト]保留中の[ブレークポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)を表すオブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 通常、`E_FAIL`パラメータが`pBPRequest`無効か不完全な場合、パラメータが DE でサポート`pBPRequest`されている言語と一致しない場合に返されます。

## <a name="remarks"></a>Remarks
保留中のブレークポイントは、基本的には、ブレークポイントをコードにバインドするために必要なすべての情報のコレクションです。 このメソッドから返される保留中のブレークポイントは[、Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)メソッドが呼び出されるまでコードにバインドされません。

ユーザーが設定する保留中の各ブレークポイントについて、セッション デバッグ マネージャー (SDM) は、アタッチされた各 DE でこのメソッドを呼び出します。 DE は、その DE で実行されているプログラムに対してブレークポイントが有効であることを確認する必要があります。

ユーザーがコード行にブレークポイントを設定すると、DE は、このコードに対応するドキュメント内の最も近い行にブレークポイントを自由にバインドできます。 これにより、ユーザーは複数行ステートメントの最初の行にブレークポイントを設定できますが、最後の行 (すべてのコードがデバッグ情報に属性付けされている) にバインドできます。

## <a name="example"></a>例
次の例は、単純な`CProgram`オブジェクトに対してこのメソッドを実装する方法を示しています。 DE の実装は`IDebugEngine2::CreatePendingBreakpoint`、各プログラムのメソッドのこの実装にすべての呼び出しを転送できます。

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

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
