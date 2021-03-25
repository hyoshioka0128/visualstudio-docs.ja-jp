---
description: このメソッドを使用すると、ユーザーが安全でないプロセスにアタッチする前に、ポート供給者が警告を表示できます。
title: 'IDebugProcessSecurity:: Querycansaf Elyattach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::QueryCanSafelyAttach
ms.assetid: 63ec1ae8-27da-4574-aa15-1c986fe9fe58
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cbbfcf11a35fcfc43ae9e903b13a7480a3cf9743
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076278"
---
# <a name="idebugprocesssecurityquerycansafelyattach"></a>IDebugProcessSecurity::QueryCanSafelyAttach
このメソッドを使用すると、ユーザーが安全でないプロセスにアタッチする前に、ポート供給者が警告を表示できます。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryCanSafelyAttach();
```

```csharp
int QueryCanSafelyAttach();
```

## <a name="return-value"></a>戻り値
 戻り値は次のとおりです。

- `S_OK`: プロセスへのアタッチは安全であり、警告ダイアログボックスは表示されません。

- `S_FALSE`: アタッチがセキュリティ上の問題であり、警告が表示されたダイアログボックスが表示される場合があります。

- `FAILURE`: プロセスにアタッチできません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
