---
title: codespace で Visual Studio を使用する (プレビュー)
description: Windows 開発向けの GitHub Codespaces で Visual Studio IDE を使用する方法について説明します。
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: add43a5d130d8938193774d50bb643f48ecc3f8c
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "104673048"
---
# <a name="how-to-use-visual-studio-with-a-codespace-preview"></a>codespace で Visual Studio を使用する方法 (プレビュー)

> [!Important] 
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 今後のプレビューとロードマップの情報のために、Visual Studio の[開発者コミュニティ フォーラム](https://developercommunity.visualstudio.com/home)に参加することをお勧めします。 

Visual Studio では、GitHub Codespaces での開発をサポートしています。 codespace を作成して接続し、Visual Studio の機能を最大限に活用して、リモートのホストされた環境でプロジェクトを操作できます。 ソース コードとツールが codespace にあり、コンパイルとデバッグがクラウドで行われている場合でも、開発エクスペリエンスは、ローカルで作業しているかのように高速でスムーズなものに感じるでしょう。

> [!NOTE]
> この記事では、Visual Studio を使用して GitHub Codespaces に接続する方法について具体的に説明します。 他のクライアントを使用して codespace に接続する方法については、[Visual Studio Code](https://docs.github.com/github/developing-online-with-codespaces/connecting-to-your-codespace-from-visual-studio-code) または [GitHub](https://docs.github.com/github/developing-online-with-codespaces/developing-in-a-codespace) のドキュメントを参照してください。

> [!NOTE]
> [Visual Studio 2019 Preview](https://aka.ms/vspreview) をまだインストールしていない場合は、[visualstudio.microsoft.com](https://aka.ms/vspreview) からダウンロードできます。

## <a name="enable-connect-to-github-codespaces"></a>GitHub Codespaces への接続を有効にする

Visual Studio 2019 Preview での GitHub Codespaces への接続は、既定では有効になっていないため、最初に [プレビュー機能] オプションを有効にする必要があります。

1. Visual Studio 2019 Preview では、 **[ツール]**  >  **[オプション]** のメニュー項目を使用して [オプション] ダイアログを開きます。

2. **[環境]** の下で **[プレビュー機能]** を選択し、**GitHub Codespaces への接続** のプレビュー機能をオンにします。

   ![GitHub Codespaces への接続のプレビュー機能をオンにする](media/connect-to-github-codespaces-preview-feature.png)

3. この機能を使用するには、Visual Studio を再起動する必要があります。

## <a name="create-a-codespace"></a>codespace を作成する

まだ codespace をお持ちでない場合は、Visual Studio から作成することができます。

1. Visual Studio を起動すると、スタート ウィンドウの [作業の開始] の下に **[Connect to a codespace]\(codespace に接続\)** ボタンが表示されます。

   ![Visual Studio のスタート ウィンドウと [Connect to a codespace]\(codespace に接続\)](media/visual-studio-start-window.png)

2. **[Connect to a codespace]\(codespace に接続\)** を選択すると、GitHub へのサインインを求めるメッセージが表示されます。 GitHub アカウントをまだお持ちでない場合は、作成することもできます。

   ![Visual Studio の [Sign in to GitHub]\(GitHub へのサインイン\)](media/visual-studio-sign-in-to-github.png)

   **[Sign in to GitHub]\(GitHub へのサインイン\)** を選択したら、オンライン GitHub のサインイン ワークフローに従います。

3. codespace を作成していない場合は、作成するよう求めるメッセージが表示されます。

   [Codespace details]\(codespace の詳細\) の下で、**リポジトリ URL** を指定する必要があります。 GitHub Codespaces により、指定されたリポジトリの作成時に、それがご使用の codespace にクローンされます。

   また、 **[インスタンスの種類]** と **[Suspend after]\(中断までの時間\)** のタイムアウトは、それぞれドロップダウンを使用して変更できます。 codespace の詳細を設定したら、 **[作成と接続]** ボタンを選択します。

   ![Visual Studio codespace の詳細](media/visual-studio-codespace-details.png)

   codespace の準備が整ったら、GitHub Codespaces によって codespace の準備が開始され、Visual Studio が開かれます。

   codespace 名は、リモート インジケーターのメニュー バーに表示されます。

   ![eShopOnWeb レポジトリ codespace に接続されている Visual Studio](media/visual-studio-eshoponweb-codespace.png)

4. ローカルで作業する場合と同じように、Visual Studio の使用を開始します。 対処方法:

   * ソース コードを参照します。
   * ソリューション ファイルを選択し、ソリューションをビルドします (**Ctrl + Shift + B**)。
   * ソース ファイルにブレークポイントを設定し、**F5** キーを押してデバッガーでアプリケーションを起動します。
   * 変更を加え、それらをリポジトリにコミットします。   

> [!NOTE]
> 現時点では、GitHub [Codespaces ポータル](https://github.com/codespaces)を通じて Visual Studio 用 GitHub Codespaces を作成することはできません。 これらは、Visual Studio を使用してのみ作成できます。

## <a name="connect-to-a-codespace"></a>codespace に接続する

codespace を作成したら、Visual Studio から直接その codespace を開くことができます。

1. Visual Studio を起動すると、スタート ウィンドウの [作業の開始] の下に **[Connect to a codespace]\(codespace に接続\)** ボタンが表示されます。

   ![Visual Studio のスタート ウィンドウと [Connect to a codespace]\(codespace に接続\)](media/visual-studio-start-window.png)

   既に Visual Studio を起動している場合は、 **[ファイル]**  >  **[Connect to a codespace]\(codespace に接続\)** メニュー項目を使用できます。

   ![Visual Studio の [ファイル]、[Connect to a codespace]\(codespace に接続\) のメニュー項目](media/visual-studio-file-connect-to-codespace.png)

2. **[Connect to a codespace]\(codespace に接続\)** を選択します。 GitHub にまだサインインしていない場合は、サインインするよう求められます。

3. すべての GitHub Codespaces が、その詳細と共に右側のパネルに表示されます。

   ![使用可能な GitHub Codespaces と詳細が表示されている Visual Studio](media/visual-studio-connect-codespace.png)

   Azure DevOps リポジトリをクローンした codespace は、Visual Studio ではここにだけ表示され、GitHub の Codespaces ページには表示されません。

4. codespace を選択し、 **[接続]** ボタンを選択します。 codespace が中断されている場合は、再起動され、その codespace に接続されている Visual Studio が開きます。

   codespace 名は、リモート インジケーターのメニュー バーに表示されます。

   ![eShopOnWeb レポジトリ codespace に接続されている Visual Studio](media/visual-studio-eshoponweb-codespace.png)

5. ローカルで作業する場合と同じように、Visual Studio の使用を開始します。 対処方法:

   * ソース コードを参照します。
   * ソリューション ファイルを選択し、ソリューションをビルドします (**Ctrl + Shift + B**)。
   * ソース ファイルにブレークポイントを設定し、**F5** キーを押してデバッガーでアプリケーションを起動します。
   * 変更を加え、それらをリポジトリにコミットします。

<!-- TBD ## Suspend a codespace -->

<!-- TBD ## Disconnect from a codespace -->

## <a name="see-also"></a>関連項目

* [GitHub Codespaces とは](codespaces-overview.md)
* [codespace をカスタマイズする方法](customize-codespaces.md)
* [サポートされている Visual Studio の機能](supported-features-codespaces.md)
