---
title: T4 出力ディレクティブ
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eb1634da6374ad49f1386be4403e72e8edeff2ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75591815"
---
# <a name="t4-output-directive"></a>T4 出力ディレクティブ

Visual Studio テキストテンプレートでは、ディレクティブを使用して、 `output` 変換されたファイルのファイル名拡張子とエンコーディングを定義します。

 たとえば、Visual Studio プロジェクトに、次のディレクティブを含む **MyTemplate.tt** という名前のテンプレートファイルが含まれているとします。

 `<#@output extension=".cs"#>`

 次に、Visual Studio によって**MyTemplate.cs**という名前のファイルが生成されます。

 `output` ディレクティブは、実行時 (前処理済み) のテキスト テンプレートには必要ありません。 その代わりに、アプリケーションは `TextTransform()` を呼び出して、生成済みの文字列を取得します。 詳細については、「 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

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
