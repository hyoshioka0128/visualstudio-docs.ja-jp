---
title: 'IDiaSession:: findAcceleratorInlineesByName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: e203e5c2-6563-43fa-be56-3063955043ab
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 47883395ec12cac60d3a21651432f5ac21cc64a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151753"
---
# <a name="idiasessionfindacceleratorinlineesbyname"></a>IDiaSession::findAcceleratorInlineesByName
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定されたインライン関数名に対応するインラインフレームのシンボルの列挙体を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT findAcceleratorInlineeLinesByName (   
   LPCOLESTR             name,  
   DWORD                 option,  
   IDiaEnumSymbols**     ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `name`  
 から検索するインライン関数の名前。  
  
 `option`  
 からに対応するインラインフレームを検索するときに使用する名前検索オプション `name` 。 詳細については、「 [Namesearchoptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)」を参照してください。  
  
 `ppResult`  
 入出力結果を使用し `IDiaEnumSymbols` て初期化されるインターフェイスポインターへのポインター。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 この関数は、アクセラレータスタブ関数内でのみインラインを検索します。 これは、ネイティブ C++ プロシージャレコードを無視します。  
  
## <a name="see-also"></a>参照  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
