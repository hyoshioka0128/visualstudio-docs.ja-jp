---
title: 構造体とクラスに注釈を付ける
ms.date: 06/28/2019
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
- _Field_z_
ms.assetid: b8278a4a-c86e-4845-aa2a-70da21a1dd52
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: 70dc130633e9f191811748b2ab316ad339ad4277
ms.sourcegitcommit: 174c992ecdc868ecbf7d3cee654bbc2855aeb67d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74879257"
---
# <a name="annotating-structs-and-classes"></a>構造体とクラスに注釈を付ける

インバリアントとして機能する注釈を使用して、構造体とクラスのメンバーに注釈を付けることができます。これらは、外側の構造体をパラメーターまたは結果値として含む関数の呼び出しまたは関数の開始/終了時に true と見なされます。

## <a name="struct-and-class-annotations"></a>構造体とクラスの注釈

- `_Field_range_(low, high)`

     フィールドは、`low` から `high`までの範囲内にあります。  適切な事前条件または事後条件を使用して、注釈付きオブジェクトに適用される `_Satisfies_(_Curr_ >= low && _Curr_ <= high)` と同じです。

- `_Field_size_(size)`, `_Field_size_opt_(size)`, `_Field_size_bytes_(size)`, `_Field_size_bytes_opt_(size)`

     `size`によって指定された、要素 (またはバイト) に書き込み可能サイズを持つフィールド。

- `_Field_size_part_(size, count)`, `_Field_size_part_opt_(size, count)`,         `_Field_size_bytes_part_(size, count)`, `_Field_size_bytes_part_opt_(size, count)`

     `size`によって指定された要素 (またはバイト) 内の書き込み可能サイズを持つフィールド、および読み取り可能な要素の `count` (バイト)。

- `_Field_size_full_(size)`, `_Field_size_full_opt_(size)`, `_Field_size_bytes_full_(size)`, `_Field_size_bytes_full_opt_(size)`

     `size`によって指定された要素 (またはバイト) 内の読み取り可能なサイズと書き込み可能なサイズの両方を持つフィールド。

- `_Field_z_`

     Null で終わる文字列を含むフィールド。

- `_Struct_size_bytes_(size)`

     構造体またはクラスの宣言に適用されます。  この型の有効なオブジェクトが、`size`によって指定されたバイト数を持つ、宣言された型よりも大きい可能性があることを示します。  例:

    ```cpp

    typedef _Struct_size_bytes_(nSize)
    struct MyStruct {
        size_t nSize;
        ...
    };

    ```

     `MyStruct *` 型のパラメーター `pM` のバイト単位のバッファーサイズは次のようになります。

    ```cpp
    min(pM->nSize, sizeof(MyStruct))
    ```

## <a name="example"></a>使用例

```cpp
#include <sal.h>

// This _Struct_size_bytes_ is equivalent to what below _Field_size_ means.
_Struct_size_bytes_(__builtin_offsetof(MyBuffer, buffer) + bufferSize * sizeof(int))
struct MyBuffer
{
    static int MaxBufferSize;
    
    _Field_z_
    const char* name;
    
    int firstField;

    // ... other fields

    _Field_range_(1, MaxBufferSize)
    int bufferSize;
    
    _Field_size_(bufferSize)        // Prefered way - easier to read and maintain.
    int buffer[]; // Using C99 Flexible array member
};
```

この例のメモ:

- `_Field_z_` は `_Null_terminated_` と同じです。  [名前] フィールドの `_Field_z_` では、[名前] フィールドが null で終わる文字列であることを指定します。
- `bufferSize` の `_Field_range_` は、`bufferSize` の値が1から `MaxBufferSize` (両方を含む) であることを指定します。
- `_Struct_size_bytes_` と `_Field_size_` の注釈の最終的な結果は同等です。 同様のレイアウトを持つ構造体またはクラスの場合、`_Field_size_` は、同等の `_Struct_size_bytes_` 注釈よりも参照と計算が少なくなるため、読み取りと保守が簡単になります。 `_Field_size_` では、バイトサイズへの変換は必要ありません。 Byte サイズが唯一のオプションである場合 (たとえば、void ポインターフィールドの場合) は、`_Field_size_bytes_` を使用できます。 `_Struct_size_bytes_` と `_Field_size_` の両方が存在する場合は、両方ともツールで使用できます。 2つの注釈が一致しない場合の対処方法は、ツールによって異なります。

## <a name="see-also"></a>参照

- [SAL 注釈を使って C/C++ のコード障害を減らす方法](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [SAL について](../code-quality/understanding-sal.md)
- [関数パラメーターおよび戻り値の注釈設定](../code-quality/annotating-function-parameters-and-return-values.md)
- [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)
- [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)
- [注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [組み込み関数](../code-quality/intrinsic-functions.md)
- [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
