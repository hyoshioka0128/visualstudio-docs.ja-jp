---
title: 'IDiaSymbol:: get_udtKind |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_udtKind method
ms.assetid: 4002f887-aea6-4475-b302-67c57079fe0a
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6fb58bec19460a78839ded86c9b7d194e838cb09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841853"
---
# <a name="idiasymbolget_udtkind"></a>IDiaSymbol::get_udtKind
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

さまざまなユーザー定義型 (UDT) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_udtKind (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力UDT の種類 (構造体、クラス、または共用体) を指定する [Udtkind 列挙](../../debugger/debug-interface-access/udtkind.md) 型の列挙体から値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、 `S_FALSE` そのシンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [UdtKind 列挙型](../../debugger/debug-interface-access/udtkind.md)
