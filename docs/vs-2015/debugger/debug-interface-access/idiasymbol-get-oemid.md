---
title: IDiaSymbol::get_oemId | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_oemId method
ms.assetid: c472830f-c3eb-46ab-9498-cd637763d241
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 406645893803094ce0ebdd4679d9809d7645401f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841632"
---
# <a name="idiasymbolget_oemid"></a>IDiaSymbol::get_oemId
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルの相手先ブランド供給 (OEM) ID 値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_oemId (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力OEM を識別する一意の値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 このプロパティは、 [Symtagenum 列挙](../../debugger/debug-interface-access/symtagenum.md) 型がのシンボルにのみ適用さ `SymTagCustomType` れます。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
