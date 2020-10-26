---
title: 'IDiaSession:: findChildren |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findChildren method
ms.assetid: 5d19046f-f668-4aa9-8788-95cda9a98997
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cf274bb0f572da11a9aa43248da7eaa72a2e73c3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150428"
---
# <a name="idiasessionfindchildren"></a>IDiaSession::findChildren
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

名前と記号の種類に一致する指定された親識別子のすべての子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findChildren (   
   IDiaSymbol*       parent,  
   SymTagEnum        symtag,  
   LPCOLESTR         name,  
   DWORD             compareFlags,  
   IDiaEnumSymbols** ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `parent`  
 から親を表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。 この親シンボルが関数、モジュール、またはブロックの場合、その構文の子がに返され `ppResult` ます。 親シンボルが型の場合は、その子クラスが返されます。 このパラメーターがの場合 `NULL` 、を `symtag` またはに設定する必要があります。これにより `SymTagExe` `SymTagNull` 、グローバルスコープ (.exe ファイル) が返されます。  
  
 `symtag`  
 から取得する子のシンボルタグを指定します。 値は [Symtagenum](../../debugger/debug-interface-access/symtagenum.md) 列挙型から取得されます。 すべての `SymTagNull` 子を取得するには、に設定します。  
  
 `name`  
 から取得する子の名前を指定します。 すべての子を取得するには、をに設定 `NULL` します。  
  
 `compareFlags`  
 から名前の一致に適用される比較オプションを指定します。 [Namesearchoptions 列挙](../../debugger/debug-interface-access/namesearchoptions.md)列挙の値は、単独で、または組み合わせて使用できます。  
  
 `ppResult`  
 入出力取得した子シンボルのリストを格納している [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="example"></a>例  
 次の例では、名前が一致する関数のローカル変数を検索する方法を示し `pFunc` `szVarName` ます。  
  
```cpp#  
IDiaEnumSymbols* pEnum;  
pSession->findChildren( pFunc, SymTagData, szVarName, nsCaseSensitive, &pEnum );  
```  
  
## <a name="see-also"></a>参照  
 [概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
