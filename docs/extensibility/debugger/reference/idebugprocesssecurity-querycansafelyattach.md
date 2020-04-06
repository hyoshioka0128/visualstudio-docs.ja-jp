---
title: Iデバッグプロセスセキュリティ::クエリカンアイアアタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::QueryCanSafelyAttach
ms.assetid: 63ec1ae8-27da-4574-aa15-1c986fe9fe58
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e03ccbb7761802401239768c54f4ea5b36ab86bf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723198"
---
# <a name="idebugprocesssecurityquerycansafelyattach"></a>IDebugProcessSecurity::QueryCanSafelyAttach
このメソッドを使用すると、ポートの供給元は、ユーザーが安全でないプロセスにアタッチする前に警告を表示できます。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryCanSafelyAttach();
```

```csharp
int QueryCanSafelyAttach();
```

## <a name="return-value"></a>戻り値
 戻り値は次のとおりです。

- `S_OK`: プロセスへのアタッチは安全で、警告ダイアログボックスは表示されません。

- `S_FALSE`: アタッチはセキュリティ上の問題であり、警告が表示されるダイアログ ボックスが表示されます。

- `FAILURE`: プロセスへのアタッチが失敗します。

## <a name="see-also"></a>関連項目
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
