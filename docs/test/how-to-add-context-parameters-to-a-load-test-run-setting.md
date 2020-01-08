---
title: ロード テストの実行設定にコンテキスト パラメーターを追加する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, run settings, context parameters
- load tests, context parameters
ms.assetid: a8a0b97e-8040-4711-85ab-36548b130ed2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 05efbba005a9455af3b9d2e8755b580a8af30d0a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75584479"
---
# <a name="how-to-add-context-parameters-to-a-load-test-run-setting"></a>方法: ロード テストの実行設定にコンテキスト パラメーターを追加する

**新しいロード テスト ウィザード**でロード テストを作成した後、**ロード テスト エディター**を使用して、テストのニーズや目標に合わせてシナリオのプロパティを変更できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> 実行設定の各プロパティとその説明の一覧については、「[ロード テストの実行設定のプロパティ](../test/load-test-run-settings-properties.md)」を参照してください。

ロード テスト エディターを使用して、ロード テストの実行設定で使用するコンテキスト パラメーターを作成できます。 コンテキスト パラメーターを使用すると、文字列をパラメーター化できます。

たとえば、コンテキスト パラメーターを使用することにより、パラメーター化された Web サーバー URL を既に使用している Web パフォーマンス テストがロード テストに含まれるとします。 Web パフォーマンス テストで使用するものと同じ名前値を使用するロード テストの実行設定に、コンテキスト パラメーターを追加できます。 これにより、ロード テストの実行時に、Web パフォーマンス テストが別のサーバーに割り当てられます。 たとえば、URL. の Web サーバーが WebServer1 という名前になっているコンテキスト パラメーターを使用する Web パフォーマンス テストが、ロード テストに含まれているとします。 そこで WebServer1 という名前が使用されているコンテキスト パラメーターを、ロード テストの実行設定に指定した場合、このロード テストでは、ロード テストの実行設定に割り当てたコンテキスト パラメーターが使用されます。 明確にするために、ロード テスト内の Web パフォーマンス テストで、ロード テキスト内と同じコンテキスト パラメーター名を使用する場合、そのロード テキスト内のコンテキスト パラメーターによって、Web パフォーマンス テストで使用されるコンテキスト パラメーターはオーバーライドされます。

> [!WARNING]
> 実行設定にコンテキスト パラメーターを使用するときは、Web パフォーマンス テストのコンテキスト パラメーターを誤ってオーバーライドしないように注意してください。 意図的に行う場合以外は、同じコンテキスト パラメーター名を使用しないようにしてください。

Webserver1 コンテキスト パラメーターの値を `http://CorporateStagingWebServer` に割り当てた場合は、そのロード テスト全体で `WebServer1` を使用できるので、この値を別の Web サーバーにいつでも簡単に変更できます。

また、別々のロード テストの実行設定に同じ名前を使用して、コンテキスト パラメーターにさまざまな値を割り当てることにより、さまざまな環境を使用してロード テストを実行できます。

- Corporate Staging Web Server の実行設定:`WebServer1=http://CorporateStagingWebServer` という名前のコンテキスト パラメーター

- Corporate Production Web Server の実行設定:`WebServer1=http://CorporateProductionWebServer` という名前のコンテキスト パラメーター

  **コマンド ラインからの実行設定の変更**

  コンテキスト パラメーターの手法を活用するためにコマンド ラインから別の実行設定を使用する場合は、次のコマンドを使用します。

  **Set Test.UseRunSetting= CorporateStagingWebServer**

  および

  **mstest /testcontainer:loadtest1.loadtest**

## <a name="to-add-a-context-parameter-to-a-run-setting"></a>コンテキスト パラメーターを実行設定に追加するには

1. ロード テストを開きます。

2. ロード テスト エディターで、ロード テスト ツリーの **[実行設定]** フォルダーを展開します。

3. コンテキスト パラメーターを追加する特定の実行設定を右クリックし、 **[コンテキスト パラメーターの追加]** を選択します。

     新しいコンテキスト パラメーターが、ロード テスト ツリーの **[実行設定]** フォルダーの **[コンテキスト パラメーター]** フォルダーに追加されます。

     \- または -

     実行設定に **[コンテキスト パラメーター]** フォルダーが既に含まれている場合は、それを右クリックして **[コンテキスト パラメーターの追加]** を選択します。

4. **[プロパティ]** ウィンドウで、必要に応じて、 **[名前]** の値を変更 (WebServer1 など) します。 **[プロパティ]** ウィンドウの **[値]** を、使用するパラメーター (`http://CorporateStagingWebServer` など) に変更します。

5. (省略可能) 手順 3. から 5. を繰り返し、 **[値]** に別の文字列 (`http://CorporateProductionWebServer` など) を使用します。

6. どの実行設定をアクティブにするかを選択します。 実行設定のショートカット メニューを開いて **[アクティブとして設定]** を選択します。

## <a name="see-also"></a>関連項目

- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
