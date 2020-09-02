---
title: テキスト テンプレートのユーティリティ メソッド
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- text templates, utility methods
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c55da4d58b717bc4d42b6fafdd084067b7e21a31
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75591763"
---
# <a name="text-template-utility-methods"></a>テキスト テンプレートのユーティリティ メソッド

Visual Studio テキストテンプレートでコードを記述するときには、常に使用できるメソッドがいくつかあります。 これらのメソッドは、「」で定義されて <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> います。

> [!TIP]
> また、ホスト環境によって提供される、通常の (前処理されていない) テキストテンプレートで、その他のメソッドやサービスを使用することもできます。 たとえば、ファイルパスを解決し、エラーをログに記録し、Visual Studio および読み込まれたパッケージによって提供されるサービスを取得することができます。 詳細については、「 [テキストテンプレートから Visual Studio にアクセスする](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))」を参照してください。

## <a name="write-methods"></a>メソッドの書き込み

`Write()` `WriteLine()` 式コードブロックを使用する代わりに、メソッドとメソッドを使用して、標準コードブロック内にテキストを追加できます。 次の2つのコードブロックは機能的に同等です。

### <a name="code-block-with-an-expression-block"></a>式ブロックのあるコードブロック

```
<#
int i = 10;
while (i-- > 0)
    { #>
        <#= i #>
    <# }
#>
```

### <a name="code-block-using-writeline"></a>WriteLine () を使用したコードブロック

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

入れ子になった制御構造を持つ長いコードブロック内の式ブロックの代わりに、これらのユーティリティメソッドのいずれかを使用すると役に立つ場合があります。

メソッド `Write()` と `WriteLine()` メソッドには、2つのオーバーロードがあります。1つは1つの文字列パラメーターを受け取り、もう1つは複合書式指定文字列を受け取り、文字列に含めるオブジェクトの配列を取得し `Console.WriteLine()` ます (メソッドなど)。 次の2つの使用 `WriteLine()` 方法は機能的に同等です。

```
<#
    string msg = "Say: {0}, {1}, {2}";
    string s1 = "hello";
    string s2 = "goodbye";
    string s3 = "farewell";

    WriteLine(msg, s1, s2, s3);
    WriteLine("Say: hello, goodbye, farewell");
#>
```

## <a name="indentation-methods"></a>インデントメソッド

インデントメソッドを使用して、テキストテンプレートの出力を書式設定できます。 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>クラスには、 `CurrentIndent` テキストテンプレートの現在のインデント、および `indentLengths` 追加されたインデントのリストであるフィールドを示す文字列プロパティがあります。 メソッドを使用してインデントを追加し、メソッドを使用してインデントを差し引くことができ `PushIndent()` `PopIndent()` ます。 すべてのインデントを解除する場合は、メソッドを使用し `ClearIndent()` ます。 次のコードブロックは、これらのメソッドの使用方法を示しています。

```
<#
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    ClearIndent();
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
#>
```

このコードブロックでは、次の出力が生成されます。

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>エラーと警告のメソッド

エラーと警告のユーティリティメソッドを使用して、Visual Studio エラー一覧にメッセージを追加できます。 たとえば、次のコードでは、エラー一覧にエラーメッセージを追加します。

```
<#
  try
  {
    string str = null;
    Write(str.Length.ToString());
  }
  catch (Exception e)
  {
    Error(e.Message);
  }
#>
```

## <a name="access-to-host-and-service-provider"></a>ホストおよびサービスプロバイダーへのアクセス

プロパティは、 `this.Host` テンプレートを実行しているホストによって公開されているプロパティへのアクセスを提供できます。 を使用するには `this.Host` 、ディレクティブに属性を設定する必要があり `hostspecific` `<@template#>` ます。

`<#@template ... hostspecific="true" #>`

の種類は、 `this.Host` テンプレートが実行されているホストの種類によって異なります。 Visual Studio で実行されているテンプレートでは、にキャストし `this.Host` `IServiceProvider` て、IDE などのサービスにアクセスできます。 次に例を示します。

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>別のユーティリティメソッドのセットの使用

テキスト生成プロセスの一環として、テンプレートファイルはクラスに変換されます。このクラスは常にという名前で `GeneratedTextTransformation` 、から継承され <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> ます。 代わりに別のメソッドのセットを使用する場合は、独自のクラスを記述し、テンプレートディレクティブで指定できます。 クラスは、から継承する必要があり <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> ます。

```
<#@ template inherits="MyUtilityClass" #>
```

ディレクティブを使用して、 `assembly` コンパイル済みクラスが見つかるアセンブリを参照します。
