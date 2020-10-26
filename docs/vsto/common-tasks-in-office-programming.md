---
title: Office プログラミングにおける一般的なタスク
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, getting started
- FAQs (frequently asked questions) [Office development in Visual Studio]
- Office development in Visual Studio, frequently asked questions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1b0856d3832d31dd7027b2f264dd0a9cd1d657ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "63007328"
---
# <a name="common-tasks-in-office-programming"></a>Office プログラミングにおける一般的なタスク
  このトピックは、Visual Studio を使用した Office ソリューションのプログラミングに共通する質問のうち、次のカテゴリの質問に対する回答を簡単に見つけることができるように構成されています。

- [セットアップタスクと一般的なタスク](#projects)。

- [ユーザーインターフェイスのカスタマイズタスク](#ui)。

- [Excel の自動化タスク](#excel)。

- [Word の自動化タスク](#word)。

- [データタスク](#data)。

- [サーバー側のドキュメント管理タスク](#server)。

- [セキュリティタスク](#security)。

- [配置タスク](#deployment)

## <a name="setup-and-general-tasks"></a><a name="projects"></a> セットアップと一般的なタスク

- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)。

- [方法: Office ソリューションをアップグレードする](https://msdn.microsoft.com/a269e539-b717-4680-a568-2152b070347e)。

- [方法: Office プライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)。

- [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)。

- [方法: Office プロジェクトでイベントハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)

- [方法: コードを実行せずに Office ソリューションを開く](../vsto/how-to-open-office-solutions-without-running-code.md)

- [方法: Office ソリューションの構成情報を設定する](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)。

- [方法: リボンに [開発] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)

- [方法: アドインのユーザーインターフェイスエラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)。

## <a name="user-interface-customization-tasks"></a><a name="ui"></a> ユーザーインターフェイスのカスタマイズタスク

### <a name="controls-on-documents-and-worksheets"></a>ドキュメントとワークシートのコントロール

- [方法: Office ドキュメントに Windows フォームコントロールを追加](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)する

- [方法: ワークシートに NamedRange コントロールを追加](../vsto/how-to-add-namedrange-controls-to-worksheets.md)する

- [方法: ワークシートに ListObject コントロールを追加](../vsto/how-to-add-listobject-controls-to-worksheets.md)する

- [方法: Office ドキュメントに Windows フォームコントロールを追加](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)する

- [方法: Word 文書にコンテンツコントロールを追加](../vsto/how-to-add-content-controls-to-word-documents.md)する

- [方法: Word 文書に Bookmark コントロールを追加](../vsto/how-to-add-bookmark-controls-to-word-documents.md)する

### <a name="task-panes-in-document-level-customizations"></a>ドキュメントレベルのカスタマイズの作業ウィンドウ

- [方法: Word 文書または Excel ブックに操作ウィンドウを追加](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)する

### <a name="task-panes-in-vsto-add-ins"></a>VSTO アドインの作業ウィンドウ

- [方法: アプリケーションにカスタム作業ウィンドウを追加](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)する

### <a name="ribbon-customizations"></a>リボンのカスタマイズ

- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)

- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)

- [方法: 組み込みタブをカスタマイズ](../vsto/how-to-customize-a-built-in-tab.md)する

- [方法: Backstage ビューにコントロールを追加](../vsto/how-to-add-controls-to-the-backstage-view.md)する

- [方法: リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)。

### <a name="outlook-form-regions"></a>Outlook フォーム領域

- [方法: フォーム領域を Outlook アドインプロジェクトに追加](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)する。

- [方法: Outlook でフォーム領域が表示されないように](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)する。

### <a name="custom-menus"></a>カスタムメニュー

- [方法: ショートカットメニューにコマンドを追加](../vsto/how-to-add-commands-to-shortcut-menus.md)する

## <a name="excel-automation-tasks"></a><a name="excel"></a> Excel の自動化タスク

- [方法: プログラムによってワークシートのセルに文字列を表示する](../vsto/how-to-programmatically-display-a-string-in-a-worksheet-cell.md)

- [方法: プログラムによって新しいブックを作成する](../vsto/how-to-programmatically-create-new-workbooks.md)

- [方法: プログラムによってブックを開き](../vsto/how-to-programmatically-open-workbooks.md)ます。

- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)。

- [方法: プログラムによってブックを閉じる](../vsto/how-to-programmatically-close-workbooks.md)

- [方法: プログラムによって新しいワークシートをブックに追加する](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)

- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)

- [方法: ブック内のワークシートをプログラムによって移動する](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)

- [方法: プログラムによってブックを保護する](../vsto/how-to-programmatically-protect-workbooks.md)

- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)。

- [方法: プログラムによってブック内の範囲にスタイルを適用](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)する。

- [方法: 選択したセルを含むワークシートの行の書式をプログラムによって変更する](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)

- [方法: プログラムによってワークシートの範囲内のテキストを検索する](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)

- [方法: プログラムによってワークシートを印刷する](../vsto/how-to-programmatically-print-worksheets.md)

- [方法: Excel の計算をプログラムで実行する](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)。

- [方法: ワークシート内のデータをプログラムによって並べ替え](../vsto/how-to-programmatically-sort-data-in-worksheets.md)ます。

## <a name="word-automation-tasks"></a><a name="word"></a> Word の自動化タスク

- [方法: プログラムによって新しいドキュメントを作成する](../vsto/how-to-programmatically-create-new-documents.md)。

- [方法: プログラムによって既存のドキュメントを開く](../vsto/how-to-programmatically-open-existing-documents.md)

- [方法: プログラムによって文書を保存する](../vsto/how-to-programmatically-save-documents.md)。

- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)

- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)。

- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)。

- [方法: Word 文書の範囲をプログラムによってリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)。

- [方法: プログラムによって文書内のテキストを書式設定する](../vsto/how-to-programmatically-format-text-in-documents.md)。

- [方法: Word 文書に XMLNode コントロールを追加](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)する

- [方法: プログラムによってブックマークのテキストを更新する](../vsto/how-to-programmatically-update-bookmark-text.md)。

- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)。

- [方法: プログラムによって文書を印刷する](../vsto/how-to-programmatically-print-documents.md)。

- [方法: プログラムによって Word の表を作成する](../vsto/how-to-programmatically-create-word-tables.md)

- [方法: プログラムによって Word の表に行と列を追加する](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)

- [方法: プログラムによって文書内の文字数をカウントする](../vsto/how-to-programmatically-count-characters-in-documents.md)。

## <a name="data-tasks"></a><a name="data"></a> データタスク

### <a name="data-bound-controls"></a>データ バインド コントロール

- [方法: データベースのデータをワークシートに読み込み](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)ます。

- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)

- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)

- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)

- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [方法: ホストコントロールのデータを使用してデータソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

### <a name="cached-data-in-document-level-solutions"></a>ドキュメントレベルのソリューションのキャッシュされたデータ

- [オフラインまたはサーバーで使用するデータをキャッシュする方法](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- [方法: Office ドキュメント内のデータソースをプログラムによってキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)。

- [方法: パスワードで保護されたドキュメント内のデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

### <a name="custom-xml-data"></a>カスタム XML データ

- [方法: ドキュメントレベルのカスタマイズにカスタム XML 部分を追加](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)する。

- [方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)

## <a name="server-side-document-management-tasks"></a><a name="server"></a> サーバー側のドキュメント管理タスク

- [方法: マネージコード拡張機能をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。

- [方法: マネージコード拡張機能をドキュメントにアタッチ](../vsto/how-to-attach-managed-code-extensions-to-documents.md)する。

## <a name="security-tasks"></a><a name="security"></a> セキュリティタスク

- [方法: Office ソリューションに署名](../vsto/how-to-sign-office-solutions.md)する。

## <a name="deployment-tasks"></a><a name="deployment"></a> 展開タスク

- [方法: ClickOnce を使用して Office ソリューションを発行する](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)。

- [方法: ClickOnce を使用してドキュメントレベルの Office ソリューションを SharePoint サーバーに発行](https://msdn.microsoft.com/2408e809-fb78-42a1-9152-00afa1522e58)する。

- [方法: ClickOnce Office ソリューションをインストール](https://msdn.microsoft.com/14702f48-9161-4190-994c-78211fe18065)する。

- [方法: Office ソリューションを実行するために、エンドユーザーのコンピューターに必須コンポーネントをインストール](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98)する。

- [方法: Office ソリューションの配置用に IIS を準備する](https://msdn.microsoft.com/f62bce70-81d4-4f8b-86e6-2f2afec5d9b4)

- [方法: 配置した Office ソリューションを更新する](https://msdn.microsoft.com/be96db53-b6ea-46ab-b8d9-b76b098b3b13)。

- [方法: Office ソリューションのインストールパスを変更する](https://msdn.microsoft.com/d0eaa07b-2d72-4902-899f-2f9fb165b8fd)。

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio で &#40;Office 開発を開始する&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
