---
title: CONNECTION_PROTOCOL |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONNECTION_PROTOCOL
helpviewer_keywords:
- CONNECTION_PROTOCOL enumeration
ms.assetid: 99df5865-8b36-486d-9f4c-d10ae2bc688a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29ac287462149a20f52a1affdeab7fa6b8333711
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737649"
---
# <a name="connection_protocol"></a>CONNECTION_PROTOCOL
デバッグ サーバーとデバッグ パッケージ (DE) の間の通信に使用されているプロトコルを示します。

## <a name="syntax"></a>構文

```cpp
typedef enum tagCONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
} CONNECTION_PROTOCOL;
```

```csharp
public enum CONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
};
```

## <a name="fields"></a>フィールド
`CONNECTION_NONE`\
サーバーへの接続が確立されていません。

`CONNECTION_UNKNOWN`\
接続が確立されましたが、不明な種類です。

`CONNECTION_LOCAL`\
ローカル サーバーへの接続です。

`CONNECTION_PIPE`\
名前付きパイプを介した接続。

`CONNECTION_TCPIP`\
接続では TCP/IP を使用します。

`CONNECTION_HTTP`\
接続では HTTP (Web サーバー経由) が使用されます。

`CONNECTION_OTHER`\
他の種類の接続が確立されています (この値は現在使用されていません)。

## <a name="remarks"></a>Remarks
これらの値は、[メソッド](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)から返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
