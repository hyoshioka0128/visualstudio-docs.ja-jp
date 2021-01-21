---
title: T4 出力ディレクティブ
description: Visual Studio テキストテンプレートでは、出力ディレクティブを使用して、変換されたファイルのファイル名拡張子とエンコーディングを定義します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9849a326549aa534d9cd558337b825b7e0b8d1f
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97363641"
---
# <a name="t4-output-directive"></a>T4 出力ディレクティブ

Visual Studio テキストテンプレートでは、ディレクティブを使用して、 `output` 変換されたファイルのファイル名拡張子とエンコーディングを定義します。

 たとえば、Visual Studio プロジェクトに、次のディレクティブを含む **MyTemplate.tt** という名前のテンプレートファイルが含まれているとします。

 `<#@output extension=".cs"#>`

 次に、Visual Studio によって **MyTemplate.cs** という名前のファイルが生成されます。

 `output` ディレクティブは、実行時 (前処理済み) のテキスト テンプレートには必要ありません。 その代わりに、アプリケーションは `TextTransform()` を呼び出して、生成済みの文字列を取得します。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

## <a name="using-the-output-directive"></a>出力ディレクティブの使用

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

 各テキスト テンプレートには複数の `output` ディレクティブを含めてはいけません。

## <a name="extension-attribute"></a>拡張属性
 生成されたテキスト出力ファイルのファイル名の拡張子を指定します。

 既定値は **.cs です。**

 例: `<#@ output extension=".txt" #>`

 `<#@ output extension=".htm" #>`

 `<#@ output extension=".cs" #>`

 `<#@ output extension=".vb" #>`

 使用できる値: 任意の有効なファイル名拡張子。

## <a name="encoding-attribute"></a>encoding 属性
 出力ファイルが生成されるときに使用するエンコードを指定します。 次に例を示します。

 `<#@ output encoding="utf-8"#>`

 既定値は、テキスト テンプレート ファイルが使用するエンコードです。

 使用可能な値: `us-ascii`

 `utf-16BE`

 `utf-16`

 `utf-8`

 `utf-7`

 `utf-32`

 `0` (システムの既定値)

 一般に、<xref:System.Text.Encoding.GetEncodings%2A?displayProperty=fullName> が返す任意のエンコードの WebName 文字列または CodePage 数値を使用できます。
