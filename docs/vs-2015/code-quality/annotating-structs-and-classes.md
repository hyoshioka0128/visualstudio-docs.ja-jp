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
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271574"
---
# <a name="annotating-structs-and-classes"></a>構造体とクラスに注釈を付ける
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

インバリアントとして機能する注釈を使用して、構造体とクラスのメンバーに注釈を付けることができます。これらは、外側の構造体をパラメーターまたは結果値として含む関数の呼び出しまたは関数の開始/終了時に true と見なされます。  
  
## <a name="struct-and-class-annotations"></a>構造体とクラスの注釈  
  
- `_Field_range_(low, high)`  
  
     フィールドは、`low` から `high`までの範囲内にあります。  適切な事前条件または事後条件を使用して、注釈付きオブジェクトに適用される `_Satisfies_(_Curr_ >= low && _Curr_ <= high)` と同じです。  
  
- `_Field_size_(size)`、`_Field_size_opt_(size)`、`_Field_size_bytes_(size)`, `_Field_size_bytes_opt_(size)`  
  
     `size`によって指定された、要素 (またはバイト) に書き込み可能サイズを持つフィールド。  
  
- `_Field_size_part_(size, count)`、`_Field_size_part_opt_(size, count)`、`_Field_size_bytes_part_(size, count)`、`_Field_size_bytes_part_opt_(size, count)`  
  
     `size`によって指定された要素 (またはバイト) 内の書き込み可能サイズを持つフィールド、および読み取り可能な要素の `count` (バイト)。  
  
- `_Field_size_full_(size)`、`_Field_size_full_opt_(size)`、`_Field_size_bytes_full_(size)`, `_Field_size_bytes_full_opt_(size)`  
  
     `size`によって指定された要素 (またはバイト) 内の読み取り可能なサイズと書き込み可能なサイズの両方を持つフィールド。  
  
- `_Struct_size_bytes_(size)`  
  
     `size`によって指定された要素 (またはバイト) 内の読み取り可能なサイズと書き込み可能なサイズの両方を持つフィールド。  
  
     構造体またはクラスの宣言に適用されます。  この型の有効なオブジェクトが、`size`によって指定されたバイト数を持つ、宣言された型よりも大きい可能性があることを示します。  例 :  
  
    ```cpp  
  
    typedef _Struct_size_bytes_(nSize)  
    struct MyStruct {  
        size_t nSize;  
        …  
    };  
  
    ```  
  
     `MyStruct *` 型のパラメーター `pM` のバイト単位のバッファーサイズは次のようになります。  
  
    ```cpp  
    min(pM->nSize, sizeof(MyStruct))  
    ```  
  
## <a name="see-also"></a>参照  
 [SAL 注釈を使用して CC++ /コードの欠陥を減らす](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [SAL](../code-quality/understanding-sal.md)  について  
 [関数のパラメーターと戻り値に注釈を付ける](../code-quality/annotating-function-parameters-and-return-values.md)   
 [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)   
 [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)   
 [注釈を適用するタイミングと場所を指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)する   
 [組み込み関数](../code-quality/intrinsic-functions.md)   
 [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
