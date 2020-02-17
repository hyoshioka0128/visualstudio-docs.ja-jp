---
title: コード分析ヒントに _Analysis_assume を使用する
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _Analysis_assume
helpviewer_keywords:
- _Analysis_assume
ms.assetid: 51205d97-4084-4cf4-a5ed-3eeaf67deb1b
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: 1fec348108afdfe3cdac3325e0a1750b55332db4
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271644"
---
# <a name="how-to-specify-additional-code-information-by-using-_analysis_assume"></a>方法: _Analysis_assume を使用して追加のコード情報を指定する

C/C++ code のコード分析ツールにヒントを提供して、分析プロセスを支援し、警告を減らすことができます。 追加情報を提供するには、次の関数を使用します。

`_Analysis_assume(`  `expr`  `)`

`expr`-true と評価されることを想定している任意の式。

コード分析ツールでは、式によって表される条件が、関数が出現する位置で true であることを前提としています。また、変数への代入などによって、式が変更されるまでは true のままです。

> [!NOTE]
> `_Analysis_assume` は、コードの最適化には影響しません。 コード分析ツールの外部では、`_Analysis_assume` は no op として定義されます。

## <a name="example"></a>例

次のコードでは、`_Analysis_assume` を使用して、コード分析の警告[C6388](../code-quality/c6388.md)を修正します。

```cpp
#include<windows.h>
#include<codeanalysis\sourceannotations.h>

using namespace vc_attributes;

//requires pc to be null
void f([Pre(Null=Yes)] char* pc);

// calls free and sets ch to null
void FreeAndNull(char** ch);

void test()
{
    char pc = (char)malloc(5);
    FreeAndNull(&pc);
    _Analysis_assume(pc == NULL);
    f(pc);
}
```

## <a name="see-also"></a>参照

- [__assume](/cpp/intrinsics/assume)
