---
title: 'IDiaEnumLineNumbers:: Clone |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Clone method
ms.assetid: fcd2479a-8ff7-4aba-a737-06123c280d54
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 21b1a47f46765c9f7bf2d1832ff54bf50c5f59a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185491"
---
# <a name="idiaenumlinenumbersclone"></a>IDiaEnumLineNumbers::Clone
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在の列挙子と同じ列挙状態を含む列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Clone (   
   IDiaEnumLineNumbers** ppenum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppenum`  
 入出力列挙子の複製を含む [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) オブジェクトを返します。 行番号は重複しておらず、列挙子のみになります。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
