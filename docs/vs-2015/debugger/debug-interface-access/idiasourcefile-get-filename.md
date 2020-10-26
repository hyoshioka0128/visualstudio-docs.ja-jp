---
title: 'IDiaSourceFile:: get_fileName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_fileName method
ms.assetid: a5cb8927-23c6-469e-8f78-f2787d85dba4
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 718b84720c3dbfc03552b6b64a95645e72951057
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68190653"
---
# <a name="idiasourcefileget_filename"></a>IDiaSourceFile::get_fileName
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソースファイル名を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_fileName (   
   BSTR* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力ソースファイル名を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
