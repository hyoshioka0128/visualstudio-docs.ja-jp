---
title: '方法: 診断データ アダプターを作成する'
description: Visual Studio を使用してクラス ライブラリを作成し、診断データ アダプター API を追加することで、診断データ アダプターを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- Diagnostic Data Adapter, creating
ms.assetid: bd7ad36c-54cb-4d2a-9aea-9d10ad98d7ba
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: b35444987686107b9ba2788392abde498661f3de
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945150"
---
# <a name="how-to-create-a-diagnostic-data-adapter"></a>方法: 診断データ アダプターを作成する

*診断データ アダプター* を作成するには、Visual Studio を使用してクラス ライブラリを作成し、Visual Studio Enterprise に用意されている診断データ アダプター API をクラス ライブラリに追加します。 テストの実行中に発生したイベントを処理するときに、フレームワークによって提供される <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink> に対し、ストリームまたはファイルとして情報を送信します。 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink> に送信したストリームまたはファイルは、テスト完了時点でテスト結果に対する添付ファイルとして保存されます。 テスト結果からバグを作成すると、または [!INCLUDE[mtrlong](../test/includes/mtrlong_md.md)] を使用すると、ファイルはバグにもリンクされます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

テストを実行するマシン、またはテスト対象のアプリケーションを実行するために使用している環境の一部を構成するマシンに影響を与える診断データ アダプターを作成できます。 たとえば、テストを実行するテスト マシンでのファイルの収集や、アプリケーションに対して Web サーバー ロールで実行されているマシンでのファイルの収集などが挙げられます。

診断データ アダプターにはフレンドリ名を設定できます。フレンドリ名は、Visual Studio を使用して、または Microsoft Test Manager (Visual Studio 2017 では非推奨) を使用してテスト設定を作成するときに表示されます。 テストの設定を使用すると、テストの実行時に、使用している環境下で、どのマシン ロールが特定の診断データ アダプターを実行するかを定義できます。 診断データ アダプターは、テストの設定を作成するときに構成することもできます。 たとえば、Web サーバーからカスタム ログを収集する診断データ アダプターを作成できます。 テストの設定を作成するとき、この Web サーバーの役割を実行しているマシン上でこの診断データ アダプターを実行するように選択できます。また、作成された最新の 3 つのログだけを収集するようにテストの設定の構成を変更できます。 テスト設定の詳細については、「[テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)」を参照してください。

イベントは、テストでイベントが発生した時点で診断データ アダプターがタスクを実行できるように、テストの実行時に発生します。

> [!IMPORTANT]
> これらのイベントは、特に複数のマシンでテストを実行する場合に、異なるスレッドで発生する可能性があります。 そのため、スレッドに関する問題が発生する可能性を認識し、カスタム アダプターの内部データが誤って破損しないようにする必要があります。 診断データ アダプターがスレッド セーフであることを確認してください。

診断データ アダプターを作成するときに使用できる主なイベントを次に示します。 診断データ アダプターのイベントの完全な一覧については、<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents> 抽象クラスを参照してください。

|event|説明|
|-|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.SessionStart>|テストの実行を開始します。|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.SessionEnd>|テストの実行を終了します。|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseStart>|テストの実行で各テストを開始します。|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseEnd>|テストの実行で各テストを終了します。|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestStepStart>|テストで各テスト ステップを開始します。|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestStepEnd>|テストで各テスト ステップを終了します。|

> [!NOTE]
> 手動テストが完了すると、これ以降、データ収集イベントは診断データ アダプターに送信されません。 テストを再実行すると、テスト ケース識別子が新しくなります。 ユーザーがテスト中にテストをリセットするか (<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseReset> イベントが発生します)、またはテスト ステップを変更すると、これ以降、データ コレクションイベントは診断データ アダプターに送信されません。ただし、テスト ケース識別子は変更されません。 テスト ケースがリセットされているかどうかを確認するには、診断データ アダプターでテスト ケース識別子を追跡する必要があります。

テストの設定を作成するときに構成した情報に基づいてデータ ファイルを収集する診断データ アダプターを作成するには、次の手順に従って操作します。

カスタムの構成エディターを含む、診断データ アダプター プロジェクトのサンプル全体については、「[診断データ アダプター作成用のサンプル プロジェクト](../test/quickstart-create-a-load-test-project.md)」を参照してください。

## <a name="create-and-install-a-diagnostic-data-adapter"></a>診断データ アダプターを作成してインストールする

1. 新しい **クラス ライブラリ** プロジェクトを作成します。

2. アセンブリ **Microsoft.VisualStudio.QualityTools.ExecutionCommon** を追加します。

   1. **ソリューション エクスプローラー** で、 **[参照]** を右クリックし、 **[参照の追加]** コマンドを選択します。

   2. **[.NET]** を選択し、**Microsoft.VisualStudio.QualityTools.ExecutionCommon.dll** を探します。

   3. **[OK]** をクリックします。

3. アセンブリ **Microsoft.VisualStudio.QualityTools.Common** を追加します。

   1. **ソリューション エクスプローラー** で、 **[参照]** を右クリックし、 **[参照の追加]** コマンドを選択します。

   2. **[/.NET]** を選択し、**Microsoft.VisualStudio.QualityTools.Common.dll** を探します。

   3. **[OK]** をクリックします。

4. クラス ファイルに次の `using` ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.TestTools.Common;
   using Microsoft.VisualStudio.TestTools.Execution;
   using System.Linq;
   using System.Text;
   using System.Xml;
   using System;
   ```

5. 診断データ アダプター用のクラスに <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorTypeUriAttribute> を追加して、診断データ アダプターとして識別します。このとき、**Company**、**Product**、および **Version** を診断データ アダプターに応じた情報に置き換えます。

   ```csharp
   [DataCollectorTypeUri("datacollector://Company/Product/Version")]
   ```

6. クラスに <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorFriendlyNameAttribute> 属性を追加して、パラメーターを診断データ アダプターに応じた情報に置き換えます。

   ```csharp
   [DataCollectorFriendlyName("Collect Log Files", false)]
   ```

    テストの設定アクティビティに表示名が表示されます。

   > [!NOTE]
   > また、<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationEditorAttribute> を追加して、このデータ アダプターのカスタム構成エディターの `Type` を指定し、必要に応じて、エディターに使用するヘルプ ファイルを指定できます。
   >
   > また、<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorEnabledByDefaultAttribute> を適用し、常に有効にすべきであることを指定できます。

7. 診断データ アダプターのクラスは、次のように、<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector> クラスから継承する必要があります。

   ```csharp
   public class MyDiagnosticDataAdapter : DataCollector
   ```

8. 次のように、ローカル変数を追加します。

   ```csharp
   private DataCollectionEvents dataEvents;
   private DataCollectionLogger dataLogger;
   private DataCollectionSink dataSink;
   private XmlElement configurationSettings;
   ```

9. <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector.Initialize*> メソッドと **Dispose** メソッドを追加します。 `Initialize` メソッドでは、次のように、データ シンクおよびテストの設定の構成データを初期化し、使用するイベント ハンドラーを登録します。

    ```csharp
    public override void Initialize(
        XmlElement configurationElement,
        DataCollectionEvents events,
        DataCollectionSink sink,
        DataCollectionLogger logger,
        DataCollectionEnvironmentContext environmentContext)
    {
           dataEvents = events;  // The test events
           dataLogger = logger;  // The error and warning log
           dataSink = sink;      // Saves collected data
           // Configuration from the test settings
           configurationSettings = configurationElement;

           // Register common events for the data collector
           // Not all of the events are used in this class
        dataEvents.SessionStart +=
            new EventHandler<SessionStartEventArgs>(OnSessionStart);
        dataEvents.SessionEnd +=
            new EventHandler<SessionEndEventArgs>(OnSessionEnd);
        dataEvents.TestCaseStart +=
            new EventHandler<TestCaseStartEventArgs>(OnTestCaseStart);
        dataEvents.TestCaseEnd +=
            new EventHandler<TestCaseEndEventArgs>(OnTestCaseEnd);
    }

    public override void Dispose(bool disposing)
    {
        if (disposing)
        {
            // Unregister the registered events
            dataEvents.SessionStart -=
                new EventHandler<SessionStartEventArgs>(OnSessionStart);
            dataEvents.SessionEnd -=
                new EventHandler<SessionEndEventArgs>(OnSessionEnd);
            dataEvents.TestCaseStart -=
                new EventHandler<TestCaseStartEventArgs>(OnTestCaseStart);
            dataEvents.TestCaseEnd -=
                new EventHandler<TestCaseEndEventArgs>(OnTestCaseEnd);
        }
    }
    ```

10. 次のようなイベント ハンドラー コードとプライベート メソッドを使用して、テスト中に生成されるログ ファイルを収集します。

    ```csharp
    public void OnTestCaseEnd(sender, TestCaseEndEventArgs e)
    {
        // Get any files to be collected that are
        // configured in your test settings
        List<string> files = getFilesToCollect();

        // For each of the files, send the file to the data sink
        // which will attach it to the test results or to a bug
        foreach (string file in files)
        {
            dataSink.SendFileAsync(e.Context, file, false);
        }
    }

    // A private method that returns the file names
    private List<string> getFilesToCollect()
    {
        // Get a namespace manager with our namespace
        XmlNamespaceManager nsmgr =
            new XmlNamespaceManager(
                configurationSettings.OwnerDocument.NameTable);
        nsmgr.AddNamespace("ns",
            "http://MyCompany/schemas/MyDataCollector/1.0");

        // Find all of the "File" elements under our configuration
        XmlNodeList files =
            configurationSettings.SelectNodes(
                "//ns:MyDataCollector/ns:File");

        // Build the list of files to collect from the
        // "FullPath" attributes of the "File" nodes.
        List<string> result = new List<string>();
        foreach (XmlNode fileNode in files)
        {
            XmlAttribute pathAttribute =
                fileNode.Attributes["FullPath"];
            if (pathAttribute != null &&
                !String.IsNullOrEmpty(pathAttribute.Value))
            {
                result.Add(pathAttribute.Value);
            }
        }

        return result;
    }
    ```

     これらのファイルは、テスト結果に添付されます。 これらのテスト結果からバグを作成する場合、または[!INCLUDE[mtrlong](../test/includes/mtrlong_md.md)]を使用する場合、ファイルはバグにも添付されます。

     独自のエディターを使用してデータを収集し、テストの設定に使用する場合は、「[方法:診断データ アダプター用のデータのカスタム エディターを作成する](../test/quickstart-create-a-load-test-project.md)」を参照してください。

11. テストが終了したときに、ユーザーによるテストの設定の構成に基づいてログ ファイルを収集するには、*App.config* ファイルを作成し、ソリューションに追加する必要があります。 このファイルは次の形式で作成し、識別するために診断データ アダプターの URI が含まれる必要があります。 "Company/ProductName/Version" を実際の値に置き換えてください。

    > [!NOTE]
    > 診断データ アダプターの情報を構成する必要がない場合は、構成ファイルを作成する必要はありません。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <configSections>
        <section name="DataCollectorConfiguration" type="Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationSection, Microsoft.VisualStudio.QualityTools.ExecutionCommon, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a "/>
      </configSections>
      <DataCollectorConfiguration xmlns="http://microsoft.com/schemas/VisualStudio/TeamTest/2010">
        <DataCollector typeUri="datacollector://MyCompany/MyProduct/1.0">
          <DefaultConfiguration>
            <!-- Your default config settings -->
            <Binaries>
              <Binary FullPath="C:\Example\Example.dll"/>
              <Binary FullPath="\\Server2\Example2.dll"/>
            </Binaries>
            <Symbols>
              <Symbol FullPath="\\ExampleServer\ExampleSymbol.pdb"/>
            </Symbols>
          </DefaultConfiguration>
        </DataCollector>
      </DataCollectorConfiguration>
    </configuration>
    ```

    > [!NOTE]
    > 既定の構成要素には必要なデータを含めることができます。 テストの設定で診断データ アダプターを構成しなかった場合は、実行時に既定のデータが診断データ アダプターに渡されます。 `<DefaultConfigurations>` セクションに追加する XML は、宣言されたスキーマの一部となる可能性が少ないため、生成される XML エラーを無視できます。
    >
    > インストール ディレクトリに基づく構成ファイルの他の例は、次のパス内にあります。*Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\DataCollectors*。

     テストの実行時に環境を使用するようにテストの設定を構成する方法の詳細については、[手動テストで診断データを収集する方法 (Azure Test Plans) ](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts&preserve-view=true)に関するページを参照してください。

     構成ファイルのインストールの詳細については、[カスタム診断データ アダプターをインストールする方法](../test/quickstart-create-a-load-test-project.md)に関するページを参照してください。

12. ソリューションをビルドして、診断データ アダプターのアセンブリを作成します。

13. カスタム エディターのインストールの詳細については、[カスタム診断データ アダプターをインストールする方法](../test/quickstart-create-a-load-test-project.md)に関するページを参照してください。

14. テストの実行時に環境を使用するようにテストの設定を構成する方法の詳細については、[手動テストで診断データを収集する方法 (Azure Test Plans) ](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts&preserve-view=true)に関するページを参照してください。

15. 診断データ アダプターを選択するには、まず既存のテスト設定を選択するか、Visual Studio から、または Microsoft Test Manager (Visual Studio 2017 では非推奨) から新しく作成する必要があります。 アダプターは、テストの設定の **[データと診断]** タブに、クラスに割り当てた表示名と共に表示されます。

16. これらの設定を有効に設定します。 テスト設定の詳細については、「[テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)」を参照してください。

17. この診断データ アダプターを選択したテストの設定を使用して、テストを実行します。

    指定したデータ ファイルがテスト結果に関連付けられます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationEditorAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorTypeUriAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorFriendlyNameAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorEnabledByDefaultAttribute>
- [テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)
- [手動テストでの診断データの収集 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts&preserve-view=true)
- [テスト中の診断データの収集 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts&preserve-view=true)
- [方法: 診断データ アダプター用のデータのカスタム エディターを作成する](../test/quickstart-create-a-load-test-project.md)
