---
description: ポートサプライヤーからユーザー名を取得します。
title: 'IDebugProcessSecurity:: GetUserName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 42a13075b233d5b0fe70b314a4b2d025a2a4c7d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076304"
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

## <a name="remarks"></a>注釈
 `GetUserName`[**プロセスにアタッチ**] ダイアログボックスの [**ユーザー名**] 列に表示されるユーザー名を返します。 [**プロセスにアタッチ**] ダイアログボックスを表示するには、統合開発環境 (IDE) の [**ツール**] メニューの [**プロセスにアタッチ**] をクリックし [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
