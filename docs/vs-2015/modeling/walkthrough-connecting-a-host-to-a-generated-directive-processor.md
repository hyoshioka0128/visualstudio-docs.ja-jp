---
title: 'チュートリアル: 生成されたディレクティブプロセッサにホストを接続する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [text templates], connecting host to processor
- text templates, custom directive hosts
ms.assetid: 254540d9-90d6-42de-8c1c-068affd56e83
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 17ec8199e99e76d5995e49570c82ad8523505ebe
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75915991"
---
# <a name="walkthrough-connecting-a-host-to-a-generated-directive-processor"></a>チュートリアル: 生成済みディレクティブ プロセッサへのホストの接続
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストテンプレートを処理する独自のホストを作成できます。 基本的なカスタムホストについては、 [「チュートリアル: カスタムテキストテンプレートホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md)」で説明しています。 このホストを拡張して、複数の出力ファイルを生成するなどの機能を追加することができます。

 このチュートリアルでは、ディレクティブプロセッサを呼び出すテキストテンプレートをサポートするようにカスタムホストを拡張します。 ドメイン固有言語を定義すると、ドメインモデルの*ディレクティブプロセッサ*が生成されます。 ディレクティブプロセッサを使用すると、モデルにアクセスするテンプレートをユーザーが簡単に記述できるようになり、テンプレートにアセンブリおよびインポートディレクティブを記述する必要性が減ります。

> [!WARNING]
> このチュートリアル[は、「チュートリアル: カスタムテキストテンプレートホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md)」を基に構築されています。 まず、このチュートリアルを実行します。

 このチュートリアルでは、次のタスクについて説明します。

- [!INCLUDE[dsl](../includes/dsl-md.md)] を使用して、ドメインモデルに基づくディレクティブプロセッサを生成します。

- 生成されたディレクティブプロセッサにカスタムテキストテンプレートホストを接続します。

- 生成されたディレクティブプロセッサを使用したカスタムホストのテスト。

## <a name="prerequisites"></a>[前提条件]
 DSL を定義するには、以下のコンポーネントをインストールしておく必要があります。

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[https://www.visualstudio.com/](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[Visual Studio SDK](../extensibility/visual-studio-sdk.md)|
|Visual Studio Visualization and Modeling SDK|[SDK のダウンロードのモデリング](https://www.microsoft.com/download/details.aspx?id=48148)|

 さらに、「[チュートリアル: カスタムテキストテンプレートホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md)」では、カスタムテキストテンプレート変換を作成する必要があります。

## <a name="using-domain-specific-language-tools-to-generate-a-directive-processor"></a>ドメイン固有言語ツールを使用したディレクティブプロセッサの生成
 このチュートリアルでは、ドメイン固有言語デザイナーウィザードを使用して、DSLMinimalTest ソリューション用のドメイン固有言語を作成します。

#### <a name="to-use-domain-specific-language-tools-to-generate-a-directive-processor-that-is-based-on-a-domain-model"></a>ドメインモデルに基づくディレクティブプロセッサを生成するためにドメイン固有言語ツールを使用するには

1. 次の特性を持つドメイン固有言語ソリューションを作成します。

   - 名前: DSLMinimalTest

   - ソリューションテンプレート: 最小言語

   - ファイル拡張子: 最小

   - 会社名: Fabrikam

     ドメイン固有言語ソリューションの作成の詳細については、「[方法: ドメイン固有言語ソリューションを作成](../modeling/how-to-create-a-domain-specific-language-solution.md)する」を参照してください。

2. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

   > [!IMPORTANT]
   > この手順では、ディレクティブプロセッサを生成し、そのキーをレジストリに追加します。

3. **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の2番目のインスタンスが開きます。

4. 実験用ビルドで、**ソリューションエクスプローラー**で、ファイルのサンプル **最小** をダブルクリックします。

    デザイナーでファイルが開きます。 モデルには、ExampleElement1 と ExampleElement2 という2つの要素と、それらの間のリンクがあります。

5. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の2番目のインスタンスを閉じます。

6. ソリューションを保存し、ドメイン固有言語デザイナーを閉じます。

## <a name="connecting-a-custom-text-template-host-to-a-directive-processor"></a>カスタムテキストテンプレートホストをディレクティブプロセッサに接続する
 ディレクティブプロセッサを生成したら、「[チュートリアル: カスタムテキストテンプレートホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md)」で作成したディレクティブプロセッサとカスタムテキストテンプレートホストを接続します。

#### <a name="to-connect-a-custom-text-template-host-to-the-generated-directive-processor"></a>生成されたディレクティブプロセッサにカスタムテキストテンプレートホストを接続するには

1. CustomHost ソリューションを開きます。

2. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

     **[参照の追加]** ダイアログボックスが開き、 **[.net]** タブが表示されます。

3. 次の参照を追加します。

    - Microsoft.VisualStudio.Modeling.Sdk.11.0

    - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0

    - Microsoft.VisualStudio.TextTemplating.11.0

    - Microsoft.VisualStudio.TextTemplating.Interfaces.11.0

    - Microsoft.VisualStudio.TextTemplating.Modeling.11.0

    - Microsoft.VisualStudio.TextTemplating.VSHost.11.0

4. Program.cs または module1.vb の先頭に、次のコード行を追加します。

    ```csharp
    using Microsoft.Win32;
    ```

    ```vb
    Imports Microsoft.Win32
    ```

5. プロパティ `StandardAssemblyReferences`のコードを見つけて、次のコードに置き換えます。

    > [!NOTE]
    > この手順では、ホストがサポートする、生成されたディレクティブプロセッサに必要なアセンブリへの参照を追加します。

    ```csharp
    //the host can provide standard assembly references
    //the engine will use these references when compiling and
    //executing the generated transformation class
    //--------------------------------------------------------------
    public IList<string> StandardAssemblyReferences
    {
        get
        {
            return new string[]
            {
                //if this host searches standard paths and the GAC
                //we can specify the assembly name like this:
                //"System"
                //since this host only resolves assemblies from the
                //fully qualified path and name of the assembly
                //this is a quick way to get the code to give us the
                //fully qualified path and name of the System assembly
                //---------------------------------------------------------
                typeof(System.Uri).Assembly.Location,
                            typeof(System.Uri).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.ModelElement).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplating).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation).Assembly.Location

            };
        }
    }
    ```

6. 関数 `ResolveDirectiveProcessor`のコードを見つけて、次のコードに置き換えます。

    > [!IMPORTANT]
    > このコードには、接続先の生成されたディレクティブプロセッサの名前へのハードコーディングされた参照が含まれています。 これを簡単に行うことができます。この場合、レジストリに一覧表示されているすべてのディレクティブプロセッサが検索され、一致の検索が試行されます。 この場合、ホストは、生成されたすべてのディレクティブプロセッサで動作します。

    ```csharp
    //the engine calls this method based on the directives the user has
            //specified it in the text template
            //this method can be called 0, 1, or more times
            //---------------------------------------------------------------------
            public Type ResolveDirectiveProcessor(string processorName)
            {
                //check the processor name, and if it is the name of the processor the
                //host wants to support, return the type of the processor
                //---------------------------------------------------------------------
                if (string.Compare(processorName, "DSLMinimalTestDirectiveProcessor", StringComparison.InvariantCultureIgnoreCase) == 0)
                {
                    try
                    {
                        string keyName = @"Software\Microsoft\VisualStudio\10.0Exp_Config\TextTemplating\DirectiveProcessors\DSLMinimalTestDirectiveProcessor";
                        using (RegistryKey specificKey = Registry.CurrentUser.OpenSubKey(keyName))
                        {
                            if (specificKey != null)
                            {
                                List<string> names = new List<String>(specificKey.GetValueNames());
                                string classValue = specificKey.GetValue("Class") as string;
                                if (!string.IsNullOrEmpty(classValue))
                                {
                                    string loadValue = string.Empty;
                                    System.Reflection.Assembly processorAssembly = null;
                                    if (names.Contains("Assembly"))
                                    {
                                        loadValue = specificKey.GetValue("Assembly") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //the assembly must be installed in the GAC
                                            processorAssembly = System.Reflection.Assembly.Load(loadValue);
                                        }
                                    }
                                    else if (names.Contains("CodeBase"))
                                    {
                                        loadValue = specificKey.GetValue("CodeBase") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //loading local assembly
                                            processorAssembly = System.Reflection.Assembly.LoadFrom(loadValue);
                                        }
                                    }
                                    if (processorAssembly == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    Type processorType = processorAssembly.GetType(classValue);
                                    if (processorType == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    return processorType;
                                }
                            }
                        }
                    }
                    catch (Exception e)
                    {
                        //if the directive processor can not be found, throw an error
                        throw new Exception("Directive Processor not found");
                    }
                }

                //if the directive processor is not one this host wants to support
                throw new Exception("Directive Processor not supported");
            }
    ```

7. **[ファイル]** メニューの **[すべてを保存]** をクリックします。

8. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="testing-the-custom-host-with-the-directive-processor"></a>ディレクティブプロセッサを使用したカスタムホストのテスト
 カスタムテキストテンプレートホストをテストするには、まず、生成されたディレクティブプロセッサを呼び出すテキストテンプレートを作成する必要があります。 次に、カスタムホストを実行し、テキストテンプレートの名前を渡して、ディレクティブが正しく処理されていることを確認します。

#### <a name="to-create-a-text-template-to-test-the-custom-host"></a>テキスト テンプレートを作成してカスタム ホストをテストするには

1. テキスト ファイルを作成し、名前を `TestTemplateWithDP.tt` にします。 メモ帳などの任意のテキストエディターを使用して、ファイルを作成できます。

2. 次の内容をテキスト ファイルに追加します。

    > [!NOTE]
    > テキストテンプレートのプログラミング言語は、カスタムホストのプログラミング言語と一致している必要はありません。

    ```csharp
    Text Template Host Test

    <#@ template debug="true" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
    <# //this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>
    <# //uncomment this line to test that the host allows the engine to set the extension #>
    <# //@ output extension=".htm" #>

    <# //uncomment this line if you want to see the generated transformation class #>
    <# //System.Diagnostics.Debugger.Break(); #>
    <# //this code uses the results of the examplemodel directive #>
    <#
        foreach ( ExampleElement box in this.ExampleModel.Elements )
        {
            WriteLine("Box: {0}", box.Name);

            foreach (ExampleElement linkedTo in box.Targets)
            {
                WriteLine("Linked to: {0}", linkedTo.Name);
            }

            foreach (ExampleElement linkedFrom in box.Sources)
            {
                WriteLine("Linked from: {0}", linkedFrom.Name);
            }

            WriteLine("");
        }
    #>
    ```

    ```vb
    Text Template Host Test

    <#@ template debug="true" language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>

    <# 'this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>

    <# 'Uncomment this line to test that the host allows the engine to set the extension. #>
    <# '@ output extension=".htm" #>

    <# 'Uncomment this line if you want to see the generated transformation class. #>
    <# 'System.Diagnostics.Debugger.Break() #>

    <# 'this code uses the results of the examplemodel directive #>

    <#
       For Each box as ExampleElement In Me.ExampleModel.Elements

           WriteLine("Box: {0}", box.Name)

            For Each LinkedTo as ExampleElement In box.Targets
                WriteLine("Linked to: {0}", LinkedTo.Name)
            Next

            For Each LinkedFrom as ExampleElement In box.Sources
                WriteLine("Linked from: {0}", LinkedFrom.Name)
            Next

            WriteLine("")

       Next
    #>
    ```

3. コード内で、最初の手順で作成したデザイン固有の言語から、パス > \<を、サンプルの最小ファイルのパスに置き換えます。

4. ファイルを保存して閉じます。

#### <a name="to-test-the-custom-host"></a>カスタム ホストをテストするには

1. コマンド プロンプト ウィンドウを開きます。

2. カスタム ホストの実行可能ファイルのパスを入力します。ただし、Enter キーはまだ押さないでください。

     たとえば、次のように入力します。

     `<YOUR PATH>CustomHost\bin\Debug\CustomHost.exe`

    > [!NOTE]
    > アドレスを入力する代わりに、 **Windows エクスプローラー**で customhost ファイルを参照し、そのファイルをコマンドプロンプトウィンドウにドラッグすることもできます。

3. 空白を入力します。

4. テキスト テンプレート ファイルのパスを入力し、Enter キーを押します。

     たとえば、次のように入力します。

     `<YOUR PATH>TestTemplateWithDP.txt`

    > [!NOTE]
    > アドレスを入力する代わりに、 **Windows エクスプローラー**で TestTemplateWithDP ファイルを参照し、ファイルをコマンドプロンプトウィンドウにドラッグすることができます。

     カスタムホストアプリケーションが実行され、テキストテンプレート変換プロセスが開始されます。

5. **エクスプローラー**で、ファイル TestTemplateWithDP .txt を含むフォルダーに移動します。

     このフォルダーには、TestTemplateWithDP1 ファイルも含まれています。

6. このファイルを開き、テキスト テンプレート変換の結果を確認します。

     生成されたテキスト出力の結果が表示され、次のようになります。

    ```
    Text Template Host Test

    Box: ExampleElement1
    Linked to: ExampleElement2

    Box: ExampleElement2
    Linked from: ExampleElement1
    ```

## <a name="see-also"></a>参照
 [チュートリアル: カスタム テキスト テンプレート ホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md)
