---
title: 'IDiaLoadCallback2:: RestrictReferencePathAccess |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictReferencePathAccess method
ms.assetid: e20cb45c-0360-4ff0-a92c-b1b6f76d6e85
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce0f2b896b60a13635818249e9faf552f3070828
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187308"
---
# <a name="idialoadcallback2restrictreferencepathaccess"></a>IDiaLoadCallback2::RestrictReferencePathAccess
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

.Exe ファイルが配置されているパスで .pdb ファイルを検索するかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT RestrictReferencePathAccess();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 `S_OK`.Exe ファイルが配置されているパスで .pdb ファイルを検索しないようにする以外のリターンコード。  
  
## <a name="see-also"></a>参照  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
