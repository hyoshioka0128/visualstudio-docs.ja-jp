---
title: 'IDiaSymbol:: get_baseType |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_baseType method
ms.assetid: 5c69a241-a8d3-48ed-8b36-27463a196572
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: df922cbbe1c065f4df79fa62b7b4b0213dd7f487
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841809"
---
# <a name="idiasymbolget_basetype"></a>IDiaSymbol::get_baseType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このシンボルの基本型を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_baseType (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力シンボルの基本型を指定する [Basictype 列挙](../../debugger/debug-interface-access/basictype.md) 型の値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 シンボルの基本型を決定するには、最初にシンボルの型を取得し、次に基本型に対して返された型を問い合わせるします。 一部のシンボルには、構造体の名前など、基本型を使用できない場合があることに注意してください。  
  
## <a name="example"></a>例  
  
```cpp#  
IDiaSymbol* pType;  
CComPtr<IDiaSymbol> pBaseType;  
if (pType->get_type( &pBaseType ) == S_OK)  
{  
    BasicType btBaseType;  
    if (pBaseType->get_baseType((DWORD *)&btBaseType) == S_OK)  
    {  
        // Do something with basic type.  
    }  
}  
```  
  
## <a name="requirements"></a>要件  
  
|要件|説明|  
|-----------------|-----------------|  
|ヘッダー:|dia2|  
|バージョン:|DIA SDK v1.0|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [BasicType 列挙型](../../debugger/debug-interface-access/basictype.md)   
 [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
