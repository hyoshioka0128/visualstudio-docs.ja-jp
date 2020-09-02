---
title: 'IDiaLoadCallback2:: RestrictDBGAccess |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictDBGAccess method
ms.assetid: 63b67a93-2910-4fff-aa70-6b2eaa08e5c8
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3c40aca343821f26213ee9e609a341918b9a7ba9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187320"
---
# <a name="idialoadcallback2restrictdbgaccess"></a>IDiaLoadCallback2::RestrictDBGAccess
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Dbg ファイルからデバッグ情報を検索できるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT RestrictDBGAccess();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 `S_OK`Dbg ファイルからデバッグ情報が検索されないようにする以外の戻り値。  
  
## <a name="see-also"></a>参照  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
