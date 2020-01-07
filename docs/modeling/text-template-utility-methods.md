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
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591763"
---
# <a name="text-template-utility-methods"></a>テキスト テンプレートのユーティリティ メソッド

Visual Studio のテキスト テンプレートでコードを記述する場合に常に使用可能ないくつかのメソッドがあります。 これらのメソッドは、 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> で定義されています。

> [!TIP]
> 通常の (前処理されていない) テキスト テンプレートにおいて、ホスト環境によって提供される他のメソッドとサービスを使用することもできます。 たとえば、ファイル パスの解決、エラーのログ、Visual Studio および読み込まれた任意のパッケージによって提供されるサービスの取得です。 詳細については、次を参照してください。[テキスト テンプレートから Visual Studio のへのアクセス](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))

## <a name="write-methods"></a>メソッドの書き込み

式 コード ブロックを使用する代わりに、標準のコード ブロック内でテキストを追加する、`Write()`および`WriteLine()`メソッドを使うことができます。 次の2つのコードブロックは機能的に同等です。

### <a name="code-block-with-an-expression-block"></a>式ブロックを持つコード ブロック

```
<#
int i = 10;
while (i-- > 0)
    { #>
        <#= i #>
    <# }
#>
```

### <a name="code-block-using-writeline"></a>WriteLine() を使用したコード ブロック

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

入れ子になった制御構造を持つ長いコード ブロック内では、式ブロックの代わりにこれらのユーティリティ メソッドのいずれかを使用すると便利です。

`Write()`と`WriteLine()`メソッドは、(`Console.WriteLine()`メソッドと同じように) ひとつの文字列パラメーターをとるものと、複合書式指定文字列および文字列に含めるためのオブジェクトの配列をとるものの、2 つのオーバー ロードがあります。 次の 2 つの `WriteLine()` の使い方は機能的に同等です。

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

テキスト テンプレートの出力を整えるために、インデント メソッドを使用できます。 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>クラスは、テキスト テンプレートでの現在のインデントの位置を示す `CurrentIndent` 文字列プロパティと、追加されたインデントのリストである `indentLengths` フィールドを持っています。 `PushIndent()`メソッドでインデントを追加し、`PopIndent()`メソッドでインデントを減らすことができます。 すべてのインデントを削除する場合は、`ClearIndent()`メソッドを使用します。 次のコードブロックは、これらのメソッドの使用方法を示しています。

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

このコード ブロックは、次の出力を生成します。

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>エラーと警告のメソッド

エラーと警告をユーティリティ メソッドを使用して、メッセージを Visual Studio のエラー一覧に追加することができます。 たとえば、次のコードはエラー一覧に、エラー メッセージを追加します。

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

`this.Host` プロパティは、テンプレートを実行しているホストによって公開されるプロパティへのアクセスを提供します。 `this.Host`を使用するには、`<@template#>` ディレクティブの `hostspecific` 属性を設定する必要があります。

`<#@template ... hostspecific="true" #>`

`this.Host`の型は、テンプレートを実行しているホストの種類によって異なります。 Visual Studio で実行されているテンプレートでは、IDE などのサービスにアクセスするために、`this.Host` を `IServiceProvider` にキャストすることができます。 例:

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>さまざまなユーティリティ メソッドの使用

テキスト生成処理の一環として、テンプレート ファイルはクラス（名前は常に `GeneratedTextTransformation` で、<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>から継承しています）に変換されます。 代わりの別のメソッド セットを使用したい場合は、独自のクラスを記述し template ディレクティブで指定することができます。 クラスは、<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> を継承する必要があります。

```
<#@ template inherits="MyUtilityClass" #>
```

コンパイル済みのクラスがあるアセンブリを参照するために、`assembly` ディレクティブを使用してください。
