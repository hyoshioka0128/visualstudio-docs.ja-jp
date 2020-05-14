---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition method
ms.assetid: 1b0f02cb-8ace-4614-88f3-0e10239012b3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 27767af36093e9424775074a55bafadac9a4480d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719407"
---
# <a name="idebugsymbolprovidergetaddressesfromposition"></a>IDebugSymbolProvider::GetAddressesFromPosition
このメソッドは、ドキュメントの位置をデバッグ アドレスの配列にマップします。

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
[in]ドキュメントの位置。

`fStatmentOnly`\
[in]TRUE の場合、デバッグ アドレスは 1 つのステートメントに制限されます。

`ppEnumBegAddresses`\
[アウト]このステートメントまたは行に関連付けられている開始デバッグ アドレスの列挙子を返します。

`ppEnumEndAddresses`\
[アウト]このステートメントまたは[行に関連](../../../extensibility/debugger/reference/ienumdebugaddresses.md)付けられている終了デバッグ アドレスの列挙子を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ドキュメントの位置は、通常、ソース行の範囲を示します。 このメソッドは、これらの行に関連付けられた開始デバッグ アドレスと終了デバッグ アドレスを提供します。 言語によっては、複数行にまたがるステートメントや、複数のステートメントを含む行を使用できるものもあります。 このメソッドは、デバッグ アドレスを 1 つのステートメントに制限するフラグを提供します。

 テンプレートの場合のように、1 つのステートメントに複数のデバッグ アドレスを設定できます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
