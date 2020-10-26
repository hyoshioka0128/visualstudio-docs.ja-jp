---
title: 'IDiaTable:: get__NewEnum |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::get__NewEnum method
ms.assetid: ee89bba8-5d5c-4a0b-aa0d-1aad56baa380
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3683f646698909150fadb0c9e520f339ce7e50b4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155447"
---
# <a name="idiatableget__newenum"></a>IDiaTable::get__NewEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

<xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT>この列挙子のバージョンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get__NewEnum (   
   IUnknown** pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力 `IUnknown` <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> この列挙子のバージョンを表すインターフェイスを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
