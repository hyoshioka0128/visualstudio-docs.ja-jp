---
title: VS 拡張機能内でのテキスト変換の呼び出し
description: テキストテンプレートサービスを使用してテキストテンプレートを変換する方法について説明します。 また、STextTemplating サービスを取得して ITextTemplating にキャストする方法についても説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40e781e08bba5e01b5e453e4545b5dd19e5a4d16
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97360872"
---
# <a name="invoke-text-transformation-in-a-visual-studio-extension"></a>Visual Studio 拡張機能でのテキスト変換の呼び出し

メニューコマンドや [ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)などの Visual Studio 拡張機能を作成する場合は、テキストテンプレートサービスを使用してテキストテンプレートを変換できます。 [Stexttemplating](/previous-versions/visualstudio/visual-studio-2012/bb932394(v=vs.110))サービスを取得し、 [itexttemplating](/previous-versions/visualstudio/visual-studio-2012/bb932392(v=vs.110))にキャストします。

## <a name="get-the-text-templating-service"></a>テキストテンプレートサービスを取得する

```csharp
using Microsoft.VisualStudio.TextTemplating;
using Microsoft.VisualStudio.TextTemplating.VSHost;
...
// Get a service provider - how you do this depends on the context:
IServiceProvider serviceProvider = ...; // An instance of EnvDTE, for example

// Get the text template service:
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;

// Process a text template:
string result = t4.ProcessTemplate(filePath, System.IO.File.ReadAllText(filePath));
```

## <a name="pass-parameters-to-the-template"></a>テンプレートにパラメーターを渡す

 パラメーターをテンプレートに渡すことができます。 テンプレート内で、`<#@parameter#>` ディレクティブを使用してパラメーター値を取得できます。

 パラメーターの型については、シリアル化またはマーシャリング可能な型を使用する必要があります。 つまり、<xref:System.SerializableAttribute> を使用して型を宣言するか、<xref:System.MarshalByRefObject> から型を派生する必要があります。 この制限が必要なのは、テキスト テンプレートは別の AppDomain で実行されるためです。 **System.string や system.string** など、**すべての組み込み** 型がシリアル化可能です。

 パラメーター値を渡すために、呼び出し元のコードでは `Session` ディクショナリまたは <xref:System.Runtime.Remoting.Messaging.CallContext> に値を配置できます。

 次の例では、両方の方法を使用して短いテスト テンプレートを変換しています。

```csharp
using Microsoft.VisualStudio.TextTemplating;
using Microsoft.VisualStudio.TextTemplating.VSHost;
...
// Get a service provider - how you do this depends on the context:
IServiceProvider serviceProvider = dte;

// Get the text template service:
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;
ITextTemplatingSessionHost sessionHost = t4 as ITextTemplatingSessionHost;

// Create a Session in which to pass parameters:
sessionHost.Session = sessionHost.CreateSession();
sessionHost.Session["parameter1"] = "Hello";
sessionHost.Session["parameter2"] = DateTime.Now;

// Pass another value in CallContext:
System.Runtime.Remoting.Messaging.CallContext.LogicalSetData("parameter3", 42);

// Process a text template:
string result = t4.ProcessTemplate("",
   // This is the test template:
   "<#@parameter type=\"System.String\" name=\"parameter1\"#>"
 + "<#@parameter type=\"System.DateTime\" name=\"parameter2\"#>"
 + "<#@parameter type=\"System.Int32\" name=\"parameter3\"#>"
 + "Test: <#=parameter1#>    <#=parameter2#>    <#=parameter3#>");

// This test code yields a result similar to the following line:
//     Test: Hello    07/06/2010 12:37:45    42
```

## <a name="error-reporting-and-the-output-directive"></a>エラー報告と output ディレクティブ

処理中に発生したエラーは、Visual Studio のエラーウィンドウに表示されます。 さらに、 [Itexttemplatingcallback](/previous-versions/visualstudio/visual-studio-2012/bb932397(v=vs.110))を実装するコールバックを指定することで、エラーを通知することができます。

結果の文字列をファイルに書き込む場合は、テンプレートの `<#@output#>` ディレクティブで指定されているファイル拡張子とエンコードを確認できます。 この情報は、コールバックにも渡されます。 詳細については、「 [T4 Output ディレクティブ](../modeling/t4-output-directive.md)」を参照してください。

```csharp
void ProcessMyTemplate(string MyTemplateFile)
{
  string templateContent = File.ReadAllText(MyTemplateFile);
  T4Callback cb = new T4Callback();
  // Process a text template:
  string result = t4.ProcessTemplate(MyTemplateFile, templateContent, cb);
  // If there was an output directive in the MyTemplateFile,
  // then cb.SetFileExtension() will have been called.
  // Determine the output file name:
  string resultFileName =
    Path.Combine(Path.GetDirectoryName(MyTemplateFile),
        Path.GetFileNameWithoutExtension(MyTemplateFile))
      + cb.fileExtension;
  // Write the processed output to file:
  File.WriteAllText(resultFileName, result, cb.outputEncoding);
  // Append any error messages:
  if (cb.errorMessages.Count > 0)
  {
    File.AppendAllLines(resultFileName, cb.errorMessages);
  }
}

class T4Callback : ITextTemplatingCallback
{
  public List<string> errorMessages = new List<string>();
  public string fileExtension = ".txt";
  public Encoding outputEncoding = Encoding.UTF8;

  public void ErrorCallback(bool warning, string message, int line, int column)
  { errorMessages.Add(message); }

  public void SetFileExtension(string extension)
  { fileExtension = extension; }

  public void SetOutputEncoding(Encoding encoding, bool fromOutputDirective)
  { outputEncoding = encoding; }
}
```

次のようなテンプレート ファイルを使用してコードをテストできます。

```
<#@output extension=".htm" encoding="ASCII"#>
<# int unused;  // Compiler warning "unused variable"
#>
Sample text.
```

コンパイラの警告が Visual Studio のエラーウィンドウに表示され、への呼び出しも生成され `ErrorCallback` ます。

## <a name="reference-parameters"></a>参照パラメーター

<xref:System.MarshalByRefObject> から派生したパラメーター クラスを使用して、テキスト テンプレートの外部に値を渡すことができます。

## <a name="related-articles"></a>関連記事

前処理されたテキストテンプレートからテキストを生成するには `TransformText()` 、生成されたクラスのメソッドを呼び出します。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

Visual Studio 拡張機能の外部でテキストを生成するには: カスタムホストを定義します。 詳細については、「 [カスタムホストを使用したテキストテンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md)」を参照してください。

後でコンパイルして実行できるソースコードを生成するには、 [Itexttemplating](/previous-versions/visualstudio/visual-studio-2012/bb932392(v=vs.110))の[PreprocessTemplate](/previous-versions/visualstudio/visual-studio-2012/ee844321(v=vs.110))メソッドを呼び出します。
