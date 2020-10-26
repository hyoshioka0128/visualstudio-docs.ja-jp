---
title: 'IDiaSectionContrib:: get_length |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_length method
ms.assetid: d0f6b9c7-90fc-4e3c-945a-b8f683a8f006
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a8ff6b4d35447125d5923bea1a0b2d2bb48dff79
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62421617"
---
# <a name="idiasectioncontribget_length"></a>IDiaSectionContrib::get_length
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

セクション内のバイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_length (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力セクション内のバイト数を返します。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`このプロパティがサポートされていない場合は、を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
