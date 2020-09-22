---
title: 'IDiaSymbol:: get_addressSection |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressSection method
ms.assetid: fe80d479-3bb5-4f55-9b62-1bd58d0a60ce
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 85e6ffac13f25e79f51af13ac134cf538e6af5af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841393"
---
# <a name="idiasymbolget_addresssection"></a>IDiaSymbol::get_addressSection
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

アドレスの場所のセクション部分を取得します。 [LocationType 列挙](../../debugger/debug-interface-access/locationtype.md)がに設定されている場合は、を使用し `LocIsStatic` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_addressSection (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力アドレスの場所のセクション部分を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 外部 DLL に配置されている静的メンバーの場合、このメソッドは、このメソッドによって返されるセクションを0にすることができます。このメソッドは、メンバーの仮想アドレスの取得に依存します。 仮想アドレスが有効なのは、 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)インターフェイスの[IDiaSession::p ut_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)メソッドが、DLL の読み込みアドレスを指定する0以外のパラメーターを使用して呼び出されている場合のみです。  
  
 アドレスのオフセット部分を取得するには、 [IDiaSymbol:: get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md) メソッドを呼び出します。  
  
## <a name="requirements"></a>要件  
  
|要件|説明|  
|-----------------|-----------------|  
|ヘッダー:|dia2|  
|バージョン:|DIA SDK v1.0|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
