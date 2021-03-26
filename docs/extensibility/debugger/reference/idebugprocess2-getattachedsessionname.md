---
description: このプロセスをデバッグしているセッションの名前を取得します。
title: 'IDebugProcess2:: GetAttachedSessionName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetAttachedSessionName
helpviewer_keywords:
- IDebugProcess2::GetAttachedSessionName
ms.assetid: 7e5e116f-2c0c-4bc8-ad3f-e9fd2318a7e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 426904f777d65a25b92871767649cb26041e2af8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071546"
---
# <a name="idebugprocess2getattachedsessionname"></a>IDebugProcess2::GetAttachedSessionName
このプロセスをデバッグしているセッションの名前を取得します。 IDE では、特定のコンピューターで特定のプロセスをデバッグしているユーザーにこの情報を表示できます。

> [!NOTE]
> このメソッドは非推奨とされ、その実装は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="syntax"></a>構文

```
HRESULT GetAttachedSessionName(
   BSTR* pbstrSessionName
);
```

## <a name="parameters"></a>パラメーター
`pbstrSessionName`\

## <a name="return-value"></a>戻り値
 このメソッドは常にを返す必要があり `E_NOTIMPL` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
