---
title: 既定のポート 2::サーバーを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3dbe6d813b85865b0fdbc20296473684203a3f1e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732386"
---
# <a name="idebugdefaultport2getserver"></a>IDebugDefaultPort2::GetServer
このメソッドは、このポートがオンになっているサーバーへのインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServer(
   IDebugCoreServer3** ppServer
);
```

```csharp
int GetServer(
   out IDebugCoreServer3 ppServer
);
```

## <a name="parameters"></a>パラメーター
`ppServer`\
[アウト]インターフェイスを実装するオブジェクト[を](../../../extensibility/debugger/reference/idebugcoreserver3.md)返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)は、Visual Studio によって実装され、ポートが配置されているサーバーを表します。

## <a name="see-also"></a>関連項目
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
