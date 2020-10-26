---
title: 'IDebugSymbolProvider:: Getアドレス Fromcontext |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ebd36bdda5059a4fd3c0334a5a2f222aaae40f01
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68206007"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、ドキュメントコンテキストをデバッグアドレスの配列にマップします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
#### <a name="parameters"></a>パラメーター  
 `pDocContext`  
 からドキュメントコンテキスト。  
  
 `fStatmentOnly`  
 からTRUE の場合、デバッグアドレスを1つのステートメントに限定します。  
  
 `ppEnumBegAddresses`  
 入出力このステートメントまたは行に関連付けられている開始デバッグアドレスの列挙子を返します。  
  
 `ppEnumEndAddresses`  
 入出力このステートメントまたは行に関連付けられている終了デバッグアドレスの [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md) 列挙子を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 ドキュメントコンテキストは、通常、ソース行の範囲を示します。 このメソッドは、これらの行に関連付けられているデバッグの開始アドレスと終了アドレスを提供します。 一部の言語では、複数の行にまたがるステートメントや、複数のステートメントを含む行が許可されます。 このメソッドには、デバッグアドレスを1つのステートメントに制限するフラグが用意されています。  
  
 テンプレートの場合のように、1つのステートメントに複数のデバッグアドレスを含めることができます。  
  
## <a name="see-also"></a>参照  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [Getアドレス Fromposition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)   
 [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
