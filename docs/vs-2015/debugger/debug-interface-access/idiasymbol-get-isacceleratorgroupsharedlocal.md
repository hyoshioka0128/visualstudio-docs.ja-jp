---
title: 'IDiaSymbol:: get_isAcceleratorGroupSharedLocal |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: 17a20542-5b45-478f-bb80-0d56031aadb5
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c2e975f75d25e64925c2566c1c311d942e9c3766
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180984"
---
# <a name="idiasymbolget_isacceleratorgroupsharedlocal"></a>IDiaSymbol::get_isAcceleratorGroupSharedLocal
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルが C++ AMP Accelerator 用にコンパイルされたコード内のグループ共有ローカル変数に対応するかどうかを示すフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT get_isAcceleratorGroupSharedLocal(   
   BOOL* pFlag);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pFlag`  
 入出力 `BOOL` C++ AMP Accelerator 用にコンパイルされたコード内のグループ共有ローカル変数にシンボルが対応するかどうかを示すへのポインター。 の場合 `TRUE` 、 `get_baseDataSlot` メソッドとメソッドを使用して、 `get_baseDataOffset` 変数のストレージの場所情報を取得できます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol:: get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)   
 [IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)
