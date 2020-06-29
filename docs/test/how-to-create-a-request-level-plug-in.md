---
title: Web パフォーマンス テストの要求レベル プラグインを作成する
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- request-level plug-in, creating
- Web performance tests, requests
ms.assetid: d0b5b23c-7e94-4637-be6c-2620a5442d46
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03de870da2cd75c8a254010db682903f314cc10d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287975"
---
# <a name="how-to-create-a-request-level-plug-in"></a>方法: 要求レベルのプラグインを作成する

"*要求*" は、Web パフォーマンス テストを構成する宣言ステートメントです。 Web パフォーマンス テスト プラグインを使用すると、Web パフォーマンス テストの主要な宣言ステートメントとコードを分離し、そのコードを再利用できます。 プラグインを作成し、要求を含む Web パフォーマンス テストに追加するのと同じように、個々の要求にも追加できます。 カスタマイズされた "*要求プラグイン*" を使用すると、Web パフォーマンス テスト中の特定の要求の実行時にコードを呼び出すことができます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

すべての Web パフォーマンス テスト要求プラグインには、PreRequest メソッドと PostRequest メソッドがあります。 要求プラグインを特定の HTTP 要求にアタッチすると、その要求の発行前に PreRequest イベントが発生し、応答の受信後に PostRequest が起動します。

カスタマイズされた Web パフォーマンス テスト要求プラグインは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin> 基底クラスから独自のクラスを派生することによって作成できます。

カスタマイズされた Web パフォーマンス テスト要求プラグインは、記録した Web パフォーマンス テストで使用できます。 カスタマイズした Web パフォーマンス テスト要求プラグインを使用すると、最小限のコードを記述するだけで、Web パフォーマンス テストをより高度に制御できるようになります。 ただし、コード化された Web パフォーマンス テストでそれらを使用することもできます。 [コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)に関するページを参照してください。

## <a name="to-create-a-request-level-plug-in"></a>要求レベルのプラグインを作成するには

1. **ソリューション エクスプローラー**で、ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. 新しい**クラス ライブラリ** プロジェクトを作成します。

3. **ソリューション エクスプローラー**で、新しいクラス ライブラリの **[参照設定]** フォルダーを右クリックし、 **[参照の追加]** を選択します。

     **[参照の追加]** ダイアログ ボックスが表示されます。

4. **[.NET]** タブをクリックします。スクロール ダウンし、 **[Microsoft.VisualStudio.QualityTools.WebTestFramework]** を選択して、 **[OK]** をクリックします。

     **Microsoft.VisualStudio.QualityTools.WebTestFramework** への参照が**ソリューション エクスプローラー**内の **[参照設定]** フォルダーに追加されます。

5. **ソリューション エクスプローラー**で、Web パフォーマンス テスト要求のテスト プラグインの追加先であるロード テストを含んでいる Web パフォーマンスとロード テスト プロジェクトの最上位ノードを右クリックします。 **[参照の追加]** をクリックします。

     **[参照の追加]** ダイアログ ボックスが表示されます。

6. **[プロジェクト]** タブ、 **[クラス ライブラリ プロジェクト]** 、 **[OK]** の順に選択します。

7. **コード エディター**で、プラグインのコードを記述します。 まず、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin> クラスから派生する新しいパブリック クラスを作成します。

8. <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin.PreRequest*> イベント ハンドラーと <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin.PostRequest*> イベント ハンドラーのいずれかまたは両方にコードを実装します。 実装のサンプルについては、次の例を参照してください。

9. このコードを記述した後で、新しいプロジェクトをビルドします。

10. 要求プラグインを追加する Web パフォーマンス テストを開きます。

11. 要求プラグインを追加する要求を右クリックし、 **[要求プラグインの追加]** をクリックします。

     **[Web テスト要求プラグインの追加]** ダイアログ ボックスが表示されます。

12. **[プラグインの選択]** で、新しいプラグインを選択します。

13. **[選択したプラグインのプロパティ]** ペインで、実行時に使用するプラグインの初期値を設定します。

    > [!NOTE]
    > プラグインのプロパティをパブリック、設定可能、および基本型 (整数型、ブール型、文字列型など) として設定して、任意の数だけ公開できます。 Web パフォーマンス テスト プラグインのプロパティは、後で [プロパティ] ウィンドウを使用して変更することもできます。

14. **[OK]** をクリックします。

     プラグインは、HTTP 要求の子フォルダーである **[要求プラグイン]** フォルダーに追加されます。

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

次のコードを使用して、2 つのダイアログ ボックスを表示するカスタマイズされた Web パフォーマンス テスト プラグインを作成できます。 1 つのダイアログ ボックスには、要求アドインにアタッチする要求に関連付けられている URL が表示されます。 もう 1 つのダイアログ ボックスには、エージェントのコンピューター名が表示されます。

> [!NOTE]
> 次のコードでは、System.Windows.Forms への参照を追加する必要があります。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace RequestPluginNamespace
{
    public class MyWebRequestPlugin : WebTestRequestPlugin
    {
        public override void PostRequest(object sender, PostRequestEventArgs e)
        {
            MessageBox.Show(e.WebTest.Context.AgentName);
        }
        public override void PreRequest(object sender, PreRequestEventArgs e)
        {
            MessageBox.Show(e.Request.Url);
        }
    }
}
```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Web パフォーマンス テストのカスタム抽出規則のコーディング](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [Web パフォーマンス テストのカスタム検証規則のコーディング](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)
- [コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)
