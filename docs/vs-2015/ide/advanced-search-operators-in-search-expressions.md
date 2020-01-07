---
title: 検索式の高度な検索演算子 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Help Viewer 2.0, searching for keywords
- Help Viewer 2.0, searching code
- Help Viewer 2.0, searching code by programming language
- Help Viewer 2.0, searching titles
- searching code [Help Viewer 2.0]
- searching titles [Help Viewer 2.0]
ms.assetid: 0cdc1746-8481-45ec-9c53-d0d89cdcbd5e
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c5088fc04f4440260bdb9d3f040d99061c05d243
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72620338"
---
# <a name="advanced-search-operators-in-search-expressions"></a>検索式の高度な検索演算子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

高度な検索演算子を使用すると、より単純な検索式からより複雑な検索式を作成して、コンテンツの検索を絞り込むことができます。 次の表にあるとおり、演算子はクエリが実行されるコンテキストを制限します。

> [!WARNING]
> 高度な検索演算子を入力するときは、検索エンジンに認識させるために最後にコロンを付け、コロンの前にはスペースを入れません。

|検索対象|上限のファイル数を変更するには、|例|結果|
|-------------------|---------|-------------|------------|
|トピックのタイトルの言葉|title:|title:binaryreader|タイトルに "binaryreader" が含まれるトピック。|
|コード サンプルの言葉|code:|code:readdouble|コード サンプルに "readdouble" が含まれるトピック。|
|特定のプログラミング言語のサンプルの言葉|code:vb:|code:vb:string|Visual Basic サンプルに "string" が含まれるトピック。|
|特定のインデックス キーワードに関連付けられているトピック。|keyword:|keyword:readbyte|"readbyte" というインデックス キーワードに関連付けられているトピック。|

 code: 演算子を利用して任意のいくつかのプログラミング言語に関するコンテンツを検索できますが、特定のプログラミング言語でマークアップされているコンテンツのみ、結果が返されます。 次の表は、この演算子が対応しているプログラミング言語を一覧にまとめたものです。

|プログラミング言語|上限のファイル数を変更するには、|
|--------------------------|---------|
|Visual Basic|code:vb<br /><br /> 、または<br /><br /> code:visualbasic|
|C#|code:c#<br /><br /> 、または<br /><br /> code:csharp|
|C++|code:cpp<br /><br /> 、または<br /><br /> code:c++<br /><br /> 、または<br /><br /> code:cplusplus|
|F#|code:f#<br /><br /> 、または<br /><br /> code:fsharp|
|JavaScript|code:javascript<br /><br /> 、または<br /><br /> code:js|
|XAML|code:xaml|

## <a name="see-also"></a>参照
 [検索式の論理演算子](../ide/logical-operators-in-search-expressions.md)[フルテキスト検索のヒント](../ide/full-text-search-tips.md)
