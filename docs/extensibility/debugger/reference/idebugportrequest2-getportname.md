---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67121e98f2d506aa16c2b4dc3fff2ad5128fb93b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724815"
---
# <a name="idebugportrequest2getportname"></a>IDebugPortRequest2::GetPortName
ポートの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortName( 
   BSTR* pbstrPortName
);
```

```csharp
int GetPortName( 
   out string pbstrPortName
);
```

## <a name="parameters"></a>パラメーター
`pbstrPortName`\
[アウト]ポートの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)インターフェイスは、通常、ポートへの接続を取得するポートサプライヤー (サーバー) にデバッグ パッケージ (クライアント) から渡されます。 デバッグ パッケージとポート サプライヤーの両方が、ポートの選択肢を認識しています。 単純な文字列がポートを記述できる場合、`IDebugPortRequest2::GetPortName`メソッドには接続を確立するための十分な情報が含まれます。 それ以外の場合は、クライアントが追加のインターフェイスを提供できます`IDebugPortRequest2::QueryInterface`。

## <a name="see-also"></a>関連項目
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
