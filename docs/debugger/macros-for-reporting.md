---
title: レポート用マクロ | Microsoft Docs
description: CRTDBG.H で提供されるデバッグ マクロ _RPTn と _RPTFn についてと、独自のデバッグ マクロの作成について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.macros
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1920b4eddcbffa5cd51d548ade9af3a3a2f208d0
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903793"
---
# <a name="macros-for-reporting"></a>レポート用マクロの使用
デバッグでは、CRTDBG.H に定義されている **_RPTn** マクロと **_RPTFn** マクロで使用される `printf` ステートメントを置き換えることができます。 **_DEBUG** が定義されていないリリース ビルドでは自動的に消滅するため、これらのマクロを **#ifdef** で囲む必要はありません。

|マクロ|説明|
|-----------|-----------------|
|**_RPT0**、 **_RPT1**、 **_RPT2**、 **_RPT3**、 **_RPT4**|メッセージ文字列と、0 から 4 個の引数を出力します。 **_RPT1** から **_RPT4** の場合、メッセージ文字列は、引数に対して printf 形式の書式設定文字列として機能します。|
|**_RPTF0**、 **_RPTF1**、 **_RPTF2**、 **_RPTF3**、 **_RPTF4**|**_RPTn** と同様ですが、これらのマクロが記述されているファイル名と行番号も出力します。|

 次に例を示します。

```cpp
#ifdef _DEBUG
    if ( someVar > MAX_SOMEVAR )
        printf( "OVERFLOW! In NameOfThisFunc( ),
               someVar=%d, otherVar=%d.\n",
               someVar, otherVar );
#endif
```

 このコードは、`someVar` の値と `otherVar` の値を **stdout** に出力します。 次のように `_RPTF2` を呼び出すと、これらの値と一緒にファイル名と行番号も出力できます。

```cpp
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );
```

特定のアプリケーションでは、C ランタイム ライブラリのマクロで提供されているデバッグ レポートでは不十分な場合があります。 その場合は、独自の要件を満たす専用のマクロを記述できます。 たとえば、ヘッダー ファイルの 1 つに、次のような **ALERT_IF2** というマクロを定義するコードを含めることができます。

```cpp
#ifndef _DEBUG                  /* For RELEASE builds */
#define  ALERT_IF2(expr, msg, arg1, arg2)  do {} while (0)
#else                           /* For DEBUG builds   */
#define  ALERT_IF2(expr, msg, arg1, arg2) \
    do { \
        if ((expr) && \
            (1 == _CrtDbgReport(_CRT_ERROR, \
                __FILE__, __LINE__, msg, arg1, arg2))) \
            _CrtDbgBreak( ); \
    } while (0)
#endif
```

 **ALERT_IF2** への 1 回の呼び出しで、**printf** コードのすべての機能を実行できます。

```cpp
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),
someVar=%d, otherVar=%d.\n", someVar, otherVar );
```

 カスタム マクロを簡単に変更して、さまざまな変換先に対してより多くの情報を報告することができます。 この方法は、デバッグ要件が発展するときに特に役立ちます。

## <a name="see-also"></a>関連項目
- [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)
