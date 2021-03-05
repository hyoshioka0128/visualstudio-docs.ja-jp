---
description: このメソッドを使用すると、ユーザーが安全でないプロセスにアタッチする前に、ポート供給者が警告を表示できます。
title: 'IDebugProcessSecurity:: Querycansaf Elyattach |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::QueryCanSafelyAttach
ms.assetid: 63ec1ae8-27da-4574-aa15-1c986fe9fe58
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e6a586983d64e8be27b15a0514234d1a321e943
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166165"
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

## <a name="see-also"></a>関連項目
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
