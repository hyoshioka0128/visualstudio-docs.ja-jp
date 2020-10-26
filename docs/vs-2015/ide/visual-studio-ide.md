---
title: Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.topic: conceptual
ms.assetid: 772b6cf4-cee5-42d0-bc18-b4eb07e22ff0
caps.latest.revision: 36
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3bbeeb3d65e50e4cd3e33d4cab63dc619a1ad7a8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85534317"
---
# <a name="visual-studio-ide"></a>Visual Studio IDE
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Microsoft Visual Studio 2015 は、ソフトウェアを作成するための一連のツールです。このツールを使用して、計画の段階、UI 設計、コーディング、テスト、デバッグ、コードの品質やパフォーマンスの分析、カスタマーへの配置、使用率に関するテレメトリーの収集などを実行できます。 これらのツールは、できるだけシームレスに連携するよう設計されており、すべて Visual Studio 統合開発環境 (IDE) を通して公開されています。

Visual Studio を使用すると、さまざまなアプリケーションを作成できます。モバイル クライアント向けの単純なストア アプリやゲームから、企業やデータ センターに提供するような大規模で複雑なシステムなどです。 次の階層を作成できます。

- Windows だけでなく、Android と iOS でも動作するアプリおよびゲーム。

- ASP.NET、JQuery、AngularJS、その他の一般的なフレームワークをベースとした Web サイトおよび Web サービス。

- さまざまなプラットフォームやデバイス向けのアプリケーション。Azure、Office、Sharepoint、Hololens、Kinect、モノのインターネットなどはほんの一例です。

- DirectX を使用するさまざまな Windows デバイス (Xbox など) 向けのゲームおよびグラフィックを集中的に使用するアプリケーション。

既定では、Visual Studio は C#、C、C++、JavaScript、F#、Visual Basic のサポートを提供します。 Visual Studio は、Unity ( [Visual Studio Tools for Unity](../cross-platform/visual-studio-tools-for-unity.md) 拡張機能を介して) および Apache Cordova ( [Visual Studio Tools for Apache Cordova](https://msdn.microsoft.com/library/db446f2c-6ba4-4c76-aac5-4c66f43b8c42)を介して) などのサードパーティ製アプリケーションと密接に連携および統合しています。 特殊なタスクを実行するカスタム ツールを作成することで、Visual Studio を独自に拡張できます。

Visual Studio を初めて使用する場合は、「 [Get Started Developing with Visual Studio](../ide/get-started-developing-with-visual-studio.md) 」チュートリアルで基本を学んでください。

Visual Studio 2015 の新機能については、「[Visual Studio 2015 の新機能](../what-s-new-in-visual-studio-2015.md)」を参照してください。

## <a name="visual-studio-setup"></a>Visual Studio のセットアップ
 「 [Visual Studio のエディション](https://visualstudio.microsoft.com/vs/)」で、自分に適した Visual Studio のエディションを判別できます。

 Visual Studio 2015 は、「 [Visual Studio のダウンロード](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)」からダウンロードしてインストールできます。 インストール プロセスの詳細については、「[Visual Studio 2015 のインストール](../install/install-visual-studio-2015.md)」を参照してください。

## <a name="ide-basics"></a>IDE の基本
 次の図は、プロジェクトが開かれている Visual Studio IDE、プロジェクト ファイル内を移動するためのソリューション エクスプローラー ウィンドウ、ソース管理と作業項目トラッキングを移動するためのチーム エクスプローラー ウィンドウを示しています。 示されているタイトル バーの機能については、以下で詳しく説明します。

 ![Visual Studio IDE](../ide/media/visualstudioide.png "VisualStudioIDE")

### <a name="signing-in"></a>サインイン
 Visual Studio を初めて起動する際には、まず Microsoft アカウント、仕事用アカウント、または学校用アカウントを使ってサインインできます。 サインインすると、複数のデバイス間でウィンドウのレイアウトなどの設定を最新に保つことができ、必要なサービス (Azure サブスクリプションや Visual Studio Team Services など) に自動的に接続できます。 サブスクリプションに基づくライセンスがある場合は、ライセンスのトークンを最新の状態に保つために、定期的に Visual Studio にサインインする必要があります。 プロダクト キーのライセンスがある場合、サインインする必要はありませんが、サインインすると、Visual Studio Team Services や Azure、Office 365、Salesforce.com のアカウントに接続しやすくなります。 詳しくは、「[Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)」をご覧ください。

 Visual Studio Team Services アカウント、Azure アカウント、または MSDN サブスクリプションが複数ある場合、それらをリンクして、単一のサインインですべてのアカウント内のリソースとサービスにアクセスできます。 詳細については、「 [Work with multiple user accounts](../ide/work-with-multiple-user-accounts.md)」を参照してください。

### <a name="staying-up-to-date"></a>最新の状態に保つ
 タイトル バーの右上の通知アイコンは、Visual Studio の更新プログラムまたはインストールされている関連コンポーネントが入手可能になると、通知します。 この通知を解除するか有効にするかを選択できます。 詳しくは、「[Visual Studio の通知](../ide/visual-studio-notifications.md)」をご覧ください。

### <a name="finding-things-and-getting-help"></a>検索とヘルプの取得
 キーボード ショートカットやメニューの場所が分からない場合、下の [ [クイック起動](../ide/reference/quick-launch-environment-options-dialog-box.md) ] ウィンドウを使用すると、Visual Studio コマンド、ツール、機能などをすぐに見つけることができます。 探しているものを入力すれば、クイック起動がそのリンクを教えてくれます。

 !['新しいプロジェクト' のクイック起動結果](../ide/media/productivity-quicklaunch.png "Productivity_QuickLaunch")

 MSDN は、技術情報に関する Microsoft Web サイトです。今まさに、MSDN でこのページをお読みになっています。 Visual Studio で **F1** キーを押すと、アクティブ ウィンドウに関する MSDN のヘルプ ページに移動できます。 また、コード エディターで **F1** キーを押すと、現行のカーソル位置の API またはキーワードについての MSDN ヘルプ ページに移動できます。 たとえば、C# ファイルで、`System.String` 宣言の途中か末尾にカーソルを置いて **F1** キーを押すと、<xref:System.String> の MSDN ヘルプ ページに移動します。

### <a name="giving-feedback"></a>フィードバックの提供
 Visual Studio では、いつでもフィードバックを簡単に提供できます。 **[クイック起動]** の横にあるタイトル バーのフィードバック アイコンをクリックして、 **[問題の報告]** または **[提案事項の送信]** をクリックします。 Visual Studio のプレリリース版にも、 **[この製品を評価する]** オプションが用意されています。 これらのすべてのコメントを拝見し、製品向上のための参考にさせていただきます。 詳細については、「 [Talk to Us](../ide/talk-to-us.md)」を参照してください。

### <a name="personalizing-the-ide"></a>IDE のカスタマイズ
 開発スタイルに合わせてウィンドウのレイアウトをカスタマイズできます。 どのウィンドウも、任意の時にドッキング、フローティング、または非表示にすることができます。また、エディターを全画面表示モードで実行することもできます。 特定のコンテキストで必要なウィンドウのみを表示する複数のカスタム ウィンドウ レイアウトを作成して保存できます。 たとえば、表示されるものすべてがコード エディターとなるよう、全画面レイアウトを作成できます。 デバッグ用およびチームでの操作用にさまざまなレイアウトを作成できます。 詳しくは、「[ウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」をご覧ください。

 その他にも、Visual Studio をさまざまな方法でカスタマイズできます。複数のコンピューターで作業している場合は、設定をローミングできます。 詳細については、「 [IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

 ほとんどすべてにキーボード ショートカットがあります。また、キーボード ショートカットをカスタマイズすることもできます。 新しいショートカットを作成するには、クイック起動に「キーボード」と入力して、[キーボード] ダイアログ ボックスを開きます。 オプションに関する詳細が必要な場合、そのダイアログ ボックスで F1 を押して、MSDN ヘルプ ページに移動できます。 詳しくは、「[Visual Studio の既定のキーボード ショートカット](../ide/default-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

## <a name="connecting-to-visual-studio-team-services-and-team-foundation-server"></a>Visual Studio Team Services と Team Foundation Server への接続
 Visual Studio Team Services (VSTS) は、ソフトウェア プロジェクトをホストし、チームでのコラボレーションを有効にするためのクラウド ベースのサービスです。 VSTS は、Git ソース管理システムと Team Foundation ソース管理システムの両方をサポートしています。また、Scrum、CMMI、アジャイル開発方法もサポートしています。 Team Foundation バージョン管理 (TFVC) は、単一の集中サーバー リポジトリを使用して、ファイルを追跡してバージョン管理します。 ローカルの変更は常に集中サーバーにチェックインされます。他の開発者はそこで、最新の変更を取得できます。 Team Foundation Server (TFS) 2015 は、Visual Studio のアプリケーション ライフサイクル管理のハブです。 これにより、開発プロセスに関わるすべてのユーザーが 1 つのソリューションを使用して参加できるようになります。 TFS は、異種混合のチームやプロジェクトを管理するのにも役立ちます。

 Visual Studio Team Services のアカウントまたは Team Foundation Server がネットワーク上にある場合、[チーム エクスプローラー] ウィンドウから接続することができます。 このウィンドウからソース管理にコードをチェックインしたりソース管理からコードをチェックアウトできます。また、作業項目を管理したり、ビルドを開始したり、チームのルームやワークスペースにアクセスできます。 チーム エクスプローラーは、**[クイック起動]**、**[ビュー] > [チーム エクスプローラー]** のメイン メニュー、または **[チーム] > [接続の管理]** から開くことができます。  Visual Studio Team Services について詳しくは、「 [www.visualstudio.com](https://www.visualstudio.com/)」をご覧ください。 Team Foundation Server について詳しくは、「 [Team Foundation Server](https://www.visualstudio.com/products/tfs-overview-vs)」をご覧ください。

 次の図は、VSTS でホストされているソリューションの [チーム エクスプローラー] ウィンドウを示しています。

 ![Visual Studio Team Explorer](../ide/media/vs2015-teamexplorer.png "VS2015_TeamExplorer")

## <a name="creating-solutions-and-projects"></a>ソリューションとプロジェクトの作成
 Visual Studio を使用して個々のコード ファイルを使用できますが、より一般的なのは、 *プロジェクト*で処理する方法です。 Visual Studio プロジェクトは、ファイルとリソースのを集めたものです。アプリケーションにするために単一のバイナリ実行可能ファイル (.exe、DLL、appx など) にコンパイルされます。 ASP.NET Web サイト以外では、実行可能ファイルは生成されません。プロジェクトには、HTML、JavaScript ファイル、および画像のみが含まれます。 密接に関連した複数のバイナリまたは Web サイトを作成することが必要になる時があります。そのため、Visual Studio にはソリューションという概念があります。ソリューションには、複数のプロジェクトまたは Web サイトを含めることができます。 プロジェクトを作成する際、実際にはソリューションのプロジェクトを作成していることになります。必要に応じて、後からそのソリューションにプロジェクトを追加することができます。 たとえば、DLL プロジェクトがある場合、DLL を読み込んで使用するソリューションに.exe プロジェクトを追加できます。

 *プロジェクト テンプレート* は、事前設定済みコード ファイルと構成設定のコレクションです。これにより、特定の種類のアプリケーションの作成作業をすばやくセットアップすることができます。 Visual Studio には多くの選択元となるプロジェクト テンプレートが用意されています。既定のテンプレートの中に適切なものがなければ、独自のテンプレートを作成することができます。 テンプレートを使ってプロジェクトを作成した後、そのプロジェクトでの独自のコードの作成を開始できます。提供されているファイルか、追加する新しいファイルに作成できます。 詳しくは、「[ソリューションおよびプロジェクト](../ide/solutions-and-projects-in-visual-studio.md)」をご覧ください。 次の図は、ASP.NET アプリケーション用に使用できるプロジェクト テンプレートが入った [新しいプロジェクト] ダイアログを示しています。

 ![Visual Studio の [新しいプロジェクト] ダイアログ](../ide/media/vs2015-newprojectdialog.png "VS2015_NewProjectDialog")

## <a name="designing-the-user-interface"></a>ユーザー インターフェイスの定義
 デザイナーは、コードを記述することなくユーザー インターフェイスを作成できる直感的なツールのことです。 リスト ボックス、カレンダー、ボタンなどの UI コントロールを [ [Toolbox](../ide/reference/toolbox.md) ] ウィンドウから、ウィンドウまたはダイアログ ボックスを表すデザイン サーフェイスにドラッグできます。 コードを記述することなく、要素のサイズを変更し、再配置できます。 ユーザー インターフェイスを伴うものであれば、どんな種類のプロジェクトについても、デザイナーが含まれています。

 プロジェクトに XAML ベースのユーザー インターフェイスがある場合、既定のデザイナーは、Blend for Visual Studio です。Blend for Visual Studio は、Visual Studio とシームレスに連携する高度なグラフィック ツールです。

 ![アートボード](../ide/media/b5-artboard.png "b5_artboard")

|Image|説明|
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**デザイン ビュー** ドキュメントのビジュアル デザインを表示します。 このビューでは、デザイン サーフェイス上のオブジェクトを描画または変更できます。|
|![](../designers/media/b1-2.png "B1_2")|**階層リンク** 選択したオブジェクトのテンプレート編集モード、スタイル編集モード、およびオブジェクト編集スコープを簡単に切り替えることができます。|
|![](../designers/media/b1-3.png "B1_3")|**ズーム** デザイン サーフェイスをズームするとき、またはデザイン サーフェイス上のオブジェクトをズームするときに使用します。|
|![](../designers/media/b1-4.png "B1_4")|**デザイン サーフェイス コントロール** これらのコントロール (**[スナップ グリッドの表示]**、 **[グリッド線にスナップ]** 、 **[スナップ ガイドラインへのスナップをオン/オフにする]**) は、スナップ オプションを設定するときに使用します。 スナップ機能は、オブジェクトを並べて配置するときや、デザイン サーフェイスに行を等間隔で配置するときに便利です。|
|![](../designers/media/b1-5.png "B1_5")|**コード エディター** コード エディターで XAML、C#、C++ または Visual Basic のコードを手動で編集します。|

 詳細については、[Visual Studio および Blend for Visual Studio での XAML デザインに関する記事](../designers/designing-xaml-in-visual-studio.md)を参照してください。

## <a name="writing-navigating-and-understanding-code"></a>コードの記述、移動、理解
 おそらく、開発者はほとんどの時間をエディター ウィンドウで費やします。 Visual Studio には、C#、C++、Visual Basic、JavaScript、XML、HTML、CSS、F# のエディター、およびサード パーティによって提供されるプラグイン エディター (およびコンパイラ) がその他の多数の言語で用意されています。

 テキスト エディターで **[ファイル] > [開く] > [ファイル]** とクリックすると、個別のファイルを編集できます。 とクリックすると、個別のファイルを編集できます。開いているプロジェクト内のファイルを編集するには、ソリューション エクスプ ローラーで対象ファイル名をクリックします。 コードは色分け表示されます。クイック起動で「色」と入力すると、配色をカスタマイズできます。 テキスト エディターのタブ付きウィンドウを、一度に多数開くことができます。 各ウィンドウ個別に分割できます。 テキスト エディターを全画面表示モードで実行することもできます。

 ![コード エディターの GreetingsConsoleApp.cpp](../ide/media/c-ide-editorlinenumberswordwrapon.png "C++ IDE_EditorLineNumbersWordWrapOn")

 テキスト エディターには、生産性の向上に役立つ多くの機能との高度な対話性があります (望む場合)。これによって、より質の高いコードをより早く作成できます。 機能は言語によって異なり、機能をオンまたはオフにするためにそれらを使用する必要はありません (クイック起動で「エディター」を入力)。一般的な生産性向上機能として、次のものがあります。

1. [Refactoring](../ide/refactoring-in-visual-studio.md) 。これには、変数の名前をインテリジェントに変更する、選んだコード行を別個の関数に移動する、コードを他の場所に移動する、関数パラメーターを並べ替える、などの操作が含まれます。

2. *IntelliSense*。コードに関する型情報をエディターに直接表示したり、場合によっては、ちょっとしたコードを自動的に作成したりする、よく使われる機能セットの包括的な用語です。 エディター内のインラインに基本ドキュメントがあるようなもので、これによって、別個のヘルプ ウィンドウで型情報を検索する手間が省けます。 IntelliSense 機能は言語によって異なります。 詳しくは、「 [Visual C# IntelliSense](../ide/visual-csharp-intellisense.md), [Visual C++ Intellisense](../ide/visual-cpp-intellisense.md), [JavaScript IntelliSense](../ide/javascript-intellisense.md), [Visual Basic-Specific IntelliSense](../ide/visual-basic-specific-intellisense.md)」をご覧ください。 次の図は、職場でのいくつかの IntelliSense 機能を示しています。

    ![Visual Studio のメンバーの一覧](../ide/media/vs2015-intellisense.png "vs2015_Intellisense")

3. **波線** 。入力と同時にコードのエラーまたは潜在的な問題をアラートします。これにより、コンパイルまたは実行時にエラーが発見されるのを待たずに即時に修正することができます。 破線の上に移動すると、エラーに関する追加情報が表示されます。 電球がエラーの修正方法に関する提案とともに左余白に表示される場合もあります。 詳しくは、「[電球を使ってクイック操作をする](../ide/perform-quick-actions-with-light-bulbs.md)」をご覧ください。

    ![電球でのマウス ホバー](../ide/media/vs2015-lightbulb-hover.png "VS2015_LightBulb_Hover")

4. [ブックマーク](../ide/setting-bookmarks-in-code.md) 。アクティブに作業しているファイルの特定の行にすばやく移動することができます。

5. [Call Hierarchy](../ide/reference/call-hierarchy.md) ウィンドウはテキスト エディターのコンテキスト メニューで呼び出して、キャレットの下のメソッドを呼び出す、またはそのメソッドによって呼び出されるメソッドを表示することができます。

6. **コード レンズ** 。コードへの参照および変更、リンクされたバグ、作業項目、コード レビュー、単体テストをすべて、エディターを離れずに検索できます。 詳しくは、「[コード変更およびその他の履歴の検索](../ide/find-code-changes-and-other-history-with-codelens.md)」をご覧ください。

7. [ **ピークの定義** ] ウィンドウ。現在のコンテキストから移動せずに、メソッドまたは型の定義インラインが表示されます。 このウィンドウは、XAML でも有効です。

8. [ **定義に移動** ] コンテキスト メニュー オプション。関数またはオブジェクトが定義されている場所に直接移動します。 エディターを右クリックすることで、その他のナビゲーション コマンドも使用できます。

9. [オブジェクト ブラウザー](https://msdn.microsoft.com/f89acfc5-1152-413d-9f56-3dc16e3f0470)(関連ツール)。システム上の .NET アセンブリまたは Windows ランタイム アセンブリを調べ、アセンブリにどの型が含まれているか、またそれらの型にどのメソッドとプロパティが含まれているかを確認できます。

     ![System.Timer を示すオブジェクト ブラウザー](../ide/media/objectbrowser.png "ObjectBrowser")

   [編集] メニューと [表示] メニュー上の項目のほとんどは、何らかの方法でコード エディターに関連しています。 エディターについて詳しくは、「[コードの作成](../ide/writing-code-in-the-code-and-text-editor.md)」および「[コードの編集](https://www.visualstudio.com/features/ide-vs)」をご覧ください。

## <a name="compiling-and-building-your-code"></a>コードのコンパイルとビルド

プロジェクトをビルドするということは、ソース コードをコンパイルし、実行可能ファイルの生成に必要な手順すべてを実行することを意味します。 ビルド操作は言語によって異なっており、通常の Web サイトはまったくビルドは行っていません。 プロジェクトの種類に関係なく、[ビルド] メニューはこれらのコマンドの標準の場所です。 一度のキー入力でコードをコンパイルして実行するには、F5 キーを押します。 どのコンパイラも、IDE によって完全に構成可能です。 [ビルド] ツールバーでは、プログラムのデバッグ バージョンをビルドするかどうかを指定できます。デバッグ バージョンでは、記号と追加エラー チェックが有効になり、デバッガーでのブレークポイントとシングル ステップ、リリース ビルド (最終的にお客様に渡すもの) がサポートされます。 他のビルド設定や、他の多くの設定をプロジェクトのプロパティ ページで構成できます。 ソリューション エクスプローラーでプロジェクト ノードを右クリックし、[プロパティ] を選択します。 コマンド ラインからビルドを実行することもできます。

ビルドからの出力 (エラー メッセージや成功メッセージを含む) が **[出力]** ウィンドウに表示されます。 以下に示す **[エラー一覧]** には、ビルド エラーに関する詳細情報が表示されます。

## <a name="debugging-your-code"></a>コードのデバッグ
 Visual Studio の最新のデバッガーを使用すると、ローカル プロジェクトで実行されるコード、リモート デバイスで実行されるコード、エミュレーターで実行されるコード (Android や Windows Phone のコードなど) をデバッグできます。 一度に 1 つのステートメントのコードをステップスルーでき、変数を調べることができます。マルチスレッド アプリケーションをステップスルーでき、指定された条件が true の場合のみヒットするブレークポイントを設定できます。 このすべては、コード エディター自体で構成できます。したがって、コードのコンテキストを離れる必要はありません。

 ![ブレークポイントの設定の [表示のみ] ウィンドウ](../ide/media/dbg-breakpoints-peekwindow.png "DBG_Breakpoints_PeekWindow")

 デバッガー自体に複数のウィンドウがあり、それらのウィンドウから、ローカル変数、呼び出し履歴、ランタイム環境のその他の側面を表示および操作できます。 これらのウィンドウは [ **デバッグ** ] メニューにあります。

 [Immediate Window](../ide/reference/immediate-window.md) では、式に入力し、その結果を即時に表示できます。

 [ [IntelliTrace](https://msdn.microsoft.com/629e9660-c59a-446b-8c30-290059158f61) ] ウィンドウでは、実行中の .NET プログラムの各メソッド呼び出しとその他のイベントを記録します。問題の発生源をすぐに見つけることができます。

 詳細については、「 [Debugging in Visual Studio](../debugger/debugging-in-visual-studio.md)」を参照してください。

## <a name="testing-your-code"></a>コードのテスト
 Visual Studio には、マネージド コード (.NET) の単体テスト フレームワークとネイティブ C++ の単体テスト フレームワークが含まれています。 単体テストを作成するには、単にテスト プロジェクトをソリューションに追加し、テストを作成し、そのテストを [テスト エクスプローラー] ウィンドウから実行します。 詳しくは、「[コードの単体テストUnit Test Your Code](../test/unit-test-your-code.md)」をご覧ください。

 ![単体テスト エクスプローラー](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

## <a name="analyzing-code-quality-and-performance"></a>コード品質とパフォーマンスの分析
 Visual Studio には、静的分析とランタイム分析のための強力なツールが含まれています。 静的分析ツールでは、デザイン、グローバリゼーション、相互運用性、パフォーマンス、セキュリティ、その他のカテゴリでの潜在的なエラーを特定することができます。 パフォーマンス テスト (プロファイリング) では、プログラムの実行方法を測定する必要があります。 これらのツールには、[ **分析** ] メニューからアクセスできます。 詳細については、「 [Visual Studio 診断ツールによる品質の向上](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)」を参照してください。

## <a name="connecting-to-cloud-services-and-databases"></a>クラウド サービスとデータベースへの接続
 Visual Studio の [ [サーバー エクスプローラー](https://msdn.microsoft.com/library/4ea29b3b-bbb2-45e4-9082-eaf635c41c4d) ] ウィンドウには、個人アカウント (ログインで使用するアカウント) の下で管理されているすべてのアカウントのリソースが表示されます。これには、SQL Server インスタンス、Azure、salesforce.com、Office 365、Websites が含まれます。

 ![サーバー エクスプローラー](../ide/media/vs2015-serverexplorer3.png "vs2015_ServerExplorer3")

 Visual Studio には、 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx) (SSDT) が含まれています。これを使用して、データベースをビルド、デバッグ、保守、リファクタリングできます。 データベース プロジェクトを操作したり、オンプレミスまたはオフプレミスで接続されたデータベース インスタンスを直接操作したりすることができます。

 Visual Studio の SQL Server オブジェクト エクスプローラーには、SQL Server Management Studio と同様のデータベース オブジェクトを表示する機能があります。 SQL Server オブジェクト エクスプローラーを使用すると、軽いデータベース管理と設計作業を実行できます。これには、SQL Server オブジェクト エクスプローラーのコンテキスト メニューの使用によるテーブル データの編集、スキーマの比較、クエリの実行が含まれます。 また、SSDT には、SQL Server 2012 Analysis Services、Reporting Services、Integration Services Business Intelligence (BI) の各ソリューション (以前の Business Intelligence Development Studio) を開発するための特別なプロジェクトの種類とツールも含まれます。

 ![[SQL Server オブジェクト エクスプローラー]](../ide/media/vs2015-sqlobjectexplorer.png "vs2015_SQLObjectExplorer")

## <a name="deploying-your-finished-application"></a>完成したアプリケーションの配置
 アプリケーションをお客様に配置する用意ができたら、Visual Studio の配置するためのツールを使用できます。Windows ストア や Sharepoint サイトへの配置、Installshield または Windows インストーラー テクノロジによる配置、いずれにも対応しています。 これはすべて、IDE を使用してアクセスできます。 詳細については、「 [アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)」を参照してください。

## <a name="architecture-and-modeling-tools-enterprise-only"></a>アーキテクチャおよびモデリング ツール (Enterprise のみ)
 Visual Studio アーキテクチャおよびモデリング ツールを使用して、アプリを設計してモデル化することができます。 これらのツールを使用して、コードの構造、動作、関係を視覚化できます。 モデルは、開発プロセスの一部として、アプリケーション ライフサイクル全体で詳細のさまざまなレベルで作成できます。 Team Foundation Server の作業項目と開発計画にモデル要素をリンクすることで、要件、タスク、テスト ケース、バグ、またはモデルに関連するその他の作業を追跡できます。 詳細については、「 [アプリの設計とモデル化](../modeling/analyze-and-model-your-architecture.md)」を参照してください。

## <a name="extending-visual-studio-through-the-visual-studio-sdk"></a>Visual Studio SDK による Visual Studio の拡張
 Visual Studio は、拡張可能なプラットフォームです。 Visual Studio の拡張は、IDE と統合するカスタム ツールです。 サード パーティ製の拡張機能を追加したり、独自の拡張機能を作成したりできます。 詳細については、「 [Visual Studio 拡張機能の開発](https://msdn.microsoft.com/library/5b1b5db3-6005-44cf-83b0-e608d7764d14)」を参照してください。

 [Visual Studio User Experience Guidelines](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md) は、Visual Studio の拡張機能を記述するすべてのユーザーにとって重要な参照です。 これらのプラットフォーム固有のガイドラインには、ダイアログのデザイン、フォント、色、アイコン、コモン コントロール、および新機能が Visual Studio とシームレスに統合できるようにするその他の相互作用のパターンについての情報が含まれています。

## <a name="in-this-guide"></a>このガイドの内容

- [ユーザーアカウントと更新プログラム](../ide/user-accounts-and-updates.md)
- [IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)
- [方法: IDE 内で移動する](../ide/how-to-move-around-in-the-visual-studio-ide.md)
- [Visual Studio を使用した開発の開始](../ide/get-started-developing-with-visual-studio.md)
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
- [ソリューションとプロジェクト](../ide/solutions-and-projects-in-visual-studio.md)
- [コードの作成](../ide/writing-code-in-the-code-and-text-editor.md)
- [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)
- [プロファイル ツール](../profiling/profiling-tools.md)
- [コード品質の向上](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)
- [ユーザー インターフェイスの設計](../designers/designing-user-interfaces.md)
- [アーキテクチャの分析およびモデリング](../modeling/analyze-and-model-your-architecture.md)
- [コードのコンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
- [アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)
- [Visual Studio IDE の 64 ビット サポート](../ide/visual-studio-ide-64-bit-support.md)
- [Security](../ide/security-in-visual-studio.md)
- [Visual Studio のサンプル](../ide/visual-studio-samples.md)
- [Microsoft ヘルプ ビューアー](../ide/microsoft-help-viewer.md)
- [アプリケーションのグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
- [UI リファレンス](../ide/reference/general-user-interface-elements-visual-studio.md)

## <a name="see-also"></a>参照

- [Visual Studio 2015 のインストール](../install/install-visual-studio-2015.md)
- [コードの編集](https://www.visualstudio.com/features/ide-vs)
- [Visual Studio 2015 の新機能](../what-s-new-in-visual-studio-2015.md)
- [Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)
- [ご意見](../ide/talk-to-us.md)