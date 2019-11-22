---
title: Visual Studio 2015 の新機能 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.topic: conceptual
f1_keywords:
- VS.StartPage.WhatsNew
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 7307e180-ba28-4774-8a43-cbb980085a71
caps.latest.revision: 364
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 036ad2171c3b117049635247a980cd0f8411d887
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297565"
---
# <a name="what39s-new-in-visual-studio-2015"></a>Visual Studio 2015 の新機能
[!INCLUDE[vs2017banner](./includes/vs2017banner.md)]

Visual Studio 2015 へようこそ。これは開発者用の生産性ツール、クラウド サービス、および拡張機能の統合されたスイートであり、お客様およびチームが、Web、Windows ストア、デスクトップ、Android および iOS 用のアプリやゲームを作成できるようにするものです。

このページでは、Visual Studio 2013 RTM 以降新しくなったいくつかの重要な機能に焦点を当てています。これには Visual Studio 2013 更新プログラムのいずれかで最初に導入された機能が含まれます。 Visual Studio 2015 の新機能の完全な一覧については、 [リリース ノート](https://www.visualstudio.com/news/vs2015-vs)を参照してください。

To find out more about the many improvements and new features in Visual Studio ALM, see [What's new for TFS 2015](/tfs/server/whats-new?view=vsts#tfs-2015-rtm).

## <a name="a-new-setup-experience"></a>新しいセットアップ エクスペリエンス
 [!INCLUDE[downloadvs](./includes/downloadvs-md.md)]

 Visual Studio 2015 のセットアップ エクスペリエンスはコンポーネント化されており、必要な部分のみをインストールするだけで済みます。 これにより、.NET または Web の開発に関連する多くの一般的なシナリオをより短い時間でインストールできます。 クロス プラットフォーム モバイル開発などの他の種類の開発を行う場合、または C++ や F# で作業する場合は、 **[カスタム]** インストールを選択した後、必要なコンポーネントとオプションのサードパーティ製 SDK を選択してください。 カスタム コンポーネントはいずれも、後でインストールすることもできます。 たとえば、基本インストールを選択した後、新しい C++ プロジェクトを作成しようとすると、C++ 開発ツールをダウンロードするように求められます。

 ![Visual Studio 2015 Setup Dialog](./ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

## <a name="sign-in-across-multiple-accounts"></a>複数のアカウント間のサインイン
 Visual Studio 2015 では、サインインの仕組みがすっきりとしたものに更新されており、Visual Studio のアカウントが複数ある場合でもオンライン リソースへのアクセスが大幅に簡素化されるように設計されています。 Visual Studio にサインインすると、Visual Studio 2015 およびコンピューター上の Blend のすべてのインスタンスに自動的にサインインします。 サインインすると、自動的に設定のローミングが開始されます。 Visual Studio 2015 では、複数の機能で 1 つのアカウントを共通に使うことができるため、トークンが良好なものである限り、 **チーム エクスプローラー**から Visual Studio Team Services のアカウントにアクセスしたり、サーバー エクスプローラー内の自分の Microsoft Azure サブスクリプションからさまざまなリソースや Web サイトにアクセスしたりすることが可能です。 また、Application Insights のプロジェクトの [新しいプロジェクト] ダイアログに自分の Azure リソースが表示されます。さらに、新しい [[接続済みサービスの追加]](https://msdn.microsoft.com/office/aa905340.aspx) ダイアログには、Azure Mobile、Azure Storage、 [Microsoft Office 365](https://developer.salesforce.com/) 、および **Saleforce.com developer** のアカウントが表示されます。

 新しいアカウント マネージャーを実行する際に複数のユーザー アカウントを追加することによって、Visual Studio でそれらのユーザー アカウントの作業を実行できます。 そのようにすることによって、さまざまなサービスに接続したりオンライン リソースにアクセスしたりする際に、それら複数のアカウントを自在に切り替えることができます。 Visual Studio では追加されたアカウントが記憶されるため、Visual Studio または Blend のすべてのインスタンスからそれらを使用できます。 Visual Studio は、パーソナル化アカウントを使ってアカウントのリストもローミングし (重要な資格情報はローミングしません)、それらのアカウントの 1 つを使って別のデバイスですばやく操作できるようにします。 もちろん、[アカウント設定] ダイアログ ボックスでいつでもアカウントを削除できます。 開始するには、「 [Work with multiple user accounts](./ide/work-with-multiple-user-accounts.md)」を参照してください。

 ![Account Manager](./ide/media/vs2015-accountmanager.gif "VS2015_AccountManager")

## <a name="choose-your-target-platforms"></a>ターゲット プラットフォームの選択
 Visual Studio 2015 は、クロス プラットフォームのモバイル デバイス開発をサポートします。 iOS、Android、および Windows を対象とするアプリやゲームを作成し、共通コード ベースを (すべて Visual Studio IDE 内から) 共有できます。 [ファイル] の [新しいプロジェクト] ダイアログ ボックスにさまざまな種類の新しいプロジェクトが表示されます。

 また当然のことながら、言語、ライブラリ、およびツールに多くの改善が加えられたため、クラシック デスクトップ アプリケーションのサポートは、以前より優れています。

### <a name="cross-platform-mobile-apps-in-c-with-xamarin-for-visual-studio"></a>Xamarin for Visual Studio を使った C# のクロス プラットフォームのモバイル アプリ
 Xamarin は、iOS および Android API にネイティブでバインドされるコードを C# で記述するためのモバイル フレームワークです。 Microsoft は、Xamarin for Visual Studio のリリースに伴い Xamarin と密接に働いてきました。Xamarin for Visual Studio は、単一のソリューションで共有コードを使用して Android、iOS、および Windows Phone 用に開発するための拡張機能です。 Xamarin では、プラットフォーム間の差分が最小限である 1 つの言語と 1 つのコード ベースを使用します。  Xamarin for Visual Studio は Visual Studio 2010 以降でサポートされています。 Xamarin のスタート エディションは、Visual Studio 2015 に含まれます。 To get started, see [Build apps with native UI using Xamarin in Visual Studio](./cross-platform/build-apps-with-native-ui-using-xamarin-in-visual-studio.md).

### <a name="cross-platform-mobile-apps-in-htmljavascript-with-apache-cordova"></a>Apache Cordova を使った HTML/JavaScript のクロス プラットフォームのモバイル アプリ
 Visual Studio Tools for Apache Cordova は、Microsoft とオープン ソース Apache Cordova コミュニティとの密接な共同作業の成果物です。 これらのツールは、HTML、CSS、および JavaScript (または Typescript) を使用したクロス プラットフォームのモバイル開発を可能にします。 1 つのコード ベースを使用して Android、iOS、および Windows を対象とし、Visual Studio IDE に含まれる JavaScript IntelliSense、DOM Explorer、JavaScript コンソール、ブレークポイント、ウォッチ、ローカル、Just My Code などの豊富な機能を利用できます。  Visual Studio Tools for Apache Cordova では、一般的な JavaScript API を提供するプラグインによってすべてのプラットフォーム上のネイティブ デバイス機能にアプリがアクセスできるようになります。 To get started, see [Get Started with Visual Studio Tools for Apache Cordova](https://msdn.microsoft.com/library/db446f2c-6ba4-4c76-aac5-4c66f43b8c42).

### <a name="cross-platform-mobile-games-in-c-with-unity"></a>Unity を使った C# のクロス プラットフォームのモバイル ゲーム
 Unity は、マルチプラットフォームの 2D および 3D ゲーム開発用に広く使用されているプラットフォームです。 ゲームを C# で作成し、Android、iOS、Windows Phone、その他の多くのプラットフォームでネイティブに実行できます。 Visual Studio Tools for Unity は、Unity と Visual Studio IDE を統合させる拡張機能です。 この拡張機能により、Unity 開発者用に設計された生産性機能に加えて、Visual Studio IDE のすべての機能とデバッガーが使用できるようになります。 Visual Studio Tools for Unity 2.0 Preview 2 には Visual Studio 2015 のためのサポートが追加されており、さらに [ローカル] ウィンドウや [ウォッチ] ウィンドウでのオブジェクト表示方法の改善など、数々の機能が新たに追加されています。 Microsoft は最近、Visual Studio Tools for Unity の作成元の SyntaxTree を買収しました。 Visual Studio Tools for Unity 2.0 Preview 2 のダウンロードおよび Visual Studio Tools for Unity の詳細については、「 [Visual Studio による Unity ゲームのビルド](https://aka.ms/vstu)」を参照してください。

### <a name="cross-platform-apps-and-libraries-for-native-c"></a>ネイティブ C++ 用のクロス プラットフォーム アプリおよびライブラリ
 C++ は、ほとんどのモバイル デバイスでネイティブに使用可能な言語です。 C++ を使用すると、複数のモバイル プラットフォーム ターゲット用にビルドできるクロス プラットフォームの共有コード ライブラリを作成できます。 モバイル アプリ全体を C++ で作成することもできます。 Visual C++ には、クロス プラットフォームのコードを編集、ビルド、配置、およびデバッグするためのツールが用意されています。 Windows アプリ用のテンプレートだけでなく、Android Native Activity アプリ用のプロジェクト、iOS アプリ用のプロジェクト、または Xamarin ハイブリッド アプリを含む複数のプラットフォーム用の共有コード ライブラリ オブジェクトも、テンプレートから作成できます。 プラットフォーム固有の IntelliSense を使用すると、API を調べて、Android ターゲット、iOS ターゲット、または Windows ターゲット用の正しいコードを生成することができます。 x86 または ARM ネイティブ プラットフォーム用のビルドを構成し、iOS シミュレーターやネットワークに接続された Mac 上の iOS デバイスにコードを配置したり、直接接続された Android デバイスにコードを配置したり、パフォーマンスの優れた Microsoft Visual Studio Emulator for Android をテストに使用したりできます。 Visual Studio デバッガーでは、ブレークポイントやウォッチ変数の設定、スタックの表示、C++ コードのステップスルー実行が可能です。 最も固有性の高いプラットフォームのコード以外のすべてのコードを複数のアプリ プラットフォームで共有し、Visual Studio の 1 つのソリューションでそれらをすべてビルドすることができます。

 To get started on cross-platform C++, see [Build cross-platform mobile apps with Visual C++](./misc/build-cross-platform-mobile-apps-with-visual-cpp.md)

### <a name="universal-windows-apps-for-any-windows-10-device"></a>任意の Windows 10 デバイス用のユニバーサル Windows アプリ
 ユニバーサル Windows プラットフォームと 1 つの Windows コアを使用することで、電話やデスクトップなどの Windows 10 デバイスで同じアプリを実行できます。 これらのユニバーサル Windows アプリは、Visual Studio 2015 とユニバーサル Windows アプリ開発ツールを使用して作成します。

 ![ユニバーサル Windows プラットフォーム](./cross-platform/media/uwp-coreextensions.png "UWP_CoreExtensions")

 アプリを Windows 10 Phone、Windows 10 デスクトップ、または Xbox で実行します。 同じアプリケーション パッケージが使用されています。 Windows 10 の単一の統一されたコアの導入により、1 つのアプリケーション パッケージをすべてのプラットフォームで実行できます。 いくつかのプラットフォームには、プラットフォーム固有の動作を利用するためにアプリに追加できる拡張 SDK があります。 たとえば、モバイル用の拡張 SDK を使用すれば、Windows Phone で [戻る] ボタンを処理できます。 プロジェクトで拡張 SDK を参照する場合、単純にランタイム チェックを追加して、プラットフォームでその SDK を使用できるかどうかをテストします。 このようにして、それぞれのプラットフォームで同じアプリケーション パッケージを使用できます。

 これらの [ユニバーサル Windows アプリ](https://msdn.microsoft.com/library/dn975273.aspx)を作成するには、C#、Visual Basic、C++、または JavaScript を使用します。

### <a name="web"></a>Web
 ASP.NET 5 は、MVC、WebAPI、および SignalR へのメジャー アップデートであり、Windows、Mac、および Linux で実行されます。  ASP.NET 5 は、最新のクラウド ベースのアプリをビルドするための効率的で構成可能な .NET スタックを提供するために、まったく新たに設計されました。 Visual Studio 2015 ツーリングは、Bower や Grunt などの一般的な Web 開発ツールと、より緊密に統合されています。 開始するには、「  [NET Web Development and Tools Blog](https://devblogs.microsoft.com/aspnet/)」にある多くのブログ投稿を参照してください。

### <a name="classic-desktop-and-windows-store"></a>クラシック デスクトップと Windows ストア
 Visual Studio 2015 は引き続きクラシック デスクトップと Windows ストアの開発をサポートします。 Windows の進展に伴って、Visual Studio も進化を遂げています。  Visual Studio 2015 では、.NET や C++ のライブラリや言語が著しく改良され、Windows のすべてのバージョンに適用されるようになりました。

#### <a name="the-net-framework"></a>.NET Framework
 Microsoft [!INCLUDE[net_v46](./includes/net-v46-md.md)] では、約 150 の API が新たに提供され、50 の API が更新されて、これまで以上に多くのシナリオに対応できるようになっています。 たとえば、さらに多くのコレクションで <xref:System.Collections.Generic.IReadOnlyCollection%601> が実装され、使いやすさの点で向上しています。 さらに前述の ASP.NET 5 では、最新のクラウド ベース アプリをビルドするための .NET プラットフォームがすっきりとした形で提供されています。

 .NET Framework をターゲットとして C# で書かれた Windows ストア アプリで、.NET Native を利用できるようになり、アプリを IL ではなくネイティブ コードにコンパイルすることが可能になりました。また、 [!INCLUDE[net_v46](./includes/net-v46-md.md)] には 64 ビット Just-In-Time (JIT) コンパイラーである RyuJIT も追加されています。

 C# および VB の新しいコンパイラー ("Roslyn") では、コンパイル時間が大幅に短縮されており、総合的なコード分析 API が提供されています。 Visual Studio 2015 では、Roslyn を利用することにより、インラインのリネーム、アナライザー、その場で修正する機能など、さらに多くのリファクタリング機能が提供されています。

 C# 言語と Visual Basic 言語には、両方ともコア言語と IDE サポートに多数の小さな改良が見られます。 それらの改良のすべてにより、.NET のコーディング作業がさらに便利かつ直感的になり、生産性が向上します。

 For more information, see [What's New](https://msdn.microsoft.com/library/1d971dd7-10fc-4692-8dac-30ca308fc0fa) and the [.NET Blog](https://devblogs.microsoft.com/dotnet/).

#### <a name="c"></a>C++
 Visual C++ は、C++11/14 言語への準拠、クロス プラットフォーム モバイル デバイス用開発のサポート、再利用可能関数および await (現在 C++17 での標準化に向けて検討中) のサポート、C ランタイム ライブラリ (CRT) および C++ 標準ライブラリ (STL) の実装における数々の改良とバグ修正、MFC でのサイズ変更可能なダイアログ、コンパイラの新しい最適化機能、ビルド パフォーマンスの改善、新しい診断機能、コード エディターでの新たな生産性向上ツールの点で大きく前進しています。

 For more information, see [What's New for Visual C++](https://msdn.microsoft.com/library/1cc09fad-85a2-43c2-b022-bb99f5fe0ad7) and the [Visual C++ Blog](https://devblogs.microsoft.com/cppblog/).

## <a name="device-preview-menu-bar"></a>[デバイスのプレビュー] メニュー バー
 ユニバーサル Windows プラットフォーム プロジェクトでは、[デバイスのプレビュー] メニュー バーを使用して、XAML ベースの UI がさまざまな画面サイズでどのように表示されるかを確認できます。

 ![Device Preview menu](./ide/media/vs2015-device-preview.png "vs2015_device_preview")

## <a name="visual-studio-graphics-diagnostics"></a>Visual Studio グラフィックス診断
 Visual Studio 2013 では、Visual Studio グラフィックス診断に、フレーム分析、Windows Phone のサポート、シェーダーの編集と適用、コマンド ライン キャプチャ ツールなど、多くの新機能が追加されています。 DirectX12 アプリのデバッグのサポートも追加されています。 詳しくは、「 [Visual Studio グラフィックス診断](./debugger/visual-studio-graphics-diagnostics.md)」をご覧ください。

## <a name="connect-to-services"></a>サービスへの接続
 Visual Studio 2015 により、サービスへのアプリの接続がさらに簡単になりました。  新しい [接続済みサービスの追加] ウィザードは、プロジェクトを構成し、必要な認証サポートを追加し、必要な NuGet パッケージをダウンロードして、サービスに対してすばやくかつ簡単にコーディングを開始できるようにします。 さらに、[接続済みサービスの追加] ウィザードは新しいアカウント マネージャーと統合され、複数のアカウントおよびサブスクリプションでの操作が簡単になります。 Visual Studio 2015 では、以下のサービスのためのサポートがすぐに利用できます (アカウントを持っていることを前提としています)。

1. Azure モバイル サービス

2. Azure ストレージ

3. Office 365 (メール、連絡先、カレンダー、ファイル、ユーザーおよびグループ)

4. Salesforce

   新しいサービスは継続的に追加されます。それらのサービスは、ウィザードで [新しいサービス リンクの検索] をクリックして検索できます。

   ![Add Connected Services Dialog](./ide/media/vs2015-addconnectedservicedialog.png "VS2015_AddConnectedServiceDialog")

## <a name="design-your-ui"></a>UI の設計
 XAML ユーザー インターフェイスを設計するための Blend の機能が大幅に強化されました。 Blend が完全に再設計されたことにより、より直感的な UI が提供され、IntelliSense などの XAML 編集機能が強化され、Visual Studio との統合性が向上しました。 詳細については、[Visual Studio および Blend for Visual Studio での XAML デザインに関する記事](./designers/designing-xaml-in-visual-studio.md)を参照してください。

## <a name="cross-platform-debugging-support"></a>クロスプラットフォームのデバッグのサポート
 Visual Studio を使用して、Windows、iOS、Android の各デバイスで実行されるネイティブ モバイル アプリを作成、デバッグすることができます。 [Visual Studio Emulator for Android](https://devblogs.microsoft.com/devops/introducing-visual-studios-emulator-for-android/)を使用するか、またはデバイスを接続し、Visual Studio で直接コードをデバッグします。

- **JavaScript / Cordova**。 JavaScript で Windows、iOS、Android のネイティブ アプリを作成するには、 [Visual Studio Tools for Apache Cordova](https://msdn.microsoft.com/library/dn879821\(v=vs.140\).aspx) を使用します。

     [Debug Your App](https://msdn.microsoft.com/library/c2a4a1d4-a4e8-47ec-811f-ad207c54f4d1) in the MSDN Library is a detailed look at Visual Studio debugging support for Cordova.

- **C# / Xamarin**。 [Xamarin](https://msdn.microsoft.com/library/dn879698\(v=vs.140\).aspx) を使用し、C# を使って Visual Studio で Windows、iOS、および Android のネイティブ アプリを作成します。

     デバッグ機能については、[Xamarin 開発者ガイド](https://docs.microsoft.com/xamarin/ios/deploy-test/debugging-in-xamarin-ios?tabs=windows) の「 [Debugging](https://docs.microsoft.com/xamarin/android/deploy-test/debugging/debug-on-device?tabs=windows) 」 (iOS) および「 [Debug on Device](https://docs.microsoft.com/xamarin/) 」で説明されています。

- **C++ / Android**。 [Visual C for Cross-platform Mobile Development](cross-platform/visual-cpp-for-cross-platform-mobile-development.md) テンプレートを [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) などのサード パーティ製ツールとともに使用して、Windows および Android のネイティブ アプリを作成します。

## <a name="debugging-and-diagnostics"></a>デバッグと診断

For information about what’s new in diagnostics, see [What's New in Profiling Tools](./profiling/what-s-new-in-profiling-tools.md).

次に示すのは、コードに対して異なる種類の診断および分析を実行する新しいツールまたは機能強化されたツールです。

### <a name="perftips"></a>パフォーマンスのヒント
 パフォーマンスのヒントはデバッグ中のメソッドの実行時間を表示し、プロファイラーを呼び出すことなくボトルネックをすばやく見つけることができるようになります。 開始するには、「 [PerfTips: Performance Information at-a-glance while Debugging with Visual Studio](https://devblogs.microsoft.com/devops/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)」を参照してください

### <a name="error-list"></a>エラー一覧
 エラー一覧はあらゆる列のフィルター処理をサポートするようになりました。 また入力時の C# または Visual Basic ソリューション全体におけるエラー、警告、コード分析を、コードの変更によって大量の警告が発生したとしてもライブで表示します。 新しいエラー一覧は既存の使用方法と後方互換性があります。 詳細については、「 [Error List Window](./ide/reference/error-list-window.md)」を参照してください。

### <a name="gpu-usage-tool"></a>GPU 使用率ツール
 GPU 使用率ツールは、DirectX アプリやゲームの GPU 使用率データの収集と分析、およびパフォーマンスのボトルネックが CPU または GPU で発生したかどうかをトラブルシューティングするのに役立ちます。 このツールを開始するには、 [Visual C チーム ブログの投稿](https://devblogs.microsoft.com/cppblog/gpu-usage-tool-in-visual-studio-2013-update-4-ctp1/)を参照してください。

## <a name="live-code-analysis-light-bulbs"></a>ライブ コード分析 (電球)
 C# および Visual Basic 用の新しい Roslyn コンパイラが提供するのはコンパイル時間の短縮だけではありません。ライブ コード分析などのまったく新しいシナリオが可能になります。これにより、入力時に豊富でカスタマイズ可能なフィードバックや提案が直接コード エディター内で提供されます。 Visual Studio 2015 では、キーボードを使用すると電球が左マージンに表示され、エラーの上にマウス ポインターを置くとツール ヒントが表示されます。 電球は、コンパイラが (おそらくカスタム規則セットを使用して) コード内の問題を検出し、その問題を修正する方法に関する提案があることをリアルタイムで表示します。 電球が表示された場合は、クリックしてアクション可能な提案を確認します。

 ![Light Bulbs in Visual Studio Code Editor](./ide/media/vs2015-lightbulbs.png "VS2015_LightBulbs")

## <a name="enjoy-these-additional-ide-improvements"></a>その他の IDE の強化された機能の活用

### <a name="synchronized-settings-roaming-settings"></a>同期された設定 (ローミング設定)
 Visual Studio 2013 には、テキスト エディター、ショートカット キー、テーマ & フォント & 色、スタートアップ、および環境エイリアスなどの最も一般的に構成されている設定のいくつかに対して、同期された設定が導入されています。  Visual Studio 2015 では、さらに多くの設定を同期し、Professional、Enterprise、Express SKU、Blend などの Visual Studio ファミリのアプリケーション間で設定を同期するように、この機能が改良されています。 Visual Studio 2013 で使用したアカウントで Visual Studio 2015 に初めてサインインすると、Visual Studio 2013 から適用された同期された設定が表示されます。 設定にアクセスするには、 **[クイック起動]** に「sync」と入力するか、 **[ツール] > [オプション] > [環境] > [同期された設定]** に移動します。

### <a name="automatic-extension-updates"></a>拡張機能の自動更新
 インストールされている Visual Studio の拡張機能は、Visual Studio ギャラリーで新しいバージョンが使用可能なときに、自動的に更新されるようになりました。 拡張機能の自動更新をカスタマイズする方法の詳細については、「 [Visual Studio の拡張機能を検索および使用する](./ide/finding-and-using-visual-studio-extensions.md) 」を参照してください。

### <a name="title-case-menus"></a>メニューの先頭文字の大文字指定
 お客様の声に基づいて調整されました。 Visual Studio のメニューは再び既定で先頭文字が大文字に指定されます。 ただし、すべて大文字のスタイルを希望する場合は、起動時または **[ツール] > [オプション] > [全般]** プロパティ ページで設定できます。

 ![Visual Studio 2015 Title Case Main Menu Commands](./ide/media/vs2015-mainmenu.png "VS2015_MainMenu")

### <a name="high-resolution-images-and-touch-support"></a>高解像度のイメージとタッチ サポート
 Visual Studio IDE では、高密度ディスプレイ (メニュー、コンテキスト メニュー、ツール ウィンドウのコマンド バーなどのエリアやソリューション エクスプローラー内のいくつかのプロジェクト) での高解像度のイメージが実現しました。 また、Visual Studio のコード エディター ウィンドウのタッチ スクリーンでは、タッチしてホールド、ピンチ、タップなどの動作を使って、ズーム、スクロール、テキストの選択、およびコンテキスト メニューの呼び出しができるようになりました。

 ![Touch support in editor](./ide/media/vs2015-touchsupport.png "VS2015_TouchSupport")

### <a name="custom-layouts"></a>カスタム レイアウト
 ストアを作成し、カスタム ウィンドウ レイアウトをローミングできます。 たとえば、お気に入りのレイアウトを 1 つデスクトップ コンピューターで使用するために定義し、異なるレイアウトをノート PC や画面の小さいデバイスで使用するために定義できます。 または、UI プロジェクト用にレイアウトを 1 つ選択し、データベース プロジェクト用に別のレイアウトを選択できます。 ショートカット キーを使用してすばやくレイアウトを切り替えられます。 これらのレイアウトは、サインイン中であれば Visual Studio のすべてのインスタンスで使用できます。 詳細については、「 [カスタム ウィンドウ レイアウトを作成する](./misc/create-custom-window-layouts.md)」を参照してください。

 ![Visual Studio Custom Layout menu item](./ide/media/vs2015-customlayout.png "VS2015_CustomLayout")

### <a name="notification-hub"></a>通知ハブ
 スキャンを簡単にするために、通知ハブの UI が効率化されています。 パフォーマンスの問題、レンダリングの問題、クラッシュなどの通知の種類が追加され、Visual Studio に通知の表示停止を指示できるようになりました。 詳細については、「 [Visual Studio の通知](./ide/visual-studio-notifications.md)」を参照してください。

### <a name="codelens-find-what-happened-to-your-code-enterprise-and-professional-editions-only"></a>CodeLens: コードに何が起こったかを検索します (Enterprise Edition と Professional Edition のみ)。
 エディターを離れずにコードに関する情報を検索できるため、自分の作業に専念できます。 Visual Studio Team Services (VSTS) または Team Foundation Server (TFS) に格納されているコードについて、作業項目、バグ、コード レビューなどの変更やその他の履歴を確認できます。

 Visual Studio Enterprise と Visual Studio Professional で、次の操作を実行できるようになりました。

- Visual Studio エディターでコード ファイル全体の履歴を取得する。

   ![CodeLens: Get code file details](./ide/media/codelensfilelevel.png "CodeLensFileLevel")

- コードを変更したユーザーを示すグラフを表示する。 これは、チームでの変更のパターンを見つけて影響を評価するために役立ちます。

   ![CodeLens: See code changes history as a graph](./ide/media/codelens.png "CodeLens")

- コードの最終変更日時を簡単に分かるようにする。

- 自分のコードに影響を与える、他の分岐での変更を検索できます。

  「 [CodeLens](./ide/find-code-changes-and-other-history-with-codelens.md)」を参照してください。

### <a name="design-and-modeling-tools-enterprise-edition-only"></a>設計およびモデリング ツール (Enterprise エディションのみ)
 **コード マップと依存関係グラフ**

 Visual Studio Enterprise では、コード内の具体的な依存関係を理解するには、コード マップを作成して視覚化します。 コードの横に表示されるマップを使用して、これらの関係をナビゲートできます。 コード マップを使用すると、コードの作業中またはデバッグ中にコード内での場所を追跡でき、少ないコードを読むだけで、コードの設計の多くを把握できます。

 このリリースでは、コマンドが選択、編集、管理の単位でセクションにグループ化され、グループの内容のレイアウトが変更されて、コード要素のショートカット メニューとリンクがずっと使いやすくなりました。 また、テスト プロジェクトが他のプロジェクトとは異なるスタイルで表示されること、およびマップの要素のアイコンがさらに適切なバージョンに更新されたことにも注意してください。

 ![Show selected items on a new code map](./ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")

 その他の改良点は次のとおりです。

- **改良されたトップダウン ダイアグラム**。 中規模から大規模な Visual Studio ソリューションでは、単純化された [アーキテクチャ] メニューを使用して、ソリューションのさらに便利なコード マップを取得できます。 ソリューションのアセンブリがソリューション フォルダーごとにグループ化されたため、コンテキストに応じてアセンブリを参照でき、ソリューションの構造を作成したときの作業を活用できます。 プロジェクトとアセンブリの参照がすぐに表示され、リンクの種類が表示されます。 さらに、ソリューションの外部のアセンブリが、よりコンパクトな方法でグループ化されます。

- **テスト プロジェクトが異なるスタイルになり、フィルター処理できます**。 テスト プロジェクトのスタイルが異なるため、マップで簡単かつ迅速に識別できます。 また、アプリケーションの作業中のコードに集中できるようにフィルターで除外できます。

- **簡略化された外部依存関係リンク**。 依存関係リンクで System.Object、System.ValueType、System.Enum、System.Delegate からの継承が表示されなくなり、コード マップで外部依存関係を確認しやすくなりました。

- **依存関係リンクへのドリルインでフィルターが考慮されます**。 展開すると役に立つクリアなダイアグラムが表示され、依存関係リンクへの寄与を理解できます。 ダイアグラムはわかりやすく、選択したフィルター選択オプションが考慮されます。

- **コード要素がコンテキストでコード マップに追加されます**。 ダイアグラムはコンテキストで表示されるので (必要に応じて除外できるアセンブリおよびソリューション フォルダーまで)、ソリューション エクスプローラー、クラス ビュー、オブジェクト ブラウザーからコード要素をドラッグ アンド ドロップしたとき、またはソリューション エクスプローラーで要素を選択して [コード マップに表示] を選択したときに、役に立つダイアグラムが表示されます。

- **反応型のコード マップを迅速に取得します**。 ドラッグ アンド ドロップ操作によってすぐに結果が生成され、ノード間のリンクがより迅速に作成されて、ノードの展開やより多くのノードの要求などの後続のユーザー開始操作に影響がありません。 ソリューションを作成しないでコード マップを作成すると、すべてのコーナー ケース (アセンブリがビルドされないときなど) が処理されます。

- **ソリューションのリビルドをスキップします。** ダイアグラムを作成して編集するときのパフォーマンスが向上します。

- **コード要素ノードとグループをフィルター処理します**。 カテゴリに基づいてコード要素を表示または非表示したり、ソリューション フォルダー、アセンブリ、名前空間、プロジェクト フォルダー、種類ごとにコード要素をグループ化することで、マップをすばやく整理できます。

- **リレーションシップをフィルターにかけて図を見やすくします**。 リンクのフィルター処理がクロス グループ リンクにも適用されるようになり、以前のリリースと比べてフィルター ウィンドウでの操作の関与レベルが低くなります。

- **クラス ビューおよびオブジェクト ブラウザーからダイアグラムを作成します**。 クラス ビューおよびオブジェクト ブラウザー ウィンドウから新規マップまたは既存マップにファイルとアセンブリをドラッグ アンド ドロップします。

  「 [Map dependencies across your solutions](./modeling/map-dependencies-across-your-solutions.md)」を参照してください。

  **このリリースでの設計とモデリングに関する他の変更:**

- **レイヤー図**。 クラス ビューとオブジェクト ブラウザーを使用してこれらの図を更新できます。 ソフトウェア設計要件を満たすには、レイヤー図を使用してソフトウェアの必要な依存関係を記述します。 これらの制約を満たしていないコードを探し、この基準で将来のコードを検証することにより、コードをこの設計と一致させます。

- **UML 図**。 コードから UML クラス図やシーケンス図を作成できなくなりました。 これらの図は新しい UML 要素を使って作成できます。

- **アーキテクチャ エクスプローラー**。 アーキテクチャ エクスプローラーを使ってダイアグラムを作成できなくなりました。 しかし、ソリューション エクスプローラーを使って引き続き作成できます。

## <a name="visual-studio-extensibility-tools"></a>Visual Studio 機能拡張ツール
 Visual Studio 機能拡張ツール (VS SDK とテンプレート) はセットアップ中にオプション コンポーネントとして含まれているので、そのインストールが今まで簡易化されたことはありません。  機能拡張ツールを使用すると、開発者は拡張機能を記述して、Visual Studio に機能をカスタマイズしたり、追加したりできます。 Visual Studio の機能拡張の詳細については、「 [Visual Studio SDK](./extensibility/visual-studio-sdk.md)」を参照してください。

 カスタム インストールを使用して、機能拡張ツールを含める場合は、 **[機能] / [一般的なツール] / [Visual Studio 機能拡張ツール]** で検索してください。  **[新しいプロジェクト]** ダイアログを開き、 **[Visual C#] / [機能拡張]** の下にある **[Visual Studio 機能拡張ツールをインストールする]** の項目を選択して、後で機能拡張ツールをインストールすることもできます。

## <a name="please-give-feedback"></a>フィードバックをお送りください
 Visual Studio チームにフィードバックを送ることにどんな意味があるのでしょうか? お客様からのフィードバックは、すべて真剣に考慮することにしています。 事実、フィードバック システムに寄せられるフィードバックの各部分のそれぞれを 1 つずつ検討することになっています。 お寄せいただくフィードバックが、今後の動向を左右することになるのです。

### <a name="send-a-smile"></a>気に入った機能の報告
 感想をお伝えいただくなら、ユーザーの皆様の期待に応じることができたかどうかを確認する助けになります。 さまざまな機能についてご提供いただいたデータは、新しい機能を設計実装する際に、設計の意思決定の参考として使用します。 Visual Studio で実現してほしい機能が何かありましたら、それについてお知らせください。 その方法は簡単です。IDE から直接行うことができます。

 タイトル バーにある黄色の笑顔マークをクリックして、感想を記入した後、 **[気に入った機能の報告]** ボタンをクリックするだけです。

 それで完了です! お送りいただいたフィードバックは、該当するチームに送られます。受け取ったチームにとって、それは大いに励みとなり、担当者はご要望に応えるさらに良い方法を考えることにとりかかることでしょう。

### <a name="send-a-frown"></a>問題点、改善点の報告
 製品のどこをどう改善したらよいかについてご意見をお寄せいただくなら、今後の作業においてお客様が最も気にかけておられる点を優先的に取り上げることができます。 何か気になる点がありましたら、IDE の中から直接に **[問題点、改善点の報告]** 機能を使用してご報告ください。 そのプロセスも極めてシンプルなものにしてあります。

 タイトル バーにある黄色の笑顔マークをクリックしてから、 **[問題点、改善点の報告]** をクリックします。 気になる点について記入した後、[問題点、改善点の報告] ボタンをクリックしてください。 詳細については、「 [Talk to Us](./ide/talk-to-us.md)」を参照してください。

### <a name="report-crashes-hangs-and-performance-issues"></a>クラッシュ、ハング、パフォーマンスの問題についての報告
 気になる点のちょっとしたメモでは済ませられない問題が発生するかもしれません。 ハング、クラッシュ、あるいはパフォーマンスに関する問題が発生した場合は、問題点、改善点の報告をした後に表示されるダイアログを使用することによって、簡単な操作でその再現手順、クラッシュ ダンプ、トレース ファイルをお送りいただくことが可能です。

 まずは、前述の手順に従って問題点、改善点の報告をお送りください。 その後にポップアップ表示されるダイアログで、フィードバックに既定のタグを付けるか、または独自のタグを作成してタグ付けすることができます。 タグを付けるなら、フィードバックを該当する機能のチームに転送する際に助けになります。 **[カテゴリの選択]** ドロップダウン リストで、報告する問題に該当するオプションを選択した後、問題を再現する手順に従ってください。 Visual Studio を使用してフィードバックを報告する方法についての詳細な手順も利用できます。 For more information, see [Visual Studio Send a Smile Instructions](https://msdn.microsoft.com/library/5cc9b67a-54d0-41b0-aa8f-80dff4475a6b).

## <a name="see-also"></a>参照

* [Apache Cordova を使ったクロスプラットフォーム アプリをビルドする](https://msdn.microsoft.com/library/34d3c1be-22b3-4812-97fb-10b4e8ad2134)
* [Visual Studio における Xamarin を使用したネイティブ UI を備えたアプリの作成](./cross-platform/build-apps-with-native-ui-using-xamarin-in-visual-studio.md)
* [Visual C++ を使ったクロスプラットフォーム モバイル アプリをビルドする](./misc/build-cross-platform-mobile-apps-with-visual-cpp.md)
* [IntelliTest でのコードの単体テストの生成](./test/generate-unit-tests-for-your-code-with-intellitest.md)
* [複数のユーザー アカウントを使って作業する](./ide/work-with-multiple-user-accounts.md)
* [カスタム ウィンドウ レイアウトを作成する](./misc/create-custom-window-layouts.md)
* [電球を使ってクイック操作をする](./ide/perform-quick-actions-with-light-bulbs.md)
* [Visual Studio 2017 の新機能](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)