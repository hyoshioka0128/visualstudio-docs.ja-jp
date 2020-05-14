---
title: サーバーフレンドリー名を取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerFriendlyName
helpviewer_keywords:
- IDebugCoreServer3::GetServerFriendlyName
ms.assetid: 7035b904-b3d7-4d9b-98d9-65714b8a8b9f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eec30783041a1240d8f85815c06f4ca60729a484
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732891"
---
# <a name="idebugcoreserver3getserverfriendlyname"></a>IDebugCoreServer3::GetServerFriendlyName
サーバーの表示名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServerFriendlyName(
   BSTR* pbstrName
);
```

```csharp
int GetServerFriendlyName(
   out string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
[アウト]サーバーのフレンドリ名を返します。

> [!NOTE]
> 呼び出し元は、文字列を解放する責任があります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ユーザーが起動したサーバーの場合、このメソッドによって返される名前はサーバーの完全名です。 自動起動サーバーの場合、名前はサーバーが実行されているマシンの名前です。

 マシン指向の名前の場合は、[メソッド](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [サーバー名を取得します。](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)
