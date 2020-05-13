---
title: クロス プラットフォームのモバイル開発
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 8202717a-e990-45cf-b092-438651ccb38a
caps.latest.revision: 66
ms.author: crdun
manager: crdun
ms.openlocfilehash: 1efc8ea7f40c3098e681cc80ac90789b629630a9
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301387"
---
# <a name="cross-platform-mobile-development-in-visual-studio"></a>Visual Studio におけるクロス プラットフォーム モバイル開発
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Android、iOS、および Windows デバイス用のアプリを Visual Studio を使用して作成することができます。  アプリを設計する過程で Visual Studio のツールを利用すると、Office 365、Azure App Services、Application Insights などの接続済みサービスを簡単に追加できます。

 アプリを作成するには、C# と .NET Framework、HTML と JavaScript、または C++ を使用します。 コード、文字列、イメージを共有できるほか、場合によってはユーザー インターフェイスも共有できます。

 ゲームまたは没入感のあるグラフィカル アプリを作成する場合は、Visual Studio Tools for Unity をインストールすれば、Visual Studio と Unity の強力な生産性機能をすべて活用できます。Unity は、iOS、Android、Windows、およびその他のプラットフォームで実行するアプリ用のクロスプラットフォームのゲーム/グラフィックス エンジンおよび開発環境として人気を博しています。

 **この記事では、次の手順を実行します。**

- [アンドロイド、iOS、および Windows 用のアプリをビルドする (.NET フレームワーク)](#NET)

  - [単一のコードベースからターゲットアンドロイド、iOS、およびWindows](../cross-platform/cross-platform-mobile-development-in-visual-studio.md#AndroidHTML)

  - [Windows 10 デバイスを対象にする](../cross-platform/cross-platform-mobile-development-in-visual-studio.md#WindowsHTML)

- [Android、iOS、および Windows 用のアプリをビルドする (HTML/JavaScript)](#HTML)

- [Android および Windows 用のアプリをビルドする (C++)](#CPP)

- [Android、iOS、および Windows 用のクロスプラットフォーム ゲームを Visual Studio Tools for Unity を使用してビルドする](#Unity)

## <a name="build-an-app-for-android-ios-and-windows-net-framework"></a><a name="NET"></a> Android、iOS、および Windows 用のアプリをビルドする (.NET Framework)
 ![デバイス](../cross-platform/media/homedevices.png "HomeDevices")

 Xamarin を利用すれば、コードや UI を共有し、同じソリューションで Android、iOS、Windows を対象にできます。

|**詳細情報**|
|--------------------|
|[Visual Studio のインストール](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[Visual Studio での Xamarin について学習する](https://visualstudio.microsoft.com/xamarin/) (VisualStudio.com)|
|[Visual Studio と Xamarin](../cross-platform/visual-studio-and-xamarin.md) (MSDN ライブラリ)|
|[Xamarin アプリを使用したアプリケーション ライフサイクル管理 (ALM)](../cross-platform/application-lifecycle-management-alm-with-xamarin-apps.md) (MSDN ライブラリ)|
|[Visual Studio でのユニバーサル Windows アプリについて学習する](https://www.visualstudio.com/vs/universal-windows-platform/) (VisualStudio.com)|
|[Swift と C# との間の類似点について学習する](https://aka.ms/scposter) (download.microsoft.com)|
|[Visual Studio Emulator for Android について学習する](https://visualstudio.microsoft.com/vs/msft-android-emulator/) (VisualStudio.com)|

### <a name="target-android-ios-and-windows-from-a-single-code-base"></a><a name="AndroidHTML"></a> 1 つのコード ベースから Android、iOS、Windows を対象にする
 C# または F# を使用することで (Visual Basic は現時点ではサポートされていません)、Android、iOS、Windows のネイティブ アプリを開発できます。  最初に Visual Studio 2015 をインストールし、インストーラーで **[カスタム]** オプションを選択し、[クロス プラットフォームのモバイル開発] の **[C#/.NET (Xamarin)]** ボックスを選択します。 [Xamarin インストーラー](https://www.xamarin.com/download)で開始することもできます。このインストーラーは Xamarin for Visual Studio 2013 のインストールに必須です。

 Visual Studio 2015 が既にインストールされている場合、**[コントロール パネル] の [プログラムと機能]** からインストーラーを実行し、上と同じように Xamarin に **[カスタム]** オプションを選択します。

 完了すると、[**新しい**プロジェクト] ダイアログ ボックスにプロジェクト テンプレートが表示されます。 Xamarin テンプレートを見つける最も簡単な方法は、"Xamarin" で検索することです。

 Xamarin は Android、iOS、Windows のネイティブ機能を .NET オブジェクトとして表示します。 そのため、アプリにはネイティブ API とネイティブ ユーザー コントロールのフル アクセスが与えられます。ネイティブ プラットフォーム言語で記述されたアプリと同様の応答性を持ちます。

 プロジェクトを作成した後は、生産性を高める Visual Studio の機能をすべて活用できます。 たとえば、デザイナーを使用してページを作成し、IntelliSense を使用してモバイル プラットフォームのネイティブ API を探索できます。 アプリケーションを実行して結果を確認する準備ができたら、Visual Studio Emulator for Android、または Android エミュレーターを使用したり、Windows アプリをネイティブ実行したり、Windows Phone エミュレーターで Windows アプリを実行したりできます。 テザリングされた Android デバイスや Windows デバイスを直接使用することもできます。 iOS プロジェクトでは、Mac のネットワークに接続し、Visual Studio から Mac エミュレーターを起動したり、テザリングされたデバイスに接続したりできます。

#### <a name="design-one-set-of-pages-that-render-across-all-devices-by-using-xamarinforms"></a>すべてのデバイス用にレンダリングするページを 1 セット、Xamarin.Forms を使用してデザインする
 アプリのデザインの複雑さによっては、プロジェクト テンプレートの [ *Mobile Apps* ] グループにある [ **Xamarin.Forms** ] テンプレートを使用して作成することを検討します。 Xamarin.Forms は、Android、iOS、Windows 間で共有できる単一のユーザー インターフェイスを作成する UI ツールキットです。  Xamarin.Forms ソリューションをコンパイルすると、Android アプリ、iOS アプリ、Windows アプリが生成されます。 詳細については、「[Xamarin によるモバイル開発の概要](../cross-platform/learn-about-mobile-development-with-xamarin.md)」を参照してください。

#### <a name="share-code-between-android-ios-and-windows-apps"></a><a name="ShareHTML"></a> Android、iOS、および Windows アプリ間でコードを共有する
 Xamarin.Forms を使用せず、プラットフォームごとに個別にデザインすることにした場合は、UI 以外のコードの大部分をプラットフォームのプロジェクト (Android、iOS、および Windows) 間で共有できます。 これには、ビジネス ロジック、クラウド統合、データベース アクセス、または .NET Framework を対象とするその他のコードが含まれます。 特定のプラットフォームを対象とするコードのみ、共有することができません。

 ![Windows、iOs、Android の UI でコードを共有](../cross-platform/media/sharecode.png "ShareCode")

 共有プロジェクト、ポータブル クラス ライブラリ プロジェクト、またはその両方を使用して、コードを共有できます。 共有プロジェクトに最適なコードもあれば、ポータブル クラス ライブラリ プロジェクトにより適したコードもあります。

|**詳細情報**|
|--------------------|
|共有プロジェクト、ポータブル クラス ライブラリ プロジェクト、またはその両方のいずれを使用してコードを共有するかを選択する。<br /><br /> [プラットフォーム間でコードを共有する](https://devblogs.microsoft.com/dotnet/sharing-code-across-platforms/) (.NET Framework ブログ)<br /><br /> [コード共有のオプション](/xamarin/cross-platform/app-fundamentals/code-sharing) (Xamarin)<br /><br /> [.NET Framework によるコード共有のオプション](https://msdn.microsoft.com/library/dn720832.aspx) (MSDN ライブラリ)|

### <a name="target-windows-10-devices"></a><a name="WindowsHTML"></a>ターゲットの Windows 10 デバイス
 ![デバイス](../cross-platform/media/windowsdevices.png "Windows デバイス")

 Windows 10 デバイスを幅広く対象とした単一のアプリを作成する必要がある場合は、ユニバーサル Windows アプリを作成します。 1 つのプロジェクトを使用してアプリをデザインすれば、どのデバイスを使用して表示してもアプリのページが正しくレンダリングされます。

 ユニバーサル Windows アプリのプロジェクト テンプレートから作業を開始します。 ページを視覚的にデザインした後、それらのページをプレビュー ウィンドウで開くと、さまざまな種類のデバイスでどのように表示されるかを確認できます。 デバイスに表示されるページが気に入らない場合は、画面サイズ、解像度、あるいは縦モードまたは横モードなどのさまざまな向きに合わせて、ページを最適化できます。 このような操作すべてを、Visual Studio の直感的なツール ウィンドウと簡単にアクセスできるメニュー オプションを使用して実行できます。 アプリを実行してコードをステップ実行する準備ができたら、さまざまな種類のデバイスのすべてのデバイス エミュレーターとシミュレーターが、**標準**ツール バーにある 1 つのドロップダウン リストにまとめて表示されます。

 Windows 10 はまだ新しいため、Windows 8.1 を対象にしたプロジェクト テンプレートも用意されています。 アプリを Windows 10 のスマートフォン、タブレット、および PC で実行する場合、必要であればこれらのプロジェクト テンプレートを使用できます。 ただし、Windows 8.1 を実行しているすべてのデバイスは Windows 10 への自動アップグレードが実行されるため、Windows 8.1 をターゲットにする特定の理由がない限り、Windows 10 を対象とするプロジェクト テンプレートを使用することをお勧めします。

|**詳細情報**|
|--------------------|
|[ユニバーサル Windows アプリについて学習する](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx) (Windows デベロッパー センター)|
|[初めてのアプリをビルドする](https://msdn.microsoft.com/library/windows/apps/dn609832.aspx) (Windows デベロッパー センター)|
|[ユニバーサル Windows プラットフォーム (UWP) 向けアプリの開発](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md)|
|[アプリを Universal Windows Platform (UWP) へ移行する](../misc/migrate-apps-to-the-universal-windows-platform-uwp.md)|

## <a name="build-an-app-for-android-ios-and-windows-htmljavascript"></a><a name="HTML"></a>アンドロイド、iOS、およびウィンドウ用のアプリを構築する (HTML/JavaScript)
 ![デバイス](../cross-platform/media/homedevices.png "HomeDevices")

 HTML と JavaScript に精通した Web 開発者は、Visual Studio Tools for Apache Cordova を使用して、Windows、Android、および iOS を対象とすることができます。 これらのアプリは 3 つのすべてのプラットフォームを対象にすることができ、開発者が最も慣れているスキルとプロセスを使用してアプリを作成できます。

 Apache Cordova は、プラグイン モデルを含むフレームワークです。 このプラグイン モデルは、3 つのすべてのプラットフォーム (Android、iOS、Windows) のネイティブ デバイス機能にアクセスするために使用できる単一の JavaScript API を提供します。

 これらの API はクロスプラットフォームであるため、記述するコードの大部分を 3 つのすべてのプラットフォーム間で共有できます。 このため、開発と保守のコストを削減できます。 また、ゼロから始める必要がありません。 他の種類の Web アプリケーションを既に作成してある場合は、Cordova アプリでそれらのファイルを共有できるため、修正や再設計の必要はありません。

 ![マルチ&#45;デバイス ハイブリッド アプリ](../cross-platform/media/multidevicehybridapps.png "マルチデバイスハイブリッドアプリ")

 作業を開始するには、Visual Studio 2015 をインストールして、セットアップ中に **HTML/JavaScript (Apache Cordova)** 機能を選択します。 Visual Studio 2013 を使用している場合は、Visual Studio Tools for Apache Cordova の拡張機能をインストールしてください。 いずれにしても、Cordova ツールにより、マルチプラットフォーム アプリをビルドするために必要なすべてのサード パーティのソフトウェアが自動的にインストールされます。

 拡張機能をインストールしたら、Visual Studio を開き、**空のアプリケーション (Apache Cordova)** プロジェクトを作成します。 その後、JavaScript または TypeScript を使用してアプリを開発できます。 また、プラグインを追加してアプリの機能を拡張することもでき、プラグインの API はコードを記述するときに IntelliSense に表示されます。

 アプリを実行してコードをデバッグする準備ができたら、エミュレーターとして、Apache Ripple エミュレーターや Visual Studio Emulator (Android または Windows Phone)、ブラウザー、またはコンピューターに直接接続したデバイスなどを選択します。 その後、アプリを起動します。 Windows PC でアプリを開発している場合は、この上さらにそのアプリを実行することもできます。 これらのオプションすべては、Visual Studio Tools for Apache Cordova の一部として Visual Studio に組み込まれます。

 ユニバーサル Windows アプリを作成するためのプロジェクト テンプレートは、Visual Studio でまだ使用できるので、Windows デバイスだけを対象にする場合は、自由に使用してください。 後で Android および iOS を対象にすることを決定した場合は、いつでも Cordova プロジェクトにコードを移植できます。 WinJS API のオープン ソース バージョンがあるため、それらの API を使用するすべてのコードを再利用することができます。 つまり、将来他のプラットフォームを対象にすることを決定した場合、Visual Studio Tools for Apache Cordova から始めることをお勧めします。

|**詳細情報**|
|--------------------|
|[Visual Studio のインストール](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[Visual Studio Tools for Apache Cordova の使用を開始する](/visualstudio/cross-platform/tools-for-cordova/?view=toolsforcordova-2017) (taco.visualstudio.com)|
|[Visual Studio Emulator for Android について学習する](https://visualstudio.microsoft.com/vs/msft-android-emulator/) (VisualStudio.com)|

## <a name="build-an-app-for-android-and-windows-c"></a><a name="CPP"></a>アンドロイドとウィンドウ用のアプリを構築する (C++)
 ![C&#43;&#43; を使用して Android、iOS、Windows 用に作成する](../cross-platform/media/cross-plat-cpp-intro-image.png "Cross_Plat_CPP_Intro_Image")

 最初に、Visual Studio 2015 と Visual C++ for Cross Platform Mobile Development ツールをインストールします。 その後、Android 用のネイティブ アクティビティ アプリケーションか、Windows を対象とするアプリを構築できます。 iOS を対象とする C++ テンプレートは、まだ利用できません。 必要であれば、同じソリューションで Android と Windows を対象にし、クロスプラットフォームの静的または動的な共有ライブラリを使用して両方でコードを共有することができます。

 ゲームなどの高度なグラフィックス操作を必要とする Android アプリをビルドする必要がある場合に、C++ を利用できます。 **[ネイティブ アクティビティ アプリケーション (Android)]** プロジェクトから開始できます。 このプロジェクトでは、C 言語のツール チェーンが完全にサポートされます。

 ![Native-Activity プロジェクトのテンプレート](../cross-platform/media/cross-plat-cpp-native.png "クロスPlat_CPP_Native")

 アプリケーションを実行して結果を確認する準備ができたら、Visual Studio Emulator for Android を使用できます。 高速で信頼性が高く、簡単にインストールして構成できます。

 C++ とユニバーサル Windows アプリ プロジェクト テンプレートを使用すると、幅広い Windows 10 デバイスを対象とするアプリケーションを作成することもできます。 この点については、このトピックで前に説明した「[Windows 10 デバイスを対象にする](#WindowsHTML)」セクションをお読みください。

 静的または動的な共有ライブラリを作成して、Android および Windows 間で C++ コードを共有することができます。

 ![静的および動的な共有ライブラリ](../cross-platform/media/cross-plat-cpp-libraries.png "Cross_Plat_CPP_Libraries")

 このセクションで既に説明したものと同様に、Windows または Android のプロジェクトでそのライブラリを使用することができます。 また、Xamarin、Java、またはアンマネージ DLL 内の関数を呼び出すことのできる任意の言語を使用してビルドするアプリで、そのライブラリを利用できます。

 これらのライブラリでコードを記述するときは、IntelliSense を使用して Android プラットフォームと Windows プラットフォームのネイティブ API を探索できます。 これらのライブラリ プロジェクトは Visual Studio デバッガーと完全に統合されるため、デバッガーの高度な機能をすべて活用して、ブレークポイントの設定、コードのステップ実行、問題点の検索と修正を行うことができます。

|**詳細情報**|
|--------------------|
|[ビジュアル スタジオをダウンロードします。](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[Visual C++ for Cross-Platform Mobile Development ツールのインストール](https://msdn.microsoft.com/library/dn872463\(v=vs.140\).aspx) (MSDN ライブラリ)|
|[C++ を使用して複数のプラットフォームを対象とすることについて学習する](https://www.visualstudio.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[必要なものをインストールしてから、Android 用のネイティブ アクティビティ アプリケーションを作成する](https://msdn.microsoft.com/library/dn872463\(v=vs.140\).aspx) (MSDN ライブラリ)|
|[Visual Studio Emulator for Android について学習する](https://visualstudio.microsoft.com/vs/msft-android-emulator/) (VisualStudio.com)|
|[Android と Windows アプリでの C++ コードの共有について学習する](https://visualstudio.microsoft.com/vs/features/cplusplus-mdd/) (VisualStudio.com)|
|[C++ のクロス プラットフォーム モバイル開発の例](https://msdn.microsoft.com/library/dn707596.aspx) (MSDN ライブラリ)|
|[C++ のクロス プラットフォーム モバイル開発のその他の例](https://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=android&f%5B1%5D.Type=ProgrammingLanguage&f%5B1%5D.Value=C%2B%2B&f%5B1%5D.Text=C%2B%2B) (code.msdn)|

## <a name="build-a-cross-platform-game-for-android-ios-and-windows-by-using-visual-studio-tools-for-unity"></a><a name="Unity"></a>Unity 用の Visual Studio ツールを使用して、Android、iOS、および Windows 用のクロスプラットフォーム ゲームをビルドする
 Visual Studio ツール for Unity は、Visual Studio の強力なコード編集、生産性、デバッグ ツールを*Unity*、Windows、iOS、Android、および Web を含む他のプラットフォームを対象とする没入型アプリ向けの人気クロスプラットフォーム ゲーム/グラフィックス エンジンおよび開発環境を統合する Visual Studio 用の無料の拡張機能です。

 ![VSTU 開発環境](../cross-platform/media/vstu-overview.png "VSTU_Overview")

 Visual Studio tools Unity (VSTU) を利用すると、Visual Studio を使用して C# でゲームとエディター スクリプトを記述した後、強力なデバッガーを使用してエラーを検出して修正できます。 VSTU の最新リリースでは、Unity 5 のサポートが提供され、Unity の ShaderLab シェーダー言語の構文の色分け、Unity との同期機能の向上、デバッグの機能向上、および、MonoBehavior ウィザードによるコード生成の機能強化などがなされました。 また、VSTU により、Unity のプロジェクト ファイル、コンソール メッセージ、およびゲームを開始する機能が Visual Studio に統合されるため、コードの記述中に Unity エディターとの間で切り替える手間を少なくできます。

 Unity と Visual Studio Tools for Unity を使用したゲームの構築を、今すぐに開始できます。

|**詳細情報**|
|--------------------|
|[Visual Studio での Unity ゲーム構築について学習する](https://www.visualstudio.com/features/unitytools-vs.aspx)|
|[Visual Studio Tools for Unity の詳細について](../cross-platform/visual-studio-tools-for-unity.md) (MSDN ライブラリ)|
|[Visual Studio Tools for Unity の使用を開始する](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md) (MSDN ライブラリ)|
|[Visual Studio Tools for Unity 2.0 Preview の最新の拡張機能について学習する](https://devblogs.microsoft.com/visualstudio/visual-studio-tools-for-unity-2-0-preview/) (Visual Studio ブログ)|
|[Visual Studio Tools for Unity 2.0 Preview の紹介ビデオを見る](https://www.bing.com/videos/search?q=visual+studio+tools+for+unity&qs=n&form=QBVLPG&pq=visual+studio+tools+for+unity&sc=6-29&sp=-1&sk=#view=detail&mid=0A13177F0BC7463A24080A13177F0BC7463A2408) (ビデオ)|
|[Unity について学習する](https://unity.com/) (Unity Web サイト)|

## <a name="see-also"></a>参照

- [Office 365 API を Visual Studio プロジェクトに追加する](https://msdn.microsoft.com/library/office/dn605899\(v=office.15\).aspx)
- [Azure Mobile Services](https://msdn.microsoft.com/library/dn720832\(v=vs.110\).aspx)
- [Application Insights](/azure/application-insights/app-insights-overview)
