---
title: プログラムノード2::Dエタッハデバッガ_V7 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 925f1b07662ece35d21f9b647681bc898428c4c7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722114"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 廃止。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT DetachDebugger_V7 (
   void 
);
```

```csharp
int DetachDebugger_V7 ();
```

## <a name="return-value"></a>戻り値

実装は常に`E_NOTIMPL`を返す必要があります。

## <a name="remarks"></a>Remarks

> [!WARNING]
> Visual Studio 2005 以降では、このメソッドは使用されなくなり、`E_NOTIMPL`常に を返す必要があります。

このメソッドは、デバッガーが予期せず終了したときに呼び出されます。 このメソッドが呼び出されると、DE は、ユーザーがデタッチした場合と同様にプログラムを再開する必要があります。 これ以上デバッグ イベントを送信する必要はありません。 プログラムは、デバッガーの別のインスタンスからアタッチ可能な状態にする必要があります。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
