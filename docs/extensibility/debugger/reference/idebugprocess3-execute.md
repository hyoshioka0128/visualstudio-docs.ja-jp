---
title: Iデバッグプロセス3::実行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 444eadcce38adbd8ecd8655e8e0dc3f36f446848
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723686"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
停止状態からこのプロセスを実行し続けます。 以前の実行状態 (ステップなど) はクリアされ、プロセスは再度実行を開始します。

> [!NOTE]
> このメソッドは Execute[の代](../../../extensibility/debugger/reference/idebugprogram2-execute.md)わりに使用する必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT Execute(
   IDebugThread2* pThread
);
```

```csharp
int Execute(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[in]実行するスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ユーザーが、他のプロセスのスレッドで停止状態から実行を開始すると、このメソッドがこのプロセスで呼び出されます。 このメソッドは、ユーザーが IDE の **[デバッグ**] メニューから **[スタート**] コマンドを選択したときにも呼び出されます。 このメソッドの実装は、プロセスの現在のスレッドで[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)メソッドを呼び出すのと同じくらい簡単です。

> [!WARNING]
> この呼び出しを処理する間は、停止イベントまたは即時 (同期) イベントを[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合は、デバッガーがハングする可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
