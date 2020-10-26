---
title: 'IDiaLoadCallback:: RestrictRegistryAccess |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::RestrictRegistryAccess method
ms.assetid: de4760c3-a746-4bab-8065-1388fed31b67
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: edc1bc130f2e8320de0cbd0e0ac3f84dad71b903
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150612"
---
# <a name="idialoadcallbackrestrictregistryaccess"></a>IDiaLoadCallback::RestrictRegistryAccess
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボル検索パスを検索するためにレジストリクエリを使用できるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT RestrictRegistryAccess();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 以外のリターンコード `S_OK` は、シンボル検索パスのレジストリのクエリを実行できません。  
  
## <a name="see-also"></a>参照  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
