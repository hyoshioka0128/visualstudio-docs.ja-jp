---
description: このメソッドは、ドキュメントの位置をデバッグアドレスの配列にマップします。
title: 'IDebugSymbolProvider:: Getアドレス Fromposition |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition method
ms.assetid: 1b0f02cb-8ace-4614-88f3-0e10239012b3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d4437055ccd693b40fe4f1f7d6364d9601c827a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159680"
---
# <a name="idebugsymbolprovidergetaddressesfromposition"></a>IDebugSymbolProvider::GetAddressesFromPosition
このメソッドは、ドキュメントの位置をデバッグアドレスの配列にマップします。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAddressesFromPosition( 
   IDebugDocumentPosition2* pDocPos,
   BOOL                     fStatmentOnly,
   IEnumDebugAddresses**    ppEnumBegAddresses,
   IEnumDebugAddresses**    ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromPosition( 
   IDebugDocumentPosition2  pDocPos,
   bool                     fStatmentOnly,
   out IEnumDebugAddresses  ppEnumBegAddresses,
   out IEnumDebugAddresses  ppEnumEndAddresses
);
```

## <a name="parameters"></a>パラメーター
`pDocPos`\
からドキュメントの位置。

`fStatmentOnly`\
からTRUE の場合、デバッグアドレスを1つのステートメントに限定します。

`ppEnumBegAddresses`\
入出力このステートメントまたは行に関連付けられている開始デバッグアドレスの列挙子を返します。

`ppEnumEndAddresses`\
入出力このステートメントまたは行に関連付けられている終了デバッグアドレスの [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md) 列挙子を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 通常、ドキュメントの位置は、ソース行の範囲を示します。 このメソッドは、これらの行に関連付けられているデバッグの開始アドレスと終了アドレスを提供します。 一部の言語では、複数の行にまたがるステートメントや、複数のステートメントを含む行が許可されます。 このメソッドには、デバッグアドレスを1つのステートメントに制限するフラグが用意されています。

 テンプレートの場合のように、1つのステートメントに複数のデバッグアドレスを含めることができます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
