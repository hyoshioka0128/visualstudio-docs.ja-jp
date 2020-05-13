---
title: プログラム2::実行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f34ebea67ff95d1da6d777cdd828604f4a2f56e8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722987"
---
# <a name="idebugprogram2execute"></a>IDebugProgram2::Execute
停止状態からこのプログラムを実行し続けます。 以前の実行状態 (ステップなど) はクリアされ、プログラムの実行が再開されます。

> [!NOTE]
> このメソッドは非推奨とされます。 代わりに[Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)メソッドを使用してください。

## <a name="syntax"></a>構文

```cpp
HRESULT Execute(
   void
);
```

```csharp
int Execute();
```

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ユーザーが他のプログラムのスレッドで停止状態から実行を開始すると、このメソッドがこのプログラムで呼び出されます。 このメソッドは、ユーザーが IDE の **[デバッグ**] メニューから **[スタート**] コマンドを選択したときにも呼び出されます。 このメソッドの実装は、プログラムの現在のスレッドで[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)メソッドを呼び出すのと同じくらい簡単です。

> [!WARNING]
> この呼び出しを処理する間は、停止イベントまたは即時 (同期) イベントを[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に送信しないでください。それ以外の場合は、デバッガーがハングする可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
