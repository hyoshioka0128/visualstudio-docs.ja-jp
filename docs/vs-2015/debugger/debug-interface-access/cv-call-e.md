---
title: CV_call_e |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cd1ee4c024894e5752277a5000d37745c88c4ac6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841861"
---
# <a name="cv_call_e"></a>CV_call_e
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

関数の呼び出し規約を指定します。  
  
> [!NOTE]
> 最も一般的な列挙値のみがここに記載されています。 完全な列挙体は、cvconst .h ヘッダーファイルで使用できます。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
typedef enum CV_call_e {   
   CV_CALL_NEAR_C    = 0x00,  
   CV_CALL_NEAR_FAST = 0x04,  
   CV_CALL_NEAR_STD  = 0x07,  
   CV_CALL_NEAR_SYS  = 0x09,  
   CV_CALL_THISCALL  = 0x0b,  
   CV_CALL_CLRCALL   = 0x16  
} CV_call_e;  
```  
  
## <a name="elements"></a>要素  
 CV_CALL_NEAR_C  
 右端から左へのプッシュを使用して、関数呼び出し規約を指定します。 呼び出し元の関数は、スタックをクリアします。  
  
 CV_CALL_NEAR_FAST  
 関数呼び出し規約を指定します。これは、レジスタを使用した左から右へのプッシュを使用します。 呼び出された関数は、パラメーターバイトの合計を使用してスタックをクリアします。  
  
 CV_CALL_NEAR_STD  
 Near 標準呼び出し (右から左方向のプッシュ) を使用して、関数呼び出し規約を指定します。  
  
 CV_CALL_NEAR_SYS  
 Near システム呼び出しを使用して、関数呼び出し規約を指定します。  
  
 CV_CALL_THISCALL  
 `this`Call ( `this` レジスタで渡されたポインター) を使用して関数呼び出し規約を指定します。  
  
 CV_CALL_CLRCALL  
 共通言語ランタイム (CLR: Common Language Runtime) によって使用される関数呼び出し規約を指定します (マネージコードの呼び出し規約とも呼ばれます)。  
  
## <a name="remarks"></a>注釈  
 この列挙体の値は、 [IDiaSymbol:: get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md) メソッドへの呼び出しによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
