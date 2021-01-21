---
title: テキスト テンプレートでのエスケープ シーケンスの使用
description: テキストテンプレートでエスケープシーケンスを使用してテキストテンプレートタグを生成する方法と、C# コードでのみ制御文字と引用符をエスケープする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b007a9b5ccf41a27cda7d9833064eb60394c4dc
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97361327"
---
# <a name="use-escape-sequences-in-text-templates"></a>テキストテンプレートでのエスケープシーケンスの使用

テキストテンプレートでエスケープシーケンスを使用して、テキストテンプレートタグを生成したり (C# コードのみ)、制御文字と引用符をエスケープしたりすることができます。

標準コードブロックの開いたり閉じたりするタグを出力ファイルに出力するには、次のようにタグをエスケープします。

```
\<# ... \#>
```

他のテキストテンプレートディレクティブとコードブロックタグでも同じことができます。

テキストテンプレートタグをエスケープするために使用する文字列がテキストブロックに含まれている場合は、次のエスケープシーケンスを使用できます。

- テキストテンプレートタグの前にエスケープ文字 () が偶数個ある場合 \\ 、テンプレートパーサーにはエスケープ文字の半分が含まれ、シーケンスはテキストテンプレートタグとして含まれます。 たとえば、テキストテンプレートに4つのエスケープ文字がある場合、生成されたファイルには "" という文字が2つあり \\ ます。

- テキストテンプレートタグの前にエスケープ文字 () が表示されない場合 \\ 、テンプレートパーサーには、"" 文字の半分と \\ タグ自体 () が含まれ \<# or #> ます。 タグは、テキストテンプレートタグとは見なされません。

- エスケープ ( \\ ) 文字が、制御文字または引用符をエスケープした場所以外の任意のシーケンス内にある場合 (C# の場合のみ)、文字が直接出力されます。

## <a name="see-also"></a>関連項目

- [方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成する](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
