---
title: Web パフォーマンス テストのレコーダー プラグインを作成する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, recorder plug-in
ms.assetid: 6fe13be1-aeb5-4927-9bff-35950e194da9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5e32faa4525edc79da3d759d67ad2b5676f38fc2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589152"
---
# <a name="how-to-create-a-recorder-plug-in"></a>方法: レコーダー プラグインを作成する

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin> を使用すると、記録された Web パフォーマンス テストを変更できます。 変更は、 **[Web パフォーマンス テスト レコーダー]** ツール バーの **[停止]** をクリックした後、テストが保存されて Web パフォーマンス テスト エディターで表示される前に行われます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

レコーダー プラグインを利用すると、動的パラメーターで独自のカスタム相関関係を実行できます。 組み込みの関連付け機能では、Web パフォーマンス テストによる Web 記録の動的パラメーターの検出が、完了時、または **Web パフォーマンス テスト エディター** ツール バーの **[動的パラメーターを Web テスト パラメーターに昇格]** の使用時に行われます。 しかし、組み込みの検出機能では、常にすべての動的パラメーターが検出できるわけではありません。 たとえば、セッション ID は検出されません。通常、このパラメーターは、5 ～ 30 分の間隔で変更される値を取得しています。 そのため、関連付けの処理を手動で行う必要があります。

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin> を使用すると、独自のカスタム プラグイン用のコードを記述できます。 このプラグインは、テストが保存されて Web パフォーマンス テスト エディターで表示される前に、さまざまな方法で Web パフォーマンス テストの関連付けや変更を行うことができます。 そのため、特定の動的変数を多くの記録と関連付けなければならないと判断した場合は、処理を自動化できます。

レコーダー プラグインの他の使用方法として、Web パフォーマンス テストでの抽出規則と検証規則の追加、コンテキスト パラメーターの追加、コメントからトランザクションへの変換などがあります。

次の手順では、レコーダー プラグインの基本的なコードの作成、プラグインの配置、およびプラグインの実行の方法について説明します。 手順の後のサンプル コードでは、Visual C# を使用してカスタムの動的パラメーター関連付けレコーダー プラグインを作成する方法を示します。

## <a name="create-a-recorder-plug-in"></a>レコーダー プラグインを作成する

### <a name="to-create-a-recorder-plug-in"></a>レコーダー プラグインを作成するには

1. 作成するレコーダー プラグインの対象となる Web パフォーマンス テストの Web パフォーマンスとロード テストのプロジェクトを含むソリューションを開きます。

2. 新しい**クラス ライブラリ** プロジェクトをソリューションに追加します

3. **ソリューション エクスプローラー**の新しいクラス ライブラリ プロジェクト フォルダーで、 **[参照設定]** フォルダーを右クリックし、 **[参照の追加]** を選択します。

    > [!TIP]
    > 新しいクラス ライブラリ プロジェクト フォルダーの例は、 **[RecorderPlugins]** です。

     **[参照の追加]** ダイアログ ボックスが表示されます。

4. **[.NET]** タブを選択します。

5. スクロール ダウンして、 **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** をクリックし、 **[OK]** をクリックします。

     **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** が**ソリューション エクスプローラー**の **[参照設定]** フォルダーに追加されます。

6. レコーダー プラグインのコードの記述 まず、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin> クラスから派生する新しいパブリック クラスを作成します。

7. <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*> メソッドをオーバーライドします。

    ```csharp
    public class Class1 : WebTestRecorderPlugin
        {
            public override void PostWebTestRecording(object sender, PostWebTestRecordingEventArgs e)
            {
                base.PostWebTestRecording(sender, e);
            }
        }
    ```

     イベント引数によって、作業対象となる 2 つのオブジェクトが与えられます。記録された結果と、記録された Web パフォーマンス テストです。 これにより、結果を反復処理して特定の値を検索し、Web パフォーマンス テスト内の同じ要求に移動して、変更を行うことができるようになります。 コンテキスト パラメーターや、URL のパラメーター化された部分を追加する場合は、単に Web パフォーマンス テストを変更することもできます。

    > [!NOTE]
    > Web パフォーマンス テストを変更する場合は、<xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestRecordingEventArgs.RecordedWebTestModified*> のように、`e.RecordedWebTestModified = true;` プロパティを true に設定する必要もあります。

8. Web 記録を行った後にレコーダー プラグインで何を実行するかに応じて、コードを追加します。 たとえば、以下のサンプルで示すように、カスタムの関連付けを処理するコードを追加できます。 コメントからトランザクションへの変換、Web パフォーマンス テストへの検証規則の追加などを行うようなレコーダー プラグインを作成することもできます。

9. **[ビルド]** メニューの **[\<クラス ライブラリ プロジェクト名> のビルド]** をクリックします。

次に、Visual Studio に登録するためにレコーダー プラグインを配置します。

### <a name="deploy-the-recorder-plug-in"></a>レコーダー プラグインの配置

レコーダー プラグインをコンパイルした後で、生成された DLL を次のうちいずれかの場所に配置します。

- *%ProgramFiles(x86)%\Microsoft Visual Studio\\[バージョン]\\[エディション]\Common7\IDE\PrivateAssemblies\WebTestPlugins*

- *%USERPROFILE%\Documents\Visual Studio [バージョン]\WebTestPlugins*

> [!WARNING]
> レコーダー プラグインを 2 つの場所の一方にコピーした後で、レコーダー プラグインを登録するために Visual Studio を再起動する必要があります。

### <a name="execute-the-recorder-plug-in"></a>レコーダー プラグインの実行

1. 新しい Web パフォーマンス テストを作成します。

     **[WebTestRecorderPlugins の有効化]** ダイアログ ボックスが表示されます。

2. レコーダー プラグインのチェック ボックスをオンにし、 **[OK]** をクリックします。

     Web パフォーマンス テストが記録を完了した後で、新しいレコーダー プラグインが実行されます。

    > [!WARNING]
    > プラグインを使用する Web パフォーマンス テストまたはロード テストを実行すると、次のようなエラー メッセージが表示されることがあります。
    >
    > **要求に失敗しました:\<plug-in> イベントの例外:ファイルまたはアセンブリ '\<"Plug-in name".dll file>, Version=\<n.n.n.n>, Culture=neutral, PublicKeyToken=null' またはその依存関係の 1 つが読み込めませんでした。指定されたファイルが見つかりません。**
    >
    > この問題が発生するのは、いずれかのプラグインのコードを変更して、新しい DLL バージョン **(Version=0.0.0.0)** を作成したのに、プラグインが元のプラグイン バージョンを参照したままになっている場合です。 この問題を解決するには、次の手順を実行します。
    >
    > 1. Web パフォーマンスとロード テストのプロジェクトで、参照に関する警告が表示されます。 プラグイン DLL への参照を削除し、再度追加します。
    > 2. プラグインをテストまたは該当する場所から削除し、その後、追加し直します。

## <a name="example"></a>例

このサンプルでは、カスタムの動的パラメーター関連付けを行う、カスタマイズされた Web パフォーマンス テスト レコーダー プラグインを作成する方法を示します。

> [!NOTE]
> サンプル コードの完全な一覧は、このトピックの最後にあります。

### <a name="iterate-through-the-result-to-find-first-page-with-reportsession"></a>ReportSession で最初のページを検索するための、結果の反復処理

コード サンプルのこの部分では、記録された各オブジェクトを反復処理して、応答本体で ReportSession を検索します。

```csharp
foreach (WebTestResultUnit unit in e.RecordedWebTestResult.Children)
 {
     WebTestResultPage page = unit as WebTestResultPage;
     if (page != null)
     {
         if (!foundId)
         {
             int indexOfReportSession = page.RequestResult.Response.BodyString.IndexOf("ReportSession");
             if (indexOfReportSession > -1)
             {
```

### <a name="add-an-extraction-rule"></a>抽出規則の追加

応答が見つかったら、抽出規則を追加する必要があります。 コード サンプルのこの部分では、<xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRuleReference> クラスを使用して抽出規則を作成し、抽出規則の追加先となる、Web パフォーマンス テスト内の正しい要求を検索します。 各結果オブジェクトには、DeclarativeWebTestItemId という名前の新しいプロパティが追加されており、それがコード内で Web パフォーマンス テストから正しい要求を取得するために使用されています。

```csharp
ExtractionRuleReference ruleReference = new ExtractionRuleReference();
     ruleReference.Type = typeof(ExtractText);
     ruleReference.ContextParameterName = "SessionId";
     ruleReference.Properties.Add(new PluginOrRuleProperty("EndsWith", "&ControlID="));
     ruleReference.Properties.Add(new PluginOrRuleProperty("HtmlDecode", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("IgnoreCase", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("Index", "0"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("Required", "True"));
     ruleReference.Properties.Add(new PluginOrRuleProperty("StartsWith", "ReportSession="));
     ruleReference.Properties.Add(new PluginOrRuleProperty("UseRegularExpression", "False"));

     WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
     if (requestInWebTest != null)
     {
         requestInWebTest.ExtractionRuleReferences.Add(ruleReference);
         e.RecordedWebTestModified = true;
     }
```

### <a name="replace-query-string-parameters"></a>クエリ文字列パラメーターの置換

ここで、コード サンプルのこの部分で示されているように、名前が ReportSession であるすべてのクエリ文字列パラメーターを見つけて、値を {{SessionId}} に変更します。

```csharp
WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
if (requestInWebTest != null)
{
    foreach (QueryStringParameter param in requestInWebTest.QueryStringParameters)
    {
         if (param.Name.Equals("ReportSession"))
         {
             param.Value = "{{SessionId}}";
         }
     }
 }
```

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.TestTools.WebTesting;
using Microsoft.VisualStudio.TestTools.WebTesting.Rules;

namespace RecorderPlugin
{
    [DisplayName("Correlate ReportSession")]
    [Description("Adds extraction rule for Report Session and binds this to querystring parameters that use ReportSession")]
    public class CorrelateSessionId : WebTestRecorderPlugin
    {
        public override void PostWebTestRecording(object sender, PostWebTestRecordingEventArgs e)
        {
            //first find the session id
            bool foundId = false;
            foreach (WebTestResultUnit unit in e.RecordedWebTestResult.Children)
            {
                WebTestResultPage page = unit as WebTestResultPage;
                if (page != null)
                {
                    if (!foundId)
                    {
                        int indexOfReportSession = page.RequestResult.Response.BodyString.IndexOf("ReportSession");
                        if (indexOfReportSession > -1)
                        {
                            //add an extraction rule to this request
                            // Get the corresponding request in the Declarative Web performance test
                            ExtractionRuleReference ruleReference = new ExtractionRuleReference();

                            ruleReference.Type = typeof(ExtractText);
                            ruleReference.ContextParameterName = "SessionId";
                            ruleReference.Properties.Add(new PluginOrRuleProperty("EndsWith", "&ControlID="));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("HtmlDecode", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("IgnoreCase", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("Index", "0"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("Required", "True"));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("StartsWith", "ReportSession="));
                            ruleReference.Properties.Add(new PluginOrRuleProperty("UseRegularExpression", "False"));

                            WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
                            if (requestInWebTest != null)
                            {
                                requestInWebTest.ExtractionRuleReferences.Add(ruleReference);
                                e.RecordedWebTestModified = true;
                            }
                            foundId = true;

                        }
                    }
                    else
                    {
                        //now update query string parameters
                        WebTestRequest requestInWebTest = e.RecordedWebTest.GetItem(page.DeclarativeWebTestItemId) as WebTestRequest;
                        if (requestInWebTest != null)
                        {
                            foreach (QueryStringParameter param in requestInWebTest.QueryStringParameters)
                            {
                                if (param.Name.Equals("ReportSession"))
                                {
                                    param.Value = "{{SessionId}}";
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRuleReference>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin.PostWebTestRecording*>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)
