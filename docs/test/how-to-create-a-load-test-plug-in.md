---
title: ロード テスト プラグインを作成する
ms.date: 10/19/2016
ms.topic: how-to
f1_keywords:
- vs.test.load.loadtestplugin
helpviewer_keywords:
- code, load tests
- plug-ins, load test
- load tests, plug-ins
ms.assetid: 27806972-1b15-4388-833d-6d0632816f1f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0abcc3865c21a4f4673331377af8d17b223c7875
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288027"
---
# <a name="how-to-create-a-load-test-plug-in"></a>方法: ロード テスト プラグインを作成する

ロード テスト プラグインを作成すると、ロード テストを実行するときに、さまざまな時間にコードを実行できます。 プラグインを作成して、ロード テストの組み込みの機能を拡張または変更します。 たとえば、ロード テスト プラグインのコードを作成して、ロード テストの実行中にロード テストのパターンを設定または変更できます。 これを行うには、<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> インターフェイスを継承するクラスを作成する必要があります。 このクラスは、このインターフェイスの <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin.Initialize*> メソッドを実装する必要があります。 詳細については、「<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>」を参照してください。

> [!TIP]
> Web パフォーマンス テスト用のプラグインを作成することもできます。 詳細については、「[方法:Web パフォーマンス テスト プラグインを作成する](../test/how-to-create-a-web-performance-test-plug-in.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

<!-- markdownlint-disable MD003 MD020 -->
## <a name="to-create-a-load-test-plug-in-in-c"></a>C# でロード テスト プラグインを作成するには
<!-- markdownlint-enable MD003 MD020 -->

1. Web パフォーマンス テストが含まれている、Web パフォーマンスとロード テストのプロジェクトを開きます。

2. ロード テストをテスト プロジェクトに追加して、Web パフォーマンス テストを実行するように構成します。

     詳細については、「[クイック スタート:ロード テスト プロジェクトを作成する](../test/quickstart-create-a-load-test-project.md)」を参照してください。

3. 新しい**クラス ライブラリ** プロジェクトをソリューションに追加します (**ソリューション エクスプローラー**で、ソリューションを右クリックし、 **[追加]** を選択して、 **[新しいプロジェクト]** を選択します)。

4. **ソリューション エクスプローラー**で、新しいクラス ライブラリの **[参照設定]** フォルダーを右クリックし、 **[参照の追加]** を選択します。

   **[参照の追加]** ダイアログ ボックスが表示されます。

5. **[.NET]** タブを選択します。スクロール ダウンし、 **[Microsoft.VisualStudio.QualityTools.LoadTestFramework]** を選択します。

6. **[OK]** をクリックします。

   **Microsoft.VisualStudio.QualityTools.LoadTestFramework** への参照が**ソリューション エクスプローラー**の **[参照設定]** フォルダーに追加されます。

7. **ソリューション エクスプローラー**で、ロード テスト プラグインの追加先であるロード テストを含んでいる Web パフォーマンスおよびロード テスト プロジェクトの最上位ノードを右クリックし、 **[参照の追加]** を選択します。

   **[参照の追加]** ダイアログ ボックスが表示されます。

8. **[プロジェクト]** タブをクリックし、[クラス ライブラリ プロジェクト] を選択します。

9. **[OK]** をクリックします。

10. **コード エディター**で、<xref:Microsoft.VisualStudio.TestTools.LoadTesting> 名前空間について `using` ステートメントを追加します。

11. クラス ライブラリ プロジェクトで作成されたクラスに対して、<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> インターフェイスを実装します。 実装のサンプルについては、次の例を参照してください。

12. このコードを記述した後で、新しいプロジェクトをビルドします。

13. ロード テストの最上位ノードを右クリックし、 **[ロード テスト プラグインの追加]** を選択します。

     **[ロード テスト プラグインの追加]** ダイアログ ボックスが表示されます。

14. **[プラグインの選択]** で、ロード テスト プラグイン クラスを選択します。

15. **[選択したプラグインのプロパティ]** ペインで、実行時に使用するプラグインの初期値を設定します。

    > [!NOTE]
    > プラグインのプロパティをパブリック、設定可能、および基本型 (整数型、ブール型、文字列型など) として設定して、任意の数だけ公開できます。 Web パフォーマンス テスト プラグインのプロパティは、後で **[プロパティ]** ウィンドウを使用して変更することもできます。

16. **[OK]** をクリックします。

     **[ロード テスト プラグイン]** フォルダーにプラグインが追加されます。

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

LoadTestFinished イベントが発生した後でカスタム コードを実行するロード テスト プラグインを次のコードに示します。 このコードがリモート コンピューターのテスト エージェントで実行され、テスト エージェントにローカル ホスト SMTP サービスがない場合、メッセージ ボックスが開いているためにロード テストの状態は "処理中" のままです。

> [!NOTE]
> 次のコードでは、System.Windows.Forms への参照を追加する必要があります。

```csharp
using System;
using Microsoft.VisualStudio.TestTools.LoadTesting;
using System.Net.Mail;
using System.Windows.Forms;

namespace LoadTestPluginTest
{
    public class MyLoadTestPlugin : ILoadTestPlugin
    {
        LoadTest myLoadTest;

        public void Initialize(LoadTest loadTest)
        {
            myLoadTest = loadTest;
            myLoadTest.LoadTestFinished += new
                EventHandler(myLoadTest_LoadTestFinished);
        }

        void myLoadTest_LoadTestFinished(object sender, EventArgs e)
        {
            try
            {
                // place custom code here
                MailAddress MyAddress = new MailAddress("someone@example.com");
                MailMessage MyMail = new MailMessage(MyAddress, MyAddress);
                MyMail.Subject = "Load Test Finished -- Admin Email";
                MyMail.Body = myLoadTest..Name + " has finished.";

                SmtpClient MySmtpClient = new SmtpClient("localhost");
                MySmtpClient.Send(MyMail);
            }

            catch (SmtpException ex)
            {
                MessageBox.Show(ex.InnerException.Message +
                    ".\r\nMake sure you have a valid SMTP.", "LoadTestPlugin", MessageBoxButtons.OK, MessageBoxIcon.Warning, MessageBoxDefaultButton.Button1);
            }
        }
    }
}
```

8 個のイベントがロード テストに関連付けられており、これらをロード テスト プラグインが処理することで、ロード テストでカスタム コードが実行されます。 次に示すイベントを使用して、ロード テストの実行のさまざまな時間にアクセスできます。

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestStarting>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestFinished>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestWarmupComplete>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestStarting>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestFinished>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.ThresholdExceeded>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.Heartbeat>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestAborted>

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [方法: Web パフォーマンス テスト プラグインを作成する](../test/how-to-create-a-web-performance-test-plug-in.md)
