---
description: サーバーのフレンドリ名を取得します。
title: 'IDebugCoreServer3:: GetServerFriendlyName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerFriendlyName
helpviewer_keywords:
- IDebugCoreServer3::GetServerFriendlyName
ms.assetid: 7035b904-b3d7-4d9b-98d9-65714b8a8b9f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72e281c6e40f8aea558ef600b531e59a3b26a5c3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094134"
---
# <a name="idebugcoreserver3getserverfriendlyname"></a>IDebugCoreServer3::GetServerFriendlyName
サーバーのフレンドリ名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServerFriendlyName(
   BSTR* pbstrName
);
```

```csharp
int GetServerFriendlyName(
   out string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
入出力サーバーのフレンドリ名を返します。

> [!NOTE]
> 呼び出し元は、文字列を解放する必要があります。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 ユーザーが起動したサーバーの場合、このメソッドによって返される名前はサーバーの完全な名前になります。 自動起動サーバーの場合は、サーバーが実行されているコンピューターの名前です。

 コンピューター指向の名前の場合は、 [Getservername](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md) メソッドを呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)
