---
title: 'IDiaSectionContrib:: get_read |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_read method
ms.assetid: 68bfb35c-eabd-412a-bc8f-3094703b98c4
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c06a618d0278d6a02409c33a73cd179f3b228e7a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150509"
---
# <a name="idiasectioncontribget_read"></a>IDiaSectionContrib::get_read
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

セクションを読み取ることができるかどうかを示すフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_read (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力 `TRUE` セクションを読み取ることができる場合はを返します。それ以外の場合はを返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`このプロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
