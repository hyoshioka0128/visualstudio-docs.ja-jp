---
description: メソッド内の指定されたデバッグアドレスの後に続くデバッグアドレスを取得します。
title: 'IDebugSymbolProvider:: GetNextAddress |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetNextAddress
helpviewer_keywords:
- IDebugSymbolProvider::GetNextAddress method
ms.assetid: 704eeb94-cb13-49d1-82b6-7d83ed0f19c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc269dcfc472c2f8bb3e5a9ed9a91ecd25292870
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075576"
---
# <a name="idebugsymbolprovidergetnextaddress"></a>IDebugSymbolProvider::GetNextAddress
メソッド内の指定されたデバッグアドレスの後に続くデバッグアドレスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetNextAddress( 
   IDebugAddress*  pAddress,
   BOOL            fStatementOnly,
   IDebugAddress** ppAddress
);
```

```csharp
int GetNextAddress( 
   IDebugAddress     pAddress,
   bool              fStatementOnly,
   out IDebugAddress ppAddress
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
から指定されたデバッグアドレス。

`fStatementOnly`\
からTRUE の場合、デバッグアドレスを1つのステートメントに限定します。

`ppAddress`\
入出力次のデバッグアドレスを返します。

## <a name="return-value"></a>戻り値
 は、有効な (通常は S_OK) を返し `HRESULT` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
