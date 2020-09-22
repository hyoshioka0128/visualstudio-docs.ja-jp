---
title: 'IDiaSymbol:: get_packed |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_packed method
ms.assetid: e42ff368-56c4-49a2-8676-f80e349efa21
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 90351c3319f8354685ae0d907379b8446f76cb7f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842097"
---
# <a name="idiasymbolget_packed"></a>IDiaSymbol::get_packed
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザー定義データ型 (UDT) がパックされているかどうかを指定するフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_packed (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力 `TRUE` UDT がパックされている場合はを返します。それ以外の場合はを返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 [パック済み] は、UDT のすべてのメンバーができるだけ近い場所に配置されることを意味し、メモリ境界に合わせて埋め込みは行われません。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
