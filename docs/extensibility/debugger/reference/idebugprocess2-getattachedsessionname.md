---
title: Iデバッグプロセス2::取得添付セッション名 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b70fd48adacdbbf936c6997fc373ad4a8d7e696b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724072"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
このプロセスをデバッグしているセッションの名前を取得します。 IDE は、特定のコンピューターで特定のプロセスをデバッグしているユーザーにこの情報を表示できます。

> [!NOTE]
> このメソッドは非推奨となっており、その実装は常に`E_NOTIMPL`を返す必要があります。

## <a name="syntax"></a>構文

```
HRESULT GetAttachedSessionName(
   BSTR* pbstrSessionName
);
```

## <a name="parameters"></a>パラメーター
`pbstrSessionName`\

## <a name="return-value"></a>戻り値
 このメソッドは常に`E_NOTIMPL`を返す必要があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
