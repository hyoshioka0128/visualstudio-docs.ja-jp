---
title: 'IDiaSymbol:: get_acceleratorPointerTags |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 30e13cee-e511-49ec-affd-99b0097071b2
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 829c7a0193ce2742959f677e95dd4a499997cf5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149838"
---
# <a name="idiasymbolget_acceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

C++ AMP accelerator スタブ関数に対応するすべてのアクセラレータポインタータグ値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT get_acceleratorPointerTags(   
   DWORD          cnt,  
   DWORD*         pcnt,  
   DWORD*         pPointerTags);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cnt`  
 から出力配列のサイズ `pPointerTags` 。  
  
 `pcnt`  
 入出力C++ AMP accelerator スタブ関数内のアクセラレータポインタータグの数。  
  
 `pPointerTags`  
 入出力 `DWORD` C++ AMP accelerator スタブ関数のアクセラレータポインターのタグ値を格納する配列ポインター。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは `IDiaSymbol` 、C++ AMP accelerator スタブ関数に対応するインターフェイスで呼び出されます。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
