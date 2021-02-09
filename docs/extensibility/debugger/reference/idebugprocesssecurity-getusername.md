---
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
ms.openlocfilehash: 075cc96866a2b7b4a987c04c6cb78dcd22da2b50
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912026"
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
