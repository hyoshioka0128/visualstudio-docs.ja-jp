---
title: 'IDiaSymbol:: get_liveRangeLength |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeLength
ms.assetid: ffcce3cc-085c-44eb-8145-46e3819c54f9
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 33f56615334b7d33516c6c967f165dac3942b5f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842125"
---
# <a name="idiasymbolget_liverangelength"></a>IDiaSymbol::get_liveRangeLength
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ローカルシンボルが有効なアドレス範囲の長さを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_liveRangeLength (   
   ULONGLONG* length  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `length`  
 入出力アドレス範囲の長さを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
> [!NOTE]
> 返されるエラーコードは、シンボルにライブ範囲情報が含まれていないことを意味します。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia100.dll  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
