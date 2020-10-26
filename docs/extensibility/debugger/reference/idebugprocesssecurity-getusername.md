---
title: 'IDebugProcessSecurity:: GetUserName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef00a0b7489c3e5cb709520546f3d3f26c8a4eba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723251"
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
