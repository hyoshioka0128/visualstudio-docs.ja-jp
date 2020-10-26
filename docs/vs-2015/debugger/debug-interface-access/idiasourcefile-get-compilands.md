---
title: 'IDiaSourceFile:: get_compilands |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_compilands method
ms.assetid: 57deb50a-9c22-43ea-a80c-eab205997bc4
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9502a43b02091e3109b84c22dfe99d7aa174647a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190685"
---
# <a name="idiasourcefileget_compilands"></a>IDiaSourceFile::get_compilands
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このファイルを参照している行番号を持つ compilands の列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_compilands (   
   IDiaEnumSymbols** ppRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppRetVal`  
 入出力このファイルを参照している行番号を持つすべての compilands の一覧を含む [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
