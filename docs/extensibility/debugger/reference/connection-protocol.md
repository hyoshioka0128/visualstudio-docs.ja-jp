---
title: CONNECTION_PROTOCOL |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737649"
---
# <a name="connection_protocol"></a>CONNECTION_PROTOCOL
デバッグサーバーとデバッグパッケージ (DE) 間の通信に使用されるプロトコルを示します。

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
接続が確立されましたが、これは不明な種類です。

`CONNECTION_LOCAL`\
ローカルサーバーへの接続です。

`CONNECTION_PIPE`\
接続は名前付きパイプを介して行われます。

`CONNECTION_TCPIP`\
接続は TCP/IP を使用します。

`CONNECTION_HTTP`\
接続は HTTP (Web サーバー経由) を使用します。

`CONNECTION_OTHER`\
他の種類の接続が確立されています (この値は現在使用されていません)。

## <a name="remarks"></a>解説
これらの値は、 [Getconnectionprotocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md) メソッドから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
