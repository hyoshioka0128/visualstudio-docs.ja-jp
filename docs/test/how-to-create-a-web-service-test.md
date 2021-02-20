---
title: Web サービス テストを作成する
description: Web サービスのパフォーマンス テストを使用し、Web パフォーマンス テスト エディターで要求をカスタマイズして Web サービス ページを見つける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/30/2020
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, creating Web service tests
- Web services [Visual Studio ALM], creating
- service tests, Web
ms.assetid: fbcd57ee-06ad-4260-8694-09f8e0f93e39
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: 2d368ca7cbe64f2c0e8c8dc5e18e5f3c7145274c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949845"
---
# <a name="how-to-create-a-web-service-test"></a>方法: Web サービス テストを作成する

Web パフォーマンス テストを使用して、Web サービスをテストできます。 **[要求の挿入]** オプションおよび **[Web サービス要求の挿入]** オプションを使用すると、**Web パフォーマンス テスト エディター** にある個々の要求を Web サービス ページに移動するようにカスタマイズできます。 通常、Web アプリケーションでは、これらのページは表示されません。 そのため、これらのページへアクセスできるように要求をカスタマイズする必要があります。

>[!NOTE]
> Web パフォーマンスとロード テスト機能は、Visual Studio 2019 では非推奨になりました。 Application Insights の場合、複数ステップ Web テストは、Visual Studio の Web テスト ファイルに依存します。 Visual Studio 2019 が Web テスト機能を備えた最後のバージョンとなることが[発表](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)されました。 新しい機能は追加されませんが、Visual Studio 2019 の Web テスト機能は現在もサポートされており、製品のサポート ライフサイクルの間は引き続きサポートされることを理解しておくことが重要です。 Azure Monitor 製品チームでは、複数ステップ可用性テストの今後に関するご質問に対して、[こちら](https://github.com/MicrosoftDocs/azure-docs/issues/26050#issuecomment-468814101)で回答しています。

**必要条件**

Visual Studio Enterprise

## <a name="to-create-a-simple-web-service"></a>簡単な Web サービスを作成するには

テストするには、独自の Web サービスを使用するか、Visual Studio に含まれている基本的な Web サービス (ASMX) テンプレートを使用します。 このテンプレートを使用して簡単な Web サービスを作成するには、次を実行します。

1. Visual Studio で、ASP.NET Web アプリケーション (.NET Framework) テンプレートを使用して新しいプロジェクトを作成し、メッセージが表示されたら、**空の** テンプレートを選択します。 名前を入力してプロジェクトを作成します。

1. ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、 **[追加]**  >  **[新しい項目]** の順に選択して、 **[Web サービス (ASMX)]** を選択します。 Web サービスを追加します。

1. *WebService1.asmx* を開き、既定の `HelloWorld` Web メソッドを次のコードに置き換えます。

   ```csharp
   public string HelloWorld(string str)
   {
      return "Hello, " + str;
   }
   ```

## <a name="install-the-load-testing-component"></a>ロード テスト コンポーネントをインストールする

Web パフォーマンスとロード テスト ツール コンポーネントをまだインストールしていない場合、Visual Studio インストーラーでインストールする必要があります。

1. Windows の **[スタート]** メニューから **Visual Studio インストーラー** を開きます。 このインストーラーには Visual Studio の [新しいプロジェクト] ダイアログ ボックスからアクセスしたり、メニュー バーで **[ツール]**  >  **[ツールと機能を取得]** の順に選択してアクセスしたりすることもできます。

1. **Visual Studio インストーラー** で **[個々のコンポーネント]** タブを選択し、下にスクロールして **[デバッグとテスト]** セクションを表示します。 **[Web パフォーマンスとロード テスト ツール]** を選択します。

   ![Web パフォーマンスとロード テスト ツール コンポーネント](media/web-perf-load-testing-tools-component.png)

1. **[変更]** ボタンを選択します。

   Web パフォーマンスとロード テスト ツール コンポーネントがインストールされます。

## <a name="create-a-web-test-project"></a>Web テスト プロジェクトを作成する

Web テストでは、[Web パフォーマンスとロード テストのプロジェクト] プロジェクト テンプレートが必要です。 このセクションでは、C# ロード テスト プロジェクトを作成します。 Visual Basic のロード テスト プロジェクトがよければ、そちらを作成することもできます。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

   サンプル Web サービス (ASMX) テンプレートを使用している場合は、同じソリューションに Web テスト プロジェクトを追加できます。

2. メニュー バーから、 **[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択します。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[インストール済み]** 、 **[Visual C#]** の順に展開し、 **[テスト]** カテゴリを選択します。 **[Web パフォーマンスとロード テストのプロジェクト]** テンプレートを選択します。

   ![[Web パフォーマンスとロード テストのプロジェクト] のテンプレート](media/web-perf-load-test-project-template.png)

4. 既定の名前を使用しない場合、プロジェクトの名前を入力し、 **[OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

   サンプル Web サービス (ASMX) テンプレートを使用している場合は、同じソリューションに Web テスト プロジェクトを追加できます。

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**Web テスト**」と入力し、C# 用の **[Web パフォーマンスとロード テストのプロジェクト \[非推奨]]** テンプレートを選択します。 **[次へ]** をクリックします。

4. 既定の名前を使用しない場合は、プロジェクトの名前を入力し、 **[作成]** を選択します。

::: moniker-end

   Visual Studio によってプロジェクトが作成され、**ソリューション エクスプローラー** にファイルが表示されます。 このプロジェクトには最初の段階で、「*WebTest1.webtest*」という名前の Web テスト ファイルが 1 つ含まれています。

## <a name="to-test-a-web-service"></a>Web サービスをテストするには

1. Web サービスを開始し、必要に応じて **[停止]** を選択して、サービスを一時停止します。

1. Web テスト プロジェクトで、*WebTest1.webtest* を開きます。これにより、Web パフォーマンス テスト エディターが開きます。 このテスト エディターで、Web パフォーマンス テストを右クリックし、 **[Web サービス要求の追加]** を選択します。

1. 新しい要求の **[URL]** のプロパティで、 **https://localhost:44318/WebService1.asmx** などの Web サービスの名前を入力します。

1. Web サービスについては、ブラウザーの別のセッションを開き、 **[アドレス]** ツール バーに *.asmx* ページの URL を入力します。 Web ページの先頭で、テストするメソッドを選択して、SOAP メッセージを調べます。 (Web サービスの例のメソッドは HelloWorld です。)メソッドを開くと、`SOAPAction` が含まれていることがわかります。

1. **Web パフォーマンス テスト エディター** で、要求を右クリックし、 **[ヘッダーの追加]** を選択して新しいヘッダーを追加します。 **[名前]** プロパティに「`SOAPAction`」と入力します。 **[値]** プロパティで、`SOAPAction` に表示される値 ( *http://tempuri.org/HelloWorld* など) を入力します。

1. テスト エディターで URL ノードを展開し、 **[文字列ボディ]** ノードを選択して、 **[コンテンツの種類]** プロパティの値として「`text/xml`」と入力します。

1. 手順 4 のブラウザーに戻り、[Web サービスの説明] ページから SOAP 要求の XML 部分を選択し、クリップボードにコピーします。

   次に示すのは、XML の内容の一例です。

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
       <soap:Body>
         <HelloWorld xmlns="http://tempuri.org/">
           <str>string</str>
         </HelloWorld>
       </soap:Body>
     </soap:Envelope>
     ```

1. Web パフォーマンス テスト エディターに戻り、 **[文字列ボディ]** プロパティで省略記号 **(…)** を選択します。 クリップボードの内容をプロパティに貼り付けます。

1. テストを成功させるためには、XML のプレースホルダー値を有効な値に置き換えます。 前の例では、`string` のインスタンスを名前に置き換えます。

1. Web サービス要求を右クリックし、 **[URL QueryString パラメーターの追加]** を選択します。

1. クエリ文字列パラメーターに名前と値を代入します。 前の例では、名前は `op` となり、値は `HelloWorld` となります。 これは、実行される Web サービスの操作を識別します。

    > [!NOTE]
    > SOAP 本体のデータ バインディングを使用すると、`{{DataSourceName.TableName.ColumnName}}` 構文を使用して、プレースホルダー値をデータ バインディングされた値に置き換えることができます。

1. テストを実行します。 **Web パフォーマンス テスト結果ビューアー** の上部ペインで、Web サービス要求を選択します。 下部ペインで、 **[Web ブラウザー]** タブを選択します。Web サービスによって返された XML とあらゆる操作の結果とが表示されます。

   Web サービス要求の結果を検索します。

## <a name="see-also"></a>関連項目

- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
