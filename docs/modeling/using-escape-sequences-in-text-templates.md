---
title: テキスト テンプレートでのエスケープ シーケンスの使用
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83e6e5cf163037077d0517e5f7ea460f9124f27c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594046"
---
# <a name="use-escape-sequences-in-text-templates"></a>テキストテンプレートでのエスケープシーケンスの使用

テキスト テンプレートのタグを生成したり、(C# コードにおいてのみ) エスケープ制御文字や引用符をエスケープするために、テンプレートでエスケープ シーケンスを使用することができます。

標準コードブロックの開いたり閉じたりするタグを出力ファイルに出力するには、次のようにタグをエスケープします。

```
\<# ... \#>
```

その他のテキスト テンプレート ディレクティブおよびコード ブロック タグも同じようにすることができます。

テキスト ブロックに、テキスト テンプレート タグをエスケープするために使用される文字列が含まれている場合は、次のエスケープ シーケンスを使用することがあります。

- テキスト テンプレートのタグの前に偶数個のエスケープ文字 (\\) がある場合、テンプレート パーサーはそのエスケープ文字の半分とテキスト テンプレート タグの文字列が含まれます。 たとえば、テキスト テンプレートに 4 つのエスケープ文字がある場合、生成されたファイル内には、2 つの "\\" 文字があります。

- テキスト テンプレートのタグの前に奇数個のエスケープ文字 (\\) がある場合、テンプレート パーサーはそのエスケープ\\文字の半分とタグ自体 (\<# または #>) が含まれます。 タグは、テキストテンプレートタグとは見なされません。

- (C# の場合のみ) エスケープ文字 (\\) が、制御文字または引用符をエスケープする並び以外の任意の場所で現れたら、文字が直接出力されます。

## <a name="see-also"></a>関連項目

- [方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成する](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
