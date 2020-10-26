---
title: CV_CFL_LANG |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_CFL_LANG enumeration
ms.assetid: 4e8e0613-ad02-4de9-9f46-e4753c5b0251
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9c1fabdb202d51b85eb2983360bdfd02757f7649
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699357"
---
# <a name="cv_cfl_lang"></a>CV_CFL_LANG
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

アプリケーションまたはリンクされたモジュールのソースコード言語を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef enum CV_CFL_LANG {   
   CV_CFL_C       = 0x00,  
   CV_CFL_CXX     = 0x01,  
   CV_CFL_FORTRAN = 0x02,  
   CV_CFL_MASM    = 0x03,  
   CV_CFL_PASCAL  = 0x04,  
   CV_CFL_BASIC   = 0x05,  
   CV_CFL_COBOL   = 0x06,  
   CV_CFL_LINK    = 0x07,  
   CV_CFL_CVTRES  = 0x08,  
   CV_CFL_CVTPGD  = 0x09,  
   CV_CFL_CSHARP  = 0x0A,  
   CV_CFL_VB      = 0x0B,  
   CV_CFL_ILASM   = 0x0C,  
   CV_CFL_JAVA    = 0x0D,  
   CV_CFL_JSCRIPT = 0x0E,  
   CV_CFL_MSIL    = 0x0F,  
   CV_CFL_HLSL    = 0x10  
} CV_CFL_LANG;  
```  
  
## <a name="elements"></a>要素  
 CV_CFL_C  
 アプリケーション言語は C です。  
  
 CV_CFL_CXX  
 アプリケーション言語は C++ です。  
  
 CV_CFL_FORTRAN  
 アプリケーション言語は FORTRAN です。  
  
 CV_CFL_MASM  
 アプリケーション言語は Microsoft マクロアセンブラーです。  
  
 CV_CFL_PASCAL  
 アプリケーション言語は Pascal 形式です。  
  
 CV_CFL_BASIC  
 アプリケーション言語が BASIC.  
  
 CV_CFL_COBOL  
 アプリケーション言語は COBOL です。  
  
 CV_CFL_LINK  
 アプリケーションは、リンカーによって生成されたモジュールです。  
  
 CV_CFL_CVTRES  
 アプリケーションは、CVTRES ツールを使用して変換されたリソースモジュールです。  
  
 CV_CFL_CVTPGD  
 アプリケーションは、CVTPGD ツールで生成された POGO 最適化モジュールです。  
  
 CV_CFL_CSHARP  
 アプリケーション言語は C# です。  
  
 CV_CFL_VB  
 アプリケーション言語が Visual Basic。  
  
 CV_CFL_ILASM  
 アプリケーション言語は、中間言語アセンブリ (つまり、共通言語ランタイム (CLR) アセンブリ) です。  
  
 CV_CFL_JAVA  
 アプリケーション言語は Java です。  
  
 CV_CFL_JSCRIPT  
 アプリケーション言語は Jscript です。  
  
 CV_CFL_MSIL  
 アプリケーション言語は、不明な Microsoft 中間言語 (MSIL) です。これは、 [/ltcg (リンク時のコード生成)](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2) スイッチを使用した結果である可能性があります。  
  
 CV_CFL_HLSL  
 アプリケーション言語は、高レベルのシェーダー言語です。  
  
## <a name="remarks"></a>解説  
 この列挙体の値は、 [IDiaSymbol:: get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md) メソッドへの呼び出しによって返されます。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)
