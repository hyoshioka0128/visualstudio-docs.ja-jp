---
title: 'チュートリアル: モデルにアクセスするテキスト テンプレートのデバッグ'
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f592cfbd46e0f4fc3a64ecaabadf17a6754480c0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593526"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>チュートリアル: モデルにアクセスするテキスト テンプレートのデバッグ
ドメイン固有言語ソリューションでテキストテンプレートを変更または追加すると、エンジンがテンプレートをソースコードに変換したとき、または生成されたコードをコンパイルしたときに、エラーが発生することがあります。 次のチュートリアルでは、テキストテンプレートをデバッグするために実行できるいくつかの操作について説明します。

> [!NOTE]
> 一般的なテキストテンプレートの詳細については、「[コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。 テキストテンプレートのデバッグの詳細については、「[チュートリアル: テキストテンプレートのデバッグ](debugging-a-t4-text-template.md)」を参照してください。

## <a name="creating-a-domain-specific-language-solution"></a>ドメイン固有言語ソリューションの作成
 この手順では、次の特性を持つドメイン固有言語ソリューションを作成します。

- 名前: デバッグ Testlanguage

- ソリューションテンプレート: 最小言語

- ファイル拡張子: ddd

- 会社名: Fabrikam

  ドメイン固有言語ソリューションの作成の詳細については、「[方法: ドメイン固有言語ソリューションを作成](../modeling/how-to-create-a-domain-specific-language-solution.md)する」を参照してください。

## <a name="creating-a-text-template"></a>テキストテンプレートの作成
 ソリューションにテキストテンプレートを追加します。

#### <a name="to-create-a-text-template"></a>テキストテンプレートを作成するには

1. ソリューションをビルドし、デバッガーで実行を開始します。 ( **[ビルド]** メニューの **[ソリューションのリビルド]** をクリックし、 **[デバッグ]** メニューの **[デバッグ開始]** をクリックします)。Visual Studio の新しいインスタンスによって、デバッグプロジェクトが開きます。

2. `DebugTest.tt` という名前のテキストファイルをデバッグプロジェクトに追加します。

3. DebugTest.tt の **[カスタムツール]** プロパティが `TextTemplatingFileGenerator`に設定されていることを確認します。

## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>テキストテンプレートからモデルにアクセスするディレクティブのデバッグ
 テキストテンプレート内のステートメントおよび式からモデルにアクセスするには、最初に生成されたディレクティブプロセッサを呼び出す必要があります。 生成されたディレクティブプロセッサを呼び出すと、モデル内のクラスがプロパティとしてテキストテンプレートコードで使用できるようになります。 詳細については、次を参照してください。[テキスト テンプレートからへのアクセス モデル](../modeling/accessing-models-from-text-templates.md)します。

 次の手順では、正しくないディレクティブ名と不適切なプロパティ名をデバッグします。

#### <a name="to-debug-an-incorrect-directive-name"></a>不適切なディレクティブ名をデバッグするには

1. DebugTest.tt のコードを次のコードに置き換えます。

    > [!NOTE]
    > コードにエラーが含まれています。 デバッグするためにエラーが発生しています。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. **ソリューションエクスプローラー**で、DebugTest.tt を右クリックし、**カスタムツールの実行** をクリックします。

     **[エラー一覧]** ウィンドウに次のエラーが表示されます。

     **' DebuggingTestLanguageDirectiveProcessor ' という名前のプロセッサは、' modelRoot ' という名前のディレクティブをサポートしていません。変換は実行されません。**

     この場合、ディレクティブ呼び出しに無効なディレクティブ名が含まれています。 ディレクティブ名として `modelRoot` が指定されましたが、正しいディレクティブ名が `DebuggingTestLanguage`。

3. **[エラー一覧]** ウィンドウでエラーをダブルクリックして、コードに移動します。

4. コードを修正するには、ディレクティブ名を `DebuggingTestLanguage`に変更します。

     変更が強調表示されます。

    ```csharp
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

    ```vb
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

5. **ソリューションエクスプローラー**で、DebugTest.tt を右クリックし、**カスタムツールの実行** をクリックします。

     これで、システムはテキストテンプレートを変換し、対応する出力ファイルを生成します。 **[エラー一覧]** ウィンドウにエラーは表示されません。

#### <a name="to-debug-an-incorrect-property-name"></a>不適切なプロパティ名をデバッグするには

1. DebugTest.tt のコードを次のコードに置き換えます。

    > [!NOTE]
    > コードにエラーが含まれています。 デバッグするためにエラーが発生しています。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. **ソリューションエクスプローラー**で、DebugTest.tt を右クリックし、**カスタムツールの実行** をクリックします。

     **[エラー一覧]** ウィンドウが表示され、次のいずれかのエラーが表示されます。

     (C#)

     **変換のコンパイル: VisualStudio\<GUID >。指定された Texttransformation ' に ' Examplemodel.store ' の定義が含まれていません**

     (Visual Basic)

     **変換をコンパイルしています: ' Examplemodel.store ' は ' VisualStudio\<GUID > のメンバーではありません。Texttransformation ' があります。**

     この場合、テキストテンプレートコードに無効なプロパティ名が含まれています。 プロパティ名として `ExampleModel` が指定されましたが、正しいプロパティ名が `LibraryModel`。 次のコードに示すように、[提供] パラメーターで正しいプロパティ名を見つけることができます。

    ```
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>
    ```

3. [エラー一覧] ウィンドウでエラーをダブルクリックして、コードに移動します。

4. コードを修正するには、テキストテンプレートコードでプロパティ名を `LibraryModel` に変更します。

     変更が強調表示されています。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.LibraryModel #>
    <#
    foreach (ExampleElement element in this.LibraryModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.LibraryModel #>
    <#
    For Each element as ExampleElement in Me.LibraryModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

5. **ソリューションエクスプローラー**で、DebugTest.tt を右クリックし、**カスタムツールの実行** をクリックします。

     これで、システムはテキストテンプレートを変換し、対応する出力ファイルを生成します。 **[エラー一覧]** ウィンドウにエラーは表示されません。
