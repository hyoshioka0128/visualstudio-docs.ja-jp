---
title: 'IDiaSymbol:: get_isDataAligned |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isDataAligned method
ms.assetid: ddd11a41-6c00-4829-acf4-aa1ace8c21a7
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 86c701765f9c8a67f7b95368d02febc1d254c696
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841869"
---
# <a name="idiasymbolget_isdataaligned"></a>IDiaSymbol::get_isDataAligned
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザー定義型 (UDT) が特定のメモリ境界に固定されているかどうかを指定するフラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT get_isDataAligned(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pFlag`  
 入出力 `TRUE` UDT が一部のメモリ境界に固定されている場合はを返します。それ以外の場合はを返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合 `S_FALSE` は、またはエラーコードを返します。  
  
> [!NOTE]
> の戻り値は、その `S_FALSE` シンボルに対してプロパティを使用できないことを意味します。  
  
## <a name="remarks"></a>注釈  
 このプロパティは、通常、既定以外のデータ配置で実行可能ファイルがコンパイルされるときに設定されます。 たとえば、Microsoft C++ コンパイラでは、コマンドラインオプションである/Zp を使用してデータの配置を変更できます <em>#</em> 。ここで、 *#* はバイト値です。  
  
## <a name="requirements"></a>要件  
  
|要件|説明|  
|-----------------|-----------------|  
|ヘッダー:|dia2|  
|バージョン:|DIA SDK v1.0|  
  
## <a name="see-also"></a>参照  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
