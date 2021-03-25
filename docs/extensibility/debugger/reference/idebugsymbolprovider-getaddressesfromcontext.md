---
description: このメソッドは、ドキュメントコンテキストをデバッグアドレスの配列にマップします。
title: 'IDebugSymbolProvider:: Getアドレス Fromcontext |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e9748e2e2cf7f82724398afe25624f2d1762363c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087133"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
このメソッドは、ドキュメントコンテキストをデバッグアドレスの配列にマップします。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAddressesFromContext( 
   IDebugDocumentContext2* pDocContext,
   BOOL                    fStatmentOnly,
   IEnumDebugAddresses**   ppEnumBegAddresses,
   IEnumDebugAddresses**   ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromContext(
   IDebugDocumentContext2  pDocContext,
   bool                    fStatmentOnly,
   out IEnumDebugAddresses ppEnumBegAddresses,
   out IEnumDebugAddresses ppEnumEndAddresses
);
```

## <a name="parameters"></a>パラメーター
`pDocContext`\
からドキュメントコンテキスト。

`fStatmentOnly`\
からTRUE の場合、デバッグアドレスを1つのステートメントに限定します。

`ppEnumBegAddresses`\
入出力このステートメントまたは行に関連付けられている開始デバッグアドレスの列挙子を返します。

`ppEnumEndAddresses`\
入出力このステートメントまたは行に関連付けられている終了デバッグアドレスの [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md) 列挙子を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 ドキュメントコンテキストは、通常、ソース行の範囲を示します。 このメソッドは、これらの行に関連付けられているデバッグの開始アドレスと終了アドレスを提供します。 一部の言語では、複数の行にまたがるステートメントや、複数のステートメントを含む行が許可されます。 このメソッドには、デバッグアドレスを1つのステートメントに制限するフラグが用意されています。

 テンプレートの場合のように、1つのステートメントに複数のデバッグアドレスを含めることができます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
