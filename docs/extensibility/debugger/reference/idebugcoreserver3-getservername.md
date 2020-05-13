---
title: サーバー名を取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerName
helpviewer_keywords:
- IDebugCoreServer3::GetServerName
ms.assetid: 0fc3fcf5-d6a3-4a00-bf14-458b8645714e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf8233a4e2e37478a5818da2c27e498fcf954de9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732864"
---
# <a name="idebugcoreserver3getservername"></a>IDebugCoreServer3::GetServerName
サーバーの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServerName(
   BSTR* pbstrName
);
```

```csharp
int GetServerName(
   out string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
[アウト]サーバーの名前を返します。

> [!NOTE]
> 呼び出し元は、文字列を解放する責任があります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 フレンドリーなサーバー名を[取得するには、](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)
