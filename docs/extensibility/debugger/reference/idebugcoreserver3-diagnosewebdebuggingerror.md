---
title: IDebugCoreServer3::D iagnoseWebDebuggingError |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
helpviewer_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
ms.assetid: 8c4570ca-ae55-42f2-bbaa-8d8e75d2fa19
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6c95c3953b70235daa739e48b5de50b4a815b13
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908057"
---
# <a name="idebugcoreserver3diagnosewebdebuggingerror"></a>IDebugCoreServer3::DiagnoseWebDebuggingError
自動アタッチに失敗した原因の特定を試みます。

## <a name="syntax"></a>構文

```cpp
HRESULT DiagnoseWebDebuggingError(
   LPCWSTR pszUrl
);
```

```csharp
int DiagnoseWebDebuggingError(
   string pszUrl
);
```

## <a name="parameters"></a>パラメーター
`pszUrl`\
から現在使用されていません。常に null 値に設定する必要があります。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 その他の一般的なリターンコードを次に示します。

|コード|説明|
|----------|-----------------|
|`S_WEBDBG_UNABLE_TO_DIAGNOSE`|リモートサーバーがデバッグを開始できなかった理由を特定できません。|
|`S_WEBDBG_DEBUG_VERB_BLOCKED`|リモートサーバーでデバッグできません。アクセス許可が不十分であるか、デバッグ動詞が有効になっていないことが原因である可能性があります。|
|`E_WEBDBG_DEBUG_VERB_BLOCKED`|Web サーバーがロックダウンされ、デバッグを有効にするために必要な DEBUG 動詞をブロックしています。|

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
