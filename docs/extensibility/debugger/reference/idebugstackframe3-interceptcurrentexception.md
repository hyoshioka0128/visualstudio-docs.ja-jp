---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7debd5323e753c6c5fd1476eac3c062fb63393b9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719481"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
現在の例外をインターセプトする場合に、現在のスタック フレーム上のデバッガーによって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT InterceptCurrentException(
   INTERCEPT_EXCEPTION_ACTION dwFlags,
   UINT64*                    pqwCookie
);
```

```csharp
int InterceptCurrentException(
   uint dwFlags,
   out  ulong pqwCookie
);
```

## <a name="parameters"></a>パラメーター
`dwFlags`\
[in]異なるアクションを指定します。 現在[、INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)値`IEA_INTERCEPT`のみがサポートされており、指定する必要があります。

`pqwCookie`\
[アウト]特定の例外を識別する一意の値。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

 最も一般的なエラーが返される例を次に示します。

|エラー|説明|
|-----------|-----------------|
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|現在の例外をインターセプトできません。|
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|現在の実行フレームでハンドラーが検索されていません。|
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|このメソッドは、このフレームではサポートされていません。|

## <a name="remarks"></a>Remarks
 例外がスローされると、デバッガーは例外処理プロセス中にキー ポイントでの実行時から制御を取得します。 これらの重要な瞬間に、デバッガーは、フレームが例外をインターセプトする場合は、現在のスタック フレームを確認できます。 このように、インターセプトされた例外は、スタック フレームに例外ハンドラー (たとえば、プログラム コードの try/catch ブロック) がない場合でも、基本的にはスタック フレームのオンザフライ例外ハンドラーです。

 デバッガーは、例外をインターセプトする必要があるかどうかを知りたい場合、現在のスタック フレーム オブジェクトでこのメソッドを呼び出します。 このメソッドは、例外のすべての詳細を処理します。 [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)インターフェイスが実装されていないか、メソッドが`InterceptStackException`エラーを返す場合、デバッガーは例外を通常どおり処理し続けます。

> [!NOTE]
> 例外はマネージ コード内でのみ受け取ることができます。 もちろん、サードパーティの言語実装者は、選択した`InterceptStackException`場合、独自のデバッグ エンジンで実装できます。

 インターセプトが完了すると[、IDebugインターセプト例外コンプリートイベント2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)が通知されます。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
