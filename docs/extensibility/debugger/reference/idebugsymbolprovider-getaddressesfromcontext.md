---
title: コンテキストを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7cf7599cf0fc37c16467c29c2b432f1f58b172fe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719436"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
このメソッドは、ドキュメント コンテキストをデバッグ アドレスの配列にマップします。

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
[in]ドキュメントコンテキスト。

`fStatmentOnly`\
[in]TRUE の場合、デバッグ アドレスは 1 つのステートメントに制限されます。

`ppEnumBegAddresses`\
[アウト]このステートメントまたは行に関連付けられている開始デバッグ アドレスの列挙子を返します。

`ppEnumEndAddresses`\
[アウト]このステートメントまたは[行に関連](../../../extensibility/debugger/reference/ienumdebugaddresses.md)付けられている終了デバッグ アドレスの列挙子を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ドキュメント コンテキストは、通常、ソース行の範囲を示します。 このメソッドは、これらの行に関連付けられた開始デバッグ アドレスと終了デバッグ アドレスを提供します。 言語によっては、複数行にまたがるステートメントや、複数のステートメントを含む行を使用できるものもあります。 このメソッドは、デバッグ アドレスを 1 つのステートメントに制限するフラグを提供します。

 テンプレートの場合のように、1 つのステートメントに複数のデバッグ アドレスを設定できます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
