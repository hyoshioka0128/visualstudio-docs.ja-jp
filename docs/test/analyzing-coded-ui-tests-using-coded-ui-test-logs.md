---
title: コード化された UI テスト ログを使用したコード化された UI テストの分析
description: コード化された UI テスト ログについて説明します。これにより、コード化された UI テストの実行に関する重要な情報をフィルター処理して記録できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 3dcbb1bdfd89ae13df5174b6502dc6e89437a468
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95442496"
---
# <a name="analyzing-coded-ui-tests-using-coded-ui-test-logs"></a>コード化された UI テスト ログを使用したコード化された UI テストの分析

コード化された UI テスト ログは、コード化された UI テストの実行に関する重要な情報にフィルターを適用して記録します。 問題をすばやくデバッグできるような形式で、ログが表示されます。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="step-1-enable-logging"></a>手順 1: ログ記録を有効にする

シナリオに応じて、以下のいずれかのメソッドを使用してログを有効にします。

- テスト プロジェクトに *App.config* ファイルが存在しない場合:

   1. テストを実行すると起動される *QTAgent\*.exe* プロセスを判断します。 これを行う方法の 1 つは、Windows **タスク マネージャー** の **[詳細]** タブを観察することです。

   2. *%ProgramFiles(x86)%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE* フォルダーから、対応する *.config* ファイルを開きます。 たとえば、実行しているプロセスが *QTAgent_40.exe* である場合、*QTAgent_40.exe.config* を開きます。

   2. **EqtTraceLevel** の値を、目的のログ レベルに変更します。

      ```xml
      <!-- You must use integral values for "value".
           Use 0 for off, 1 for error, 2 for warn, 3 for info, and 4 for verbose. -->
      <add name="EqtTraceLevel" value="4" />
      ```

   3. ファイルを保存します。

- テスト プロジェクトに *App.config* ファイルが存在する場合:

  - *App.config* ファイルをプロジェクトで開き、構成ノードに次のコードを追加します。

    ```xml
    <system.diagnostics>
      <switches>
        <add name="EqtTraceLevel" value="4" />
      </switches>
    </system.diagnostics>`
    ```

- テスト コード自体からログを有効にする。

   ```csharp
   Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.LoggerOverrideState = HtmlLoggerState.AllActionSnapshot;
   ```

## <a name="step-2-run-your-coded-ui-test-and-view-the-log"></a>手順 2: コード化された UI テストを実行してログを表示する

*QTAgent\*.exe.config* ファイルに変更を加えてコード化された UI テストを実行すると、**テスト エクスプローラー** の結果に、出力リンクが表示されます。 トレース レベルが **verbose** に設定されていると、ログ ファイルはテストが失敗した場合だけでなく、テストが成功した場合にも生成されます。

1. **[テスト]** メニューの **[ウィンドウ]** を選択し、 **[テスト エクスプローラー]** を選択します。

2. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

3. **テスト エクスプローラー** で、実行するコード化された UI テストを選択し、ショートカット メニューを開いて **[選択したテストの実行]** を選択します。

     自動テストが実行され、成功したか失敗したかが示されます。

    > [!TIP]
    > **テスト エクスプローラー** を表示するには、**[テスト]**、**[Windows]** の順に選択し、**[テスト エクスプローラー]** を選択します。

4. **テスト エクスプローラー** の結果で、**[出力]** リンクを選択します。

     ![テスト エクスプローラーの出力リンク](../test/media/cuit_htmlactionlog1.png)

     この操作によって表示されるテストの出力に、操作ログへのリンクが含まれています。

     ![コード化された UI テストからの結果と出力リンク](../test/media/cuit_htmlactionlog2.png)

5. *UITestActionLog.html* リンクを選択します。

     Web ブラウザーにログが表示されます。

     ![コード化された UI テストのログ ファイル](../test/media/cuit_htmlactionlog3.png)

## <a name="see-also"></a>参照

- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [方法: Microsoft Visual Studio からテストを実行する](/previous-versions/ms182470(v=vs.140))