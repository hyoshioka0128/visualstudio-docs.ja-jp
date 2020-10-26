---
title: 'IDiaSession:: symsAreEquiv |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ba8c77d7d97da75ce82fcbe732db64acf633b8af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150213"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

2つの記号が等しいかどうかを確認します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT symsAreEquiv (   
   IDiaSymbol* symbolA,  
   IDiaSymbol* symbolB  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `symbolA`  
 から比較で使用される最初の [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクト。  
  
 `symbolB`  
 から `IDiaSymbol` 比較で使用する2番目のオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 シンボルが等しい場合は、を返し `S_OK` ます。それ以外の場合はを返します `S_FALSE` 。シンボルは等価ではありません。 それ以外の場合は、エラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
