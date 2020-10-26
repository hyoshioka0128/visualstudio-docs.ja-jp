---
title: 構造体とクラスに注釈を付ける |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Field_size_bytes_part_
- _Field_size_bytes_full_opt_
- _Field_size_bytes_
- _Field_size_opt_
- _Field_size_part_
- _Field_size_bytes_part_opt_
- _Field_range_
- _Field_size_part_opt_
- _Field_size_
- _Field_size_bytes_opt_
- _Struct_size_bytes_
- _Field_size_bytes_full_
- _Field_size_full_
- _Field_size_full_opt_
ms.assetid: b8278a4a-c86e-4845-aa2a-70da21a1dd52
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 6db2202971facb0419db68c04835c8d5c848f528
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77271574"
---
# <a name="annotating-structs-and-classes"></a>構造体とクラスに注釈を付ける
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

インバリアントとして機能する注釈を使用して、構造体とクラスのメンバーに注釈を付けることができます。これらは、外側の構造体をパラメーターまたは結果値として含む関数の呼び出しまたは関数の開始/終了時に true と見なされます。  
  
## <a name="struct-and-class-annotations"></a>構造体とクラスの注釈  
  
- `_Field_range_(low, high)`  
  
     フィールドはからまでの範囲に `low` あります (を含む) `high` 。  `_Satisfies_(_Curr_ >= low && _Curr_ <= high)`適切な事前条件または事後条件を使用して、注釈付きオブジェクトに適用されると同じです。  
  
- `_Field_size_(size)`, `_Field_size_opt_(size)`, `_Field_size_bytes_(size)`, `_Field_size_bytes_opt_(size)`  
  
     で指定されたように、要素 (またはバイト) 内の書き込み可能サイズを持つフィールド `size` 。  
  
- `_Field_size_part_(size, count)`, `_Field_size_part_opt_(size, count)`,         `_Field_size_bytes_part_(size, count)`, `_Field_size_bytes_part_opt_(size, count)`  
  
     によって指定された要素 (またはバイト) 内の書き込み可能サイズを持つフィールド、 `size` および `count` 読み取り可能な要素 (バイト) の。  
  
- `_Field_size_full_(size)`, `_Field_size_full_opt_(size)`, `_Field_size_bytes_full_(size)`, `_Field_size_bytes_full_opt_(size)`  
  
     で指定された要素 (またはバイト) 内の読み取り可能なサイズと書き込み可能なサイズの両方を持つフィールド `size` 。  
  
- `_Struct_size_bytes_(size)`  
  
     で指定された要素 (またはバイト) 内の読み取り可能なサイズと書き込み可能なサイズの両方を持つフィールド `size` 。  
  
     構造体またはクラスの宣言に適用されます。  この型の有効なオブジェクトが、で指定されているバイト数を使用して、宣言された型よりも大きくなる可能性があることを示し `size` ます。  次に例を示します。  
  
    ```cpp  
  
    typedef _Struct_size_bytes_(nSize)  
    struct MyStruct {  
        size_t nSize;  
        …  
    };  
  
    ```  
  
     次に、型のパラメーターのバッファーサイズ (バイト単位) を `pM` `MyStruct *` 次のように取得します。  
  
    ```cpp  
    min(pM->nSize, sizeof(MyStruct))  
    ```  
  
## <a name="see-also"></a>参照  
 [SAL 注釈を使用して C/c + + コードの欠陥を減らす](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [SAL について](../code-quality/understanding-sal.md)   
 [関数のパラメーターと戻り値に注釈を付ける](../code-quality/annotating-function-parameters-and-return-values.md)   
 [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)   
 [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)   
 [注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [組み込み関数](../code-quality/intrinsic-functions.md)   
 [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
