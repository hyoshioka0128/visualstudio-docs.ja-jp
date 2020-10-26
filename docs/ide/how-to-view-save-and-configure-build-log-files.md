---
title: '方法: ビルド ログ ファイルを表示、保存、および構成する | Microsoft Docs'
ms.date: 08/28/2019
ms.technology: vs-ide-compile
ms.topic: how-to
ms.assetid: 75d38b76-26d6-4f43-bbe7-cbacd7cc81e7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4acf8ca4e116bfb0ab990f1b0aed66bef95820ad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85283906"
---
# <a name="how-to-view-save-and-configure-build-log-files"></a>方法: ビルド ログ ファイルを表示、保存、および構成する

Visual Studio IDE でプロジェクトをビルドしたら、 **[出力]** ウィンドウでそのビルドに関する情報を表示できます。 この情報を使用して、たとえば、ビルド エラーをトラブルシューティングできます。

- C++ のプロジェクトでは、プロジェクトのビルド時に作成および保存されたログ ファイルで同じ情報を確認することもできます。 

- マネージド コード プロジェクトでは、ビルド出力ウィンドウ内をクリックし、**Ctrl**+**S** キーを押します。 Visual Studio から、 **[出力]** ウィンドウの情報を保存するログ ファイルの場所を指定することを求められます。

また、IDE を使用すれば、各ビルドについて、表示する情報の種類を指定することもできます。

MSBuild を使用して任意の種類のプロジェクトをビルドする場合は、ビルドに関する情報を保存するログ ファイルを作成することができます。 詳細については、[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)に関するページを参照してください。

## <a name="to-view-the-build-log-file-for-a-c-project"></a>C++ プロジェクトのビルド ログ ファイルを表示するには

1. **エクスプローラー**または**エクスプローラー**で、次のファイルを開きます (プロジェクトのルート フォルダーの相対パスです)。*Release*\\<ProjectName>\>.Log* または *Debug\\<プロジェクト名\>.log*

## <a name="to-create-a-build-log-file-for-a-managed-code-project"></a>マネージ コード プロジェクトのビルド ログ ファイルを作成するには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

2. **[出力]** ウィンドウで、テキスト内のどこかをクリックします。

3. **Ctrl**+**S** を押します。

   Visual Studio から、ビルド出力を保存する場所を指定することを求められます。

`-fileLogger` (`-fl`) コマンド ライン オプションを使用して、コマンド ラインから直接 MSBuild を実行してログを生成することもできます。 「[MSBuild でのビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)」を参照してください。

## <a name="to-change-the-amount-of-information-included-in-the-build-log"></a>ビルド ログに含める情報の量を変更するには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

2. **[プロジェクトおよびソリューション]** ページで、 **[ビルド/実行]** ページを選択します。

3. **[MSBuild プロジェクト ビルドの出力の詳細]** の一覧で、次の値のいずれかを選択し、 **[OK]** ボタンを選択します。

    |詳細レベル|説明|
    | - |-----------------|
    |**非表示**|ビルドの概要のみを表示します。|
    |**最小限**|ビルドの概要と、重要度 - 高として分類されたエラー、警告、メッセージを表示します。|
    |**標準**|ビルドの概要と、重要度 - 高として分類されたエラー、警告、およびメッセージと、ビルドの主なステップとを表示します。 この詳細レベルを最も頻繁に使用します。|
    |**詳細**|ビルドの概要と、重要度 - 高として分類されたエラー、警告、およびメッセージと、ビルドのすべてのステップと、標準的な重要度として分類されたメッセージとを表示します。|
    |**診断**|ビルドで使用できるすべてのデータを表示します。 このレベルの詳細は、カスタム ビルド スクリプトの問題およびその他のビルドの問題をデバッグする場合に役に立ちます。|

     詳細については、「[[オプション] ダイアログ ボックス、[プロジェクトおよびソリューション]、[ビルド/実行]](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)」および「<xref:Microsoft.Build.Framework.LoggerVerbosity>」を参照してください。

    > [!IMPORTANT]
    > **[出力]** ウィンドウ (すべてのプロジェクト) と *\<ProjectName>.txt* ファイル (C++ プロジェクトのみ) に変更を反映するには、プロジェクトをリビルドする必要があります。

## <a name="use-binary-logs-to-make-it-easier-to-browse-large-log-files"></a>バイナリ ログを使用して、大きなログ ファイルを簡単に参照できるようにする

バイナリ ログは .NET プロジェクトのオプション機能です。これにより、ログ参照のエクスペリエンスが向上し、大きなログで情報を見つけやすくなります。 バイナリ ログを使用するには、[Project System Tools](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ProjectSystemTools) をインストールします。 詳細については、[https://msbuildlog.com](https://msbuildlog.com) および[バイナリ ログ](https://github.com/microsoft/msbuild/blob/master/documentation/wiki/Binary-Log.md)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
