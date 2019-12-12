---
title: Visual Studio 2017 の新機能
titleSuffix: ''
description: Visual Studio 2017 の新機能について説明します。
ms.date: 12/18/2018
f1_keywords:
- VS.StartPage.WhatsNew
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 7307e180-ba28-4774-8a43-cbb980085a71
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: de26054894783df283d38223a59741c0500d0bc5
ms.sourcegitcommit: 0a8855572c6c88f4b2ece232c04aa124fbd9cec3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74955037"
---
# <a name="whats-new-in-visual-studio-2017"></a>Visual Studio 2017 の新機能

**[15.9 リリース](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017)の更新**

以前のバージョンの Visual Studio からのアップグレードを検討していますか。 Visual Studio 2017 でできること:すべての開発、すべてのアプリ、すべてのプラットフォームにおいて、他に類を見ない生産性を実現します。 Visual Studio 2017 を利用し、Android、iOS、Windows、Linux、Web、クラウド向けのアプリを開発します。 短期間でプログラミングできて、デバッグや診断も簡単に行えます。テストを頻繁に行うことで、自信をもってリリースできます。 独自の拡張機能を開発することで Visual Studio を拡張し、カスタマイズすることもできます。 今回のリリースでは、バージョン管理を使用した、迅速で、効率的な共同作業が可能になりました。

>[!div class="button"]
>[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

以前のバージョンである Visual Studio 2015 以降に行われた主な変更点の要約を示します。

* **[基本の再定義](#redefined-fundamentals)** 。 新しいセットアップ エクスペリエンスにより、必要なものを必要なタイミングでより短い時間でインストールできるようになりました。
* **[パフォーマンスと生産性](#performance-and-productivity)** 。 Microsoft は、新しく、現代的なモバイル、クラウド、デスクトップの開発機能を導入することを中心に取り組んできました。 また、Visual Studio の起動が以前と比較してより高速になり、より応答性が向上し、メモリの消費量が少なくなりました。
* **[Azure によるクラウド アプリの開発](#cloud-app-development-with-azure)** 。 Microsoft Azure を使用するクラウド ファーストのアプリを簡単に作成できる Azure ツールのビルトイン スイート。 Visual Studio を使用すれば、Azure でアプリとサービスを構成、ビルド、デバッグ、パッケージ化、デプロイするのが容易になります。
* **[Windows アプリ開発](#windows-app-development)** 。 Visual Studio 2017 で UWP テンプレートを使用して、すべての Windows 10 デバイス (PC、タブレット、電話、Xbox、HoloLens、Surface Hub など) を対象とした単一のプロジェクトを作成します。
* **[モバイル アプリの開発](#mobile-app-development)** 。 マルチプラットフォームのモバイル要件を 1 つのコア コードベースとスキル セットに統合する Xamarin により、短期間で革新的な成果を出すことができます。
* **[クロスプラットフォーム開発](#cross-platform-development)** 。 対象となるプラットフォームにソフトウェアをシームレスに届けます。 Redgate Data Tools により DevOps プロセスを SQL Server に拡張し、Visual Studio からのデータベース配置を安全に自動化します。 あるいは、.NET Core を利用し、変更しなくても Windows、Linux、macOS オペレーティング システムをまたいで実行できるアプリやライブラリを作成します。
* **[ゲーム開発](#games-development)** 。 Visual Studio tools Unity (VSTU) を利用すると、Visual Studio を使用して C# でゲームとエディター スクリプトを記述した後、強力なデバッガーを使用してエラーを検出して修正できます。
* **[AI の開発](#ai-development)** 。 Visual Studio Tools for AI では、Visual Studio の生産性機能を使用して、AI 革新を高速化することができます。 堅牢な実験機能のために、Azure Machine Learning とシームレスに統合するディープ ラーニング / AI ソリューションをビルド、テスト、展開します。

> [!NOTE]
> Visual Studio 2017 の新機能の一覧については、「[最新のリリース ノート](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017)」を参照してください。 また、将来的な機能の内容については、「[リリース ノートのプレビュー](/visualstudio/releasenotes/vs2017-preview-relnotes?context=visualstudio/default&contextView=vs-2017)」を参照してください。

Visual Studio 2017 の最も重要な改善点と新機能について、そのいくつかの詳細を確認できます。

## <a name="redefined-fundamentals"></a>基本の再定義

### <a name="a-new-setup-experience"></a>新しいセットアップ エクスペリエンス

Visual Studio により、必要な機能だけを必要なタイミングでより簡単により短い時間でインストールできます。 また、アンインストールも正常に行われます。

Visual Studio をインストールするときに確認できる最も重要な変更は、新しいセットアップ エクスペリエンスです。 **[ワークロード]** タブには、共通のフレームワーク、言語、プラットフォーム別にグループ化されたインストール オプションが表示されます。 .NET デスクトップ開発から Windows、Linux、iOS での C++ アプリケーション開発まで、すべてを網羅します。

必要なワークロードを選択し、必要に応じてそれらを変更します。

![Visual Studio 2017 のセットアップ ダイアログ](../install/media/install-visual-studio-enterprise.png)

また、インストールを調整するオプションもあります。

* ワークロードを使用する代わりに、独自のコンポーネントを選択するには、 インストーラーから **[個別のコンポーネント]** タブを選択します。
* また、Windows の言語オプションを変更することなく、言語パックをインストールする場合は、 インストーラーの **[言語パック]** タブを選択します。
* **15.7 の新機能**:Visual Studio のインストール場所を変更したいですか? インストーラーの **[インストール オプション]** タブを選択します。

ステップ バイ ステップの手順を含む、新しいインストール エクスペリエンスの詳細については、[Visual Studio のインストール](../install/install-visual-studio.md)に関するページを参照してください。

### <a name="a-focus-on-accessibility"></a>アクセシビリティに重点を置く

**15.3 の新機能**として、Visual Studio と多くのユーザーが使用している支援技術との互換性を改善する、1,700 を超える変更を行いました。 スクリーン リーダーやハイ コントラスト テーマなどの支援技術との互換性を従来よりも改善するシナリオが、数多くあります。 デバッガー、エディター、シェルのすべてに重要な変更点があります。

詳細については、ブログ投稿の「[Accessibility improvements in Visual Studio 2017 version 15.3 (Visual Studio 2017 バージョン 15.3 でのアクセシビリティの機能強化)](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)」をご覧ください。

## <a name="performance-and-productivity"></a>パフォーマンスと生産性

### <a name="sign-in-across-multiple-accounts"></a>複数のアカウント間のサインイン

チーム エクスプローラー、Azure Tools、Microsoft ストアでの発行で使用するユーザー アカウントを共有できるように、Visual Studio で新しい ID サービスを導入しました。

また、より長い時間サインインしたままにできます。 Visual Studio に 12 時間ごとにサインインを求められることはなくなりました。 詳細については、「[Fewer Visual Studio Sign-in Prompts](https://devblogs.microsoft.com/visualstudio/fewer-visual-studio-sign-in-prompts/)」 (Visual Studio のサインインの確認メッセージを減らす) のブログの投稿を参照してください。

### <a name="start-visual-studio-faster"></a>Visual Studio の起動の高速化

Visual Studio の新しいパフォーマンス センターは、IDE の起動時間を最適化するのに役立ちます。 パフォーマンス センターでは、IDE の起動を遅くしている可能性のある拡張機能やツール ウィンドウをすべて一覧表示します。 拡張機能を起動するタイミングや、ツール ウィンドウを起動時に開くかどうかを指定して、起動時のパフォーマンスを向上させるために使用することができます。

### <a name="faster-on-demand-loading-of-extensions"></a>拡張機能のオンデマンド読み込みの高速化

Visual Studio では、独自およびサードパーティの拡張機能が IDE の起動時ではなく必要に応じて読み込まれるように取り組みを進めています。 どの拡張機能が起動、ソリューションの読み込み、および入力パフォーマンスに影響があるかについて関心をお持ちですか? この情報については、 **[ヘルプ]** 、 **[Visual Studio のパフォーマンスの管理]** の順に選択して確認することができます。

  ![Visual Studio 2017 の [オプション] ダイアログ ボックス](media/vs2017ide-manage-vs-perf.png)

#### <a name="manage-your-extensions-with-roaming-extensions-manager"></a>[拡張機能マネージャーのローミング] で拡張機能を管理する

Visual Studio にサインインすると、お気に入りの拡張機能を使用して、各開発環境を容易に設定できるようになりました。 新しい [拡張機能マネージャーのローミング] は、クラウドに同期されたリストを作成することで、お気に入りの拡張機能をすべて追跡します。

Visual Studio の拡張機能の一覧を表示するには、 **[ツール]** 、 **[拡張機能と更新プログラム]** の順にクリックし、 **[拡張機能マネージャーのローミング]** をクリックします。

![Visual Studio 2017 - [拡張機能と更新プログラム] ダイアログ ボックス](media/vs2017ide-extensions-and-updates.png)

[拡張機能マネージャーのローミング] では、インストールするすべての拡張機能を追跡しますが、どの拡張機能をローミング リストに追加するかを選択することができます。

![Visual Studio 2017 - [拡張機能と更新プログラム] ダイアログ ボックス](media/vs2017ide-RoamingExtensionManager.png)

[拡張機能マネージャーのローミング] を使用する場合、リストに次の 3 つの種類のアイコンが表示されます。

* ![ローミング済みアイコン](media/vs2017ide-roamedicon.png) **_ローミング済み_** :ローミング リストにあり、このコンピューターにはインストールされていない拡張機能を示します。
  (これらの拡張機能は、 **[ダウンロード]** ボタンでインストールできます。)
* ![ローミングおよびインストール済みアイコン](media/vs2017ide-roamedinstalledicon.png) **_ローミングおよびインストール済み_** :ローミング リストにあり、お使いの開発環境にインストールされているすべての拡張機能を示します。
  (ローミングしない場合は、 **[ローミングの停止]** ボタンで削除することができます。)
* ![インストール済みアイコン](media/vs2017ide-installedicon.png) **_インストール済み_** :この環境にインストールされ、ローミング リストにはないすべての拡張機能を示します。
  ( **[ローミングの開始]** ボタンを使用して、拡張機能をローミング リストに追加できます。)

サインイン中にダウンロードするすべての拡張機能が **[ローミングおよびインストール済み]** としてリストに追加されます。 拡張機能はローミング リストの一部となり、任意のコンピューターからアクセスできるようになります。

### <a name="experience-live-unit-testing"></a>Enterprise のライブ単体テスト

Visual Studio Enterprise 2017 では、ライブ単体テストを実行することで、コーディング中にエディターで単体テストの結果とコード カバレッジをライブで確認できます。 .NET Framework と .NET Core の両方で C# プロジェクトと Visual Basic プロジェクトと連動し、MSTest、xUnit、NUnit の 3 つのテスト フレームワークをサポートします。

![Live Unit Testing](media/lut-codewindow.png)

詳細については、「[Introducing Live Unit Testing](../test/live-unit-testing-intro.md)」(Live Unit Testing の概要) を参照してください。 Visual Studio Enterprise 2017 の各リリースで追加された新機能の一覧は、「[What's new in Live Unit Testing](../test/live-unit-testing-whats-new.md)」(Live Unit Testing の新機能) を参照してください。

### <a name="set-up-a-cicd-pipeline"></a>CI/CD パイプラインの設定

#### <a name="automated-testing"></a>自動テスト

自動化されたテストは、DevOps パイプラインの重要な部分です。 短い周期で、一貫性と信頼性のある方法でソリューションをテストし、公開できます。 CI/CD (Continuous Integration and Continuous Delivery/継続的インテグレーションと継続的デリバリー) フローにより、このプロセスがさらに効率的になります。

自動化されたテストの詳細については、[DevOps の 自動化テストの CI/CD パイプライン](https://blogs.msdn.microsoft.com/visualstudioalmrangers/2017/04/20/set-up-a-cicd-pipeline-to-run-automated-tests-efficiently/)に関するブログ投稿をご覧ください。

[Continuous Delivery Tools for Visual Studio (Visual Studio 用の継続的デリバリー ツール)](https://marketplace.visualstudio.com/items?itemName=VSIDEDevOpsMSFT.ContinuousDeliveryToolsforVisualStudio) DevLabs 拡張の新機能の詳細については、ブログ投稿「[Commit with confidence: Commit time code quality](https://devblogs.microsoft.com/visualstudio/committing-with-confidence-getting-code-quality-information-at-commit-time/)」 (自信を持ってコミットする: タイム コードの品質をコミットする) をご覧ください。

### <a name="visual-studio-ide-enhancements"></a>Visual Studio IDE の拡張機能

#### <a name="multi-caret-editing"></a>マルチキャレットの編集

**15.8 の新機能**:ファイル内の複数の場所の同時編集が簡単になりました。 まず、ファイル内の複数の場所で挿入ポイントと選択範囲を作成します。 次に、マルチ キャレット編集機能を使用し、複数の場所で同時に同じ編集を行うことができます。

詳細については、[[テキストの検索と置換]](finding-and-replacing-text.md) ページの [[マルチキャレット選択]](finding-and-replacing-text.md#multi-caret-selection) セクションをご覧ください。

#### <a name="keep-keybinding-profiles-consistent"></a>キー バインド プロファイルの一貫性を維持する

**15.8 の新機能**:2 つの新しいキーボード プロファイル、Visual Studio Code と ReSharper (Visual Studio) を利用し、ツール間でキーバインドの一貫性を維持できるようになりました。 これらのスキームは、 **[ツール]**  >  **[オプション]**  >  **[全般]**  >  **[キーボード]** および上部のドロップダウン メニューで見つけることができます。

  ![Visual Studio Code と ReSharper の新しいキー バインド プロファイル](media/vs-keyboard-mappings-code-resharper.png)

#### <a name="use-new-refactorings"></a>新しいリファクタリングの使用

リファクタリングは、コード作成後の改善プロセスです。 リファクタリングでは、動作を変更せずにコードの内部構造を変更します。 新しいリファクタリングが頻繁に追加されています。ここではいくつかの例を挙げます。

* パラメーターを追加する (CallSite から)
* オーバーライドを生成する
* 名前付き引数を追加する
* パラメーターの null チェックを追加する
* リテラルに桁区切り記号を挿入する
* 数値リテラルの基本を変更する (たとえば、16 進数を 2 進数に)
* if を switch に変換する
* 未使用の変数を削除する

詳細については、[クイック アクション](common-quick-actions.md)に関するページを参照してください。

#### <a name="interact-with-git"></a>Git との連携

Visual Studio でプロジェクトを操作する際に、コードを迅速にセットアップしてコミットし、Git サービスにコードを公開できます。 また、IDE の右下隅のボタンからメニュー クリックを使用して、Git リポジトリを管理することもできます。

![Visual Studio 2017 と Git の対話のダイアログ](media/vsIDE-GitInteraction.png)

#### <a name="experience-improved-navigation-controls"></a>操作性が改善されたナビゲーション コントロール

より確実に混乱なく A から B に移動できるようにナビゲーション エクスペリエンスを更新しました。

* **15.4 の新機能**:**定義へ移動** (**Ctrl** + **クリック**または **F12**) &ndash; マウスを使っているユーザーは、**Ctrl** キーを押しながらメンバーをクリックすることで、メンバーの定義に簡単に移動することができます。 **Ctrl** キーを押しながらコード記号の上にマウスを置くと、下線が引かれ、リンクに変わります。 詳細については、「[Go To Definition and Peek Definition](go-to-and-peek-definition.md)」([定義へ移動] および [定義をここに表示]) を参照してください。

* **実装に移動** (**Ctrl** + **F12**) &ndash; 任意の基本データ型やメンバーから各種実装に移動します。

* **すべてにジャンプ** (**Ctrl** + **T** または **Ctrl** + **,** ) &ndash; 任意のファイル/型/メンバー/シンボル宣言に直接移動します。 結果の一覧をフィルターしたり、クエリ構文 (例: ファイルは “f searchTerm”、型は “t searchTerm” など) を使用したりできます。

  ![[すべてにジャンプ] の改善](media/vs2017ide-navigation-go-to.png)

* **すべての参照の検索** (**Shift** + **F12**) &ndash; 構文の色付けにより、[すべての参照の検索] の結果をプロジェクト、定義、パスの組み合わせでグループ化できます。 また、結果を "ロック" して元の結果を失うことなく別の参照を検索できます。

  ![新しい [すべての参照の検索] ツール](media/vs2017ide-find-all-references.png)

* **Structure Visualizer\(構造ビジュアライザ\)** &ndash; 灰色の縦の点線 (インデント ガイド) がコード内のランドマークとしての役割を果たし、ビューのフレーム内のコンテキストを提供します。 おすすめの Productivity Power Tools で認識できます。 これを使用することで、スクロールすることなく現在作業しているコード ブロックを視覚化して検出できます。 行にカーソルを置くとツールチップが表示され、そのブロックの開始地点とその親を確認できます。 TextMate 文法を介してサポートされるすべての言語のほか、C#、Visual Basic、XAML で使用できます。

  ![Visual Studio 2017 の構造ビジュアライザー](media/vsIDE-StructureVisualizer.png)

新しい生産性機能について詳しくは、「[Visual Studio 2017: Productivity, Performance, and Partners (Visual Studio 2017: 生産性、パフォーマンス、およびパートナー)](https://devblogs.microsoft.com/visualstudio/visual-studio-2017-productivity-performance-and-partners/)」ブログ投稿をご覧ください。

### <a name="visual-c"></a>Visual C++

Visual Studio には、C++ Core ガイドラインの配信、C++11 および C++ 機能の拡張サポートを追加することによるコンパイラの更新、C++ ライブラリへの機能の追加および更新など、いくつかの改善が加えられています。 また、C++ IDE やインストールのワークロードなどのパフォーマンスも改善しました。

同時に 250 以上のバグを修正し、コンパイラおよびツールのイシューをレポートしてきました。その多くは [C++ の開発者コミュニティ](https://developercommunity.visualstudio.com/spaces/62/index.html "C++ の開発者コミュニティ")を通じてお客様から寄せられたものです。

詳細については、「[What's new for Visual C++ in Visual 2017](/cpp/top/what-s-new-for-visual-cpp-in-visual-studio)」 (Visual 2017 での Visual C++ の新機能) ページを参照してください。

### <a name="debugging-and-diagnostics"></a>デバッグと診断

#### <a name="run-to-click"></a>[Run To Click (クリックで実行)]

デバッグ中に必要な行に止まるためにブレークポイントを設定することなく、簡単に前方にスキップできるようになりました。 デバッガーが停止した場合は、コード行の横に表示されるアイコンをクリックします。 次にコード パスでその地点に到達すると、その行でコードが実行されて停止します。

![Visual Studio 2017 のデバッグ - クリックで実行](media/vs2017ide-RunToClick.png)

#### <a name="the-new-exception-helper"></a>新しい例外ヘルパー

新しい例外ヘルパーを使用すると、例外情報を一目で確認できます。 情報はコンパクトな形式で表示され、内部の例外に簡単にアクセスできます。 NullReferenceException を診断するときに、例外ヘルパー内の null をすばやく確認できます。

![Visual Studio の新しい例外ヘルパー ダイアログ](media/vs2017ide-ExceptionHelper.png)

詳細については、「[Use the new Exception Helper in Visual Studio](https://devblogs.microsoft.com/devops/using-the-new-exception-helper-in-visual-studio-15-preview/)」 (Visual Studio で新しい例外ヘルパーを使用する) のブログの投稿を参照してください。

#### <a name="snapshots-and-intellitrace-step-back"></a>スナップショットと IntelliTrace ステップ バック

**15.5 の新機能**:IntelliTrace のステップ バックでは、ブレークポイントとデバッガー ステップ イベントごとにアプリケーションのスナップショットを自動作成します。 記録されたスナップショットにより、前のブレークポイントまたはステップに戻り、過去の時点でのアプリケーションの状態を確認できるようになります。 IntelliTrace ステップ バックでは、以前のアプリケーションの状態を確認したいが、デバッグの再開や必要なアプリ状態の再作成は必要でない場合に時間を節約できます。

スナップショット間を移動して表示するには、**デバッグ** ツールバーの **[前に戻る]** ボタンと **[次へ進む]** ボタンを使用します。 これらのボタンを使用して、 **[診断ツール]** ウィンドウの **[イベント]** タブに表示されるイベント間を移動します。 あるイベントに戻るまたは進むと、選択したイベントの過去のデバッグが自動的に有効になります。

![Visual Studio の新しい例外ヘルパー ダイアログ](../debugger/media/intellitrace-step-back-icons-description.png  "[前に戻る] ボタンと [次へ進む] ボタン")

詳細については、「[IntelliTrace ステップ バックを使用してスナップショットを表示する](../debugger/view-historical-application-state.md)」のページ参照してください。

### <a name="containerization"></a>コンテナー詰め

コンテナーを使用することで、生産性と DevOps アジリティを高めるだけでなく、アプリの集積度を増やし、展開コストを下げることができます。

#### <a name="docker-container-tooling"></a>Docker コンテナーのツール

**15.5 の新機能**:

* Visual Studio には Docker コンテナー用のツールが含まれており、最適化されたコンテナー イメージの作成を効率化するマルチステージの Dockerfile がサポートされるようになりました。
* 既定では、Docker サポートが含まれるプロジェクトを開くと、Visual Studio が必要なコンテナー イメージをバックグラウンドで自動的にプル、ビルド、および実行します。 これは Visual Studio の **[コンテナーをバックグラウンドで自動的に開始する]** 設定で無効にすることができます。

## <a name="cloud-app-development-with-azure"></a>Azure によるクラウド アプリの開発

### <a name="azure-functions-tools"></a>Azure Functions ツール

"Azure 開発" ワークロードの一部として、コンパイル済みの C# クラス ライブラリを利用して Azure Functions を開発するためのツールを追加しました。 ローカルの開発マシンでビルドし、実行し、デバッグし、Visual Studio から Azure に直接公開できます。

詳細については、「[Azure Functions Tools for Visual Studio](/azure/azure-functions/functions-develop-vs)」 (Visual Studio の Azure Functions ツール) ページを参照してください。

### <a name="debug-live-aspnet-apps-using-snappoints-and-logpoints-in-live-azure-applications"></a>ライブ Azure アプリケーションでスナップショットとログポイントを使用して、ライブ ASP.NET アプリをデバッグする

**15.5 の新機能**:スナップショット デバッガーは、対象コードの実行時に実稼働アプリのスナップショットを取得します。 スナップショットを取得するようにデバッガーに指示するには、コードでスナップショットとログポイントを設定します。 デバッガーでは、実稼働アプリケーションのトラフィックに影響を与えることなく、問題を正確に確認できます。 スナップショット デバッガーは、実稼働環境で発生する問題の解決にかかる時間を大幅に短縮するのに役立ちます。

スナップショット コレクションは、Azure App Service で実行されている次の Web アプリで利用できます。

* .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
* Windows の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。

詳細については、[スナップショットとログポイントを使用するライブ ASP.NET アプリのデバッグ](../debugger/debug-live-azure-applications.md)に関するページを参照してください。

## <a name="windows-app-development"></a>Windows アプリ開発

### <a name="universal-windows-platform"></a>ユニバーサル Windows プラットフォーム

ユニバーサル Windows プラットフォーム (UWP) は Windows 10 用のアプリ プラットフォームです。 API セット、アプリ パッケージ、ストアをそれぞれ 1 つ使用するだけで、すべての Windows 10 デバイス (PC、タブレット、電話、Xbox、HoloLens、Surface Hub など) で利用可能な UWP 用アプリを開発できます。 UWP では、異なる画面サイズやさまざまな相互作用モデル (タッチ、マウスとキーボード、ゲーム コントローラー、ペン) がサポートされます。 UWP アプリの中核となるのは、ユーザーがすべてのデバイスでモバイル エクスペリエンスを手に入れたい、目の前の作業に最も便利または効率的なデバイスを使用したいという考え方です。

![ユニバーサル Windows プラットフォーム](../cross-platform/media/uwp_coreextensions.png)

希望する開発言語を &mdash;C#、Visual Basic、C++ または JavaScript の中から&mdash;選び、Windows 10 デバイスを対象とするユニバーサル Windows プラットフォーム アプリを作成します。 Visual Studio 2017 には、各言語の UWP アプリ テンプレートが用意されており、すべてのデバイスを対象とした単一のプロジェクトを作成できます。 作業が終わったら、アプリ パッケージを生成し、Visual Studio 内から Microsoft Store に提出できます。これで、すべての Windows 10 デバイスのユーザーにアプリが公開されます。

**15.5 の新機能**:Visual Studio 2017 バージョン 15.5 では、Windows 10 Fall Creators Update SDK (10.0.16299.0) の最適なサポートが提供されます。 また、Windows 10 Fall Creators Update により、UWP 開発者のための数多くの機能が強化されます。 最も大きな変更点をいくつか以下に示します。 

* **.NET Standard 2.0 のサポート**<br/>Windows 10 Fall Creators Update は、アプリ配置を効率化するだけでなく、.NET Standard 2.0 サポートを提供する Windows 10 の最初のリリースとなります。 実際には、[.NET Standard](https://devblogs.microsoft.com/dotnet/introducing-net-standard/) は、すべての .NET プラットフォームで実装できる基本クラス ライブラリの参照実装です。 .NET Standard の目的は、.NET 開発者が作業用に選択したすべての .NET プラットフォームでコードをできるだけ簡単に共有できるようにすることです。
* **UWP と Win32 の両方に長所**<br/>[デスクトップ ブリッジ](/windows/uwp/porting/desktop-to-uwp-root)を使用して Windows 10 プラットフォームを改善しました。これにより、現在のフォーカスが UWP、WPF、Windows Forms、または Xamarin のいずれにあるかに関係なく、すべての .NET 開発者は Windows 10 を改善することができます。 Visual Studio 2017 バージョン 15.5 の新しいアプリ パッケージング プロジェクト タイプを使用することで、UWP プロジェクトの場合と同じように、WPF または Windows Forms プロジェクトの Windows アプリケーション パッケージを作成できます。 アプリをパッケージ化すると、Windows 10 アプリ配置のすべての利点が得られ、Microsoft Store (コンシューマー アプリケーションの場合) または Microsoft Store for Business と Education を通じて配布することができます。 パッケージ化されたアプリは完全な UWP API 画面とデスクトップ上の Win32 API の両方にアクセスできるため、WPF および Windows Forms アプリケーションを UWP API および Windows 10 の機能で段階的に最新化できるようになりました。 さらに、すべての Win32 機能を使用して、デスクトップ上で点灯する UWP アプリケーションに Win32 コンポーネントを含めることができます。

UWP の詳細については、「[ユニバーサル Windows プラットフォーム (UWP) 向けアプリの開発](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md)」を参照してください。

## <a name="mobile-app-development"></a>モバイル アプリの開発

### <a name="xamarin"></a>Xamarin

".NET によるモバイル開発" ワークロードの一部として、C#、.NET、Visual Studio に詳しい開発者は Xamarin を利用し、Android、iOS、Windows のネイティブ アプリを開発できます。 開発者は、Android、iOS、および Windows デバイスでのリモート デバッグなど、モバイル アプリを Xamarin で開発する場合 &mdash; Objective-C または Java のようなネイティブのコーディング言語を習得しなくても、同じ機能と生産性を享受できます。

詳細については、「[Visual Studio と Xamarin](/xamarin/)」ページを参照してください。

### <a name="entitlements-editor"></a>権利エディター

**15.3 の新機能**:iOS 開発で必要になることから、スタンドアロンの権利エディターを追加しました。 使いやすい UI で簡単に閲覧できます。 *entitlements.plist* ファイルをダブルクリックすると起動します。

![Xamarin のエンタイトルメント エディター](media/xamarin-entitlements-editor.png)

### <a name="visual-studio-tools-for-xamarin"></a>Xamarin 用の Visual Studio ツール

**15.4 の新機能**:Xamarin Live では、開発者は iOS および Android デバイスで直接、アプリを継続的に展開、テストおよびデバッグできます。 Xamarin Live Player (&mdash;App Store または Google Play で利用可能&mdash;) をダウンロードした後、デバイスを Visual Studio とペアリングすることで、モバイル アプリの構築方法を一変させることができます。 この機能は、Visual Studio に含まれるようになりました。 **[ツール]**  >  **[オプション]**  >  **[Xamarin]**  >  **[Other] \(その他)**  >  **[Xamarin Live Player を有効にする]** で有効にすることができます。

![Xamarin Live Player のペアリング、展開、ライブ エディット モードのアニメーション](media/xamarinliveplayer.gif)

### <a name="support-for-google-android-emulator"></a>Google Android Emulator のサポート

**15.8 の新機能**:Hyper-V を使用するとき、Google の Android エミュレーターを、Hyper-V 仮想マシン、Docker ツール、HoloLens エミュレーターなど、Hyper-V ベースの他のテクノロジと並行して利用できるようになりました。 (この機能を利用するには、Windows 10 の 2018 年 4 月以降の更新プログラムが必要です。)

![Hyper-V テクノロジの Google Android Emulator](media/xamarin-hyperv-android-emulator.png)

#### <a name="xamarinandroid-designer-split-view-editor"></a>Xamarin.Android Designer 分割ビュー エディター

**15.8 の新機能**:デザイナーにとっての Xamarin.Android の使い勝手が大幅に改善されました。 ハイライトは、レイアウトを同時に作成、編集、プレビューできる新しい分割ビュー エディターです。

![Xamarin.Android Designer 分割ビュー エディター](media/android-designer-split-view.png)

詳細については、「[エミュレーター パフォーマンスのためのハードウェア高速化](/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin)」を参照してください。

### <a name="visual-studio-app-center"></a>Visual Studio アプリ センター

**15.5 の新機能**:Visual Studio App Center (Android、iOS、macOS、Windows アプリで現在一般公開されています) には、自動化されたビルド、クラウドの実際のデバイスでのテスト、ベータ テスターとアプリ ストアへの配布、クラッシュと分析データによる実際の使用状況の監視など、アプリのライフサイクルを管理するために必要なすべてのものがあります。 Objective-C、Swift、Java、C#、Xamarin、React Native で作成されたアプリはすべての機能でサポートされます。

  ![Visual Studio App Center のテスト環境](media/app-center-test-env.png)

詳細については、「[Introducing App Center: Build, Test, Distribute and Monitor Apps in the Cloud](https://blogs.msdn.microsoft.com/vsappcenter/introducing-visual-studio-app-center/)」 (App Center の概要: クラウドでのアプリのビルド、テスト、配布および監視) というブログ投稿を参照してください。

## <a name="cross-platform-development"></a>プラットフォーム間の開発

### <a name="redgate-data-tools"></a>Redgate Data Tools

DevOps 機能を SQL Server データベース開発に拡張するために、Visual Studio で Redgate Data Tools が利用できるようになりました。

Visual Studio 2017 Enterprise に付属:

* [Redgate ReadyRoll Core](https://www.red-gate.com/products/sql-development/sql-change-automation/?utm_source=microsoft&utm_medium=link&utm_campaign=readyroll&utm_term=docs-newinvs) は、移行スクリプトの開発、ソース管理によるデータベースの変更管理、アプリケーション変更と並行した SQL Server データベース変更の配置の安全な自動化に役立ちます。
* [Redgate SQL Prompt Core](https://www.red-gate.com/products/sql-development/sql-prompt/?utm_source=microsoft&utm_medium=link&utm_campaign=sqlprompt&utm_term=docs-newinvs) を利用すると、インテリジェントなコード入力候補機能により、SQL を短時間で正確に記述できます。 SQL Prompt は、データベース、システム オブジェクト、キーワードをオートコンプリートし、入力と同時に列の入力候補を提案します。 列の名前やエイリアスを覚える必要がないため、結果として、間違いが少なく、読みやすいコードが完成します。

Visual Studio 2017 のすべてのエディションに付属:

* [Redgate SQL Search](https://www.red-gate.com/products/sql-development/sql-search/?utm_source=microsoft&utm_medium=link&utm_campaign=sqlsearch&utm_term=docs-newinvs) では、複数のデータベースから SQL のフラグメントやオブジェクトをすばやく見つけることができ、生産性が向上します。

詳細については、ブログの投稿「[Redgate Data Tools in Visual Studio 2017](https://devblogs.microsoft.com/visualstudio/redgate-data-tools-in-visual-studio-2017/)」 (Visual Studio 2017 の Redgate Data Tools) を参照してください。

### <a name="net-core"></a>.NET Core

.NET Core は、モジュール形式のクロスプラットフォームかつオープン ソースを実装した汎用の .NET Standard です、.NET Framework と同じ API がたくさん含まれています。

.NET Core プラットフォームは複数コンポーネントで構成され、マネージド コンパイラ、ランタイム、基本クラス ライブラリ、および ASP.NET Core などの多数のアプリケーション モデルが含まれます。 .NET Core は、Windows、Linux、macOS の 3 つの主要オペレーティング システムをサポートしています。 .NET Core は、デバイス、クラウド、埋め込み/IoT のシナリオで使用できます。

Docker 対応にもなりました。

**15.3 の新機能**:Visual Studio 2017 バージョン 15.3 は .NET Core 2.0 開発に対応しています。 .NET Core 2.0 を使用するには、.NET Core 2.0 SDK を別にダウンロードし、インストールする必要があります。

詳細については、「[.NET Core ガイド](/dotnet/core/index)」ページを参照してください。

## <a name="games-development"></a>ゲーム開発

### <a name="visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity

"Unity のゲーム開発" ワークロードの一部として、2D ゲーム、3D ゲーム、対話型コンテンツを開発するためのクロスプラットフォーム開発に役立つツールを追加しました。 Visual Studio 2017 と Unity 5.6 を利用することで、1 回作成するだけですべてのモバイル プラットフォーム、WebGL、Mac、PC、Linux デスクトップ、Web、コンソールなど、21 のプラットフォームに発行できます。

詳しくは、「[Visual Studio Tools for Unity](../cross-platform/visual-studio-tools-for-unity.md)」 (Unity の Visual Studio ツール) をご覧ください。

## <a name="ai-development"></a>AI の開発

### <a name="visual-studio-tools-for-ai"></a>Visual Studio Tools for AI

**15.5 の新機能**:Visual Studio の生産性機能を使って今日の AI 革新を高速化します。 組み込みコード エディターの構文強調表示、IntelliSense、テキスト自動書式設定などの機能を使用します。 ローカル変数とモデルに対してステップ実行デバッグを使用して、ローカル環境でディープ ラーニング アプリケーションを対話的にテストできます。

  ![ディープ ラーニング IDE](../ai/media/about/ide.png)

詳細については、「[Visual Studio Tools for AI](../ai/about-ai-tools.md)」のページを参照してください。

## <a name="whats-next"></a>次の内容

Visual Studio 2017 は、より優れた開発を可能にする新機能で頻繁に更新されています。 現在、試験的プレビュー状態にある、特に重要な更新のいくつかをご紹介します。

* **[Live Share](https://visualstudio.microsoft.com/services/live-share/)** 。コードベースとそのコンテキストをチームメイトと共有し、Visual Studio 内で直接、双方向のインスタント コラボレーションができるようにする新しいツールです。 Live Share では自分が共有したプロジェクトをチームメイトがシームレスかつ安全に読み取り、移動、編集、デバッグすることができます。<br><br>詳細については、[Live Share の FAQ](/visualstudio/liveshare/faq) を参照してください。<br><br>
* **[IntelliCode](https://visualstudio.microsoft.com/services/intellicode/)** 。AI を使用してコンテキスト対応の優れた入力候補を提示したり、開発者のコードをチームのパターンとスタイルに誘導したり、見つけにくいコードの問題を検出したり、非常に重要な領域のコード レビューに注目したりすることでソフトウェア開発を拡張する新機能です。 <br><br>詳細については、[IntelliCode の FAQ](/visualstudio/intellicode/faq) を参照してください。

Visual Studio 2017 のその他の機能について知りたい場合は、 [Visual Studio のロードマップ](/visualstudio/productinfo/vs2018-roadmap)のページを参照してください。

また、最新バージョンの [Visual Studio 2019](whats-new-visual-studio-2019.md) を忘れずにチェック アウトしてください。

## <a name="contact-us"></a>お問い合わせ

Visual Studio チームにフィードバックを送ることにどんな意味があるのでしょうか? お客様からのフィードバックは、すべて真剣に考慮することにしています。 フィードバックによって今後の動向が左右されることになります。

Visual Studio を向上させることができる提案がある場合、または製品のサポート オプションについてさらに知りたい場合は、[フィードバックの送信](feedback-options.md)に関するページをご覧ください。

### <a name="report-a-problem"></a>問題を報告する

メッセージは、発生した問題の影響をすべて表せていない場合があります。 ハング、クラッシュ、またはその他のパフォーマンスの問題が発生した場合、 **[問題の報告]** ツールを使用すると、再現手順やサポート ファイル (スクリーン ショット、トレース ファイル、ヒープ ダンプ ファイルなど) を簡単に Microsoft と共有することができます。 このツールの使用方法については、「[問題を報告する方法](how-to-report-a-problem-with-visual-studio.md)」のページを参照してください。

## <a name="see-also"></a>関連項目

* [Visual Studio 2017 リリース ノート](/visualstudio/releasenotes/vs2017-relnotes)
* [Visual Studio 2017 SDK の新機能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)
* [Visual C++ の新機能](/cpp/top/what-s-new-for-visual-cpp-in-visual-studio)
* [C# の新機能](/dotnet/csharp/whats-new)
* [Team Foundation Server の新機能](/azure/devops/server/whats-new)
* [Visual Studio for Mac の新機能](https://visualstudio.microsoft.com/vs/visual-studio-mac/)
* [Visual Studio 2019 の新機能](whats-new-visual-studio-2019.md)
