---
description: ポートの名前を取得します。
title: 'IDebugPortRequest2:: GetPortName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89bff19026a8bbdab72f1bec84c5feef0b37d8c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072235"
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
入出力ポートの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)インターフェイスは、通常、ポートへの接続を取得するために、デバッグパッケージ (クライアント) からポートサプライヤー (サーバー) に渡されます。 デバッグパッケージとポートサプライヤーは、どちらもポートの選択肢を認識しています。 単純な文字列でポートを記述できる場合、メソッドには `IDebugPortRequest2::GetPortName` 接続に必要な情報が含まれています。 それ以外の場合、クライアントは追加のインターフェイスを提供できます。これは、を使用してサーバーで取得でき `IDebugPortRequest2::QueryInterface` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
