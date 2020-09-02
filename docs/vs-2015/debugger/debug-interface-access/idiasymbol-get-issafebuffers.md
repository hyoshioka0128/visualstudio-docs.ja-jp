---
title: 'IDiaSymbol:: get_isSafeBuffers |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSafeBuffers method
ms.assetid: f29e373d-e7bb-4181-ab9f-bf708d401d83
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 046744fda09f272ca80c2760e880dce23d45ae36
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65673758"
---
# <a name="idiasymbolget_issafebuffers"></a>IDiaSymbol::get_isSafeBuffers
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

セーフバッファーのプリプロセッサディレクティブを使用するかどうかを指定するフラグを取得します。 [Symtagenum 列挙型](../../debugger/debug-interface-access/symtagenum.md)がに設定されている場合は、を使用し `SymTagFunction` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_isSafeBuffers(   
   BOOL* pRetVal)  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力 `TRUE` ポインターがセーフバッファーにプリプロセッサディレクティブを使用している場合はを返します。それ以外の場合はを返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、 `S_FALSE` そのシンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia100.dll  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [strict_gs_check](https://msdn.microsoft.com/library/decfec81-c916-42e0-a07f-8cc26df6a7ce)
