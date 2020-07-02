---
title: SetWefProcessId メソッド
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 13a6748e2e3b66f581a3c72c1f847e0329189e64
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537333"
---
# <a name="setwefprocessid-method"></a>SetWefProcessId メソッド
  Web Extensions Framework (WEF) コンテンツを実行するプロセス識別子を提供します。

## <a name="syntax"></a>構文

```csharp
HRESULT SetWefProcessId(
    [in] DWORD dwProcessId
);
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*dwProcessId*|WEF コンテンツを実行するために使用されるプロセス識別子。|

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>Remarks
 このメソッドは、WEF コンテンツプロセスを作成した後、WEF コンテンツを実行する前に呼び出す必要があります。

 開発環境で、WEF コンテンツプロセスにデバッガーをアタッチする場合は、このメソッドの実装でこの操作を実行する必要があります。
