---
description: ポートサプライヤーからユーザー名を取得します。
title: 'IDebugProcessSecurity:: GetUserName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04ad8bf6ba572a1f9e14e26ef2ca37d021f6e3a0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166204"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
ポートサプライヤーからユーザー名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetUserName(
    BSTR *pbstrUserName
);
```

```csharp
int GetUserName (
    string pbstrUserName
);
```

## <a name="parameters"></a>パラメーター
`pbstrUserName`\
入出力ユーザー名を表す文字列です。

## <a name="return-value"></a>戻り値
 メソッドが成功した場合は `S_OK` を返します。 それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 `GetUserName`[**プロセスにアタッチ**] ダイアログボックスの [**ユーザー名**] 列に表示されるユーザー名を返します。 [**プロセスにアタッチ**] ダイアログボックスを表示するには、統合開発環境 (IDE) の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックし [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="see-also"></a>関連項目
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
