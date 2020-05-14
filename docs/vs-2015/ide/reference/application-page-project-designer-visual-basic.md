---
title: '[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesApplicationWPF
- vb.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
ms.assetid: 8cec9fea-cd92-47ff-88dd-7c928f0b4a74
caps.latest.revision: 68
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 893647303b493ea633caf076658edbdcf0664ccc
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850838"
---
# <a name="application-page-project-designer-visual-basic"></a>Application Page, Project Designer (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクト デザイナーの **[アプリケーション]** ページを使用して、プロジェクトのアプリケーション設定とプロパティを指定します。

 **[アプリケーション]** ページにアクセスするには、**ソリューション エクスプローラー**のプロジェクト ノード ( **[ソリューション]** ノードではありません) を選択します。 その後、メニュー バーで **[プロジェクト]** 、 **[プロパティ]** の順に選択します。 プロジェクト デザイナーが表示されたら、 **[アプリケーション]** タブをクリックします。

 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

## <a name="general-application-settings"></a>アプリケーションの全般設定
 次のオプションでは、アプリケーションの全般設定を構成できます。

 **アセンブリ名**アセンブリマニフェストを格納する出力ファイルの名前を指定します。 このプロパティを変更すると、 **[出力名]** プロパティも変更されます。 コマンド プロンプトで [/out (Visual Basic)](https://msdn.microsoft.com/library/9f148c15-0909-4cb8-a2db-777f8a8b45ae) を使用して変更することもできます。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.AssemblyName%2A>」を参照してください。

 **ルート名前空間**プロジェクト内のすべてのファイルの基本名前空間を指定します。 たとえば、 **[ルート名前空間]** を `Project1` に設定し、コード内のいずれの名前空間にも存在しない `Class1` がある場合、その名前空間は `Project1.Class1` になります。 また、コード内の名前空間 `Order` に `Class2` がある場合、その名前空間は `Project1.Order.Class2` になります。

 **[ルート名前空間]** をクリアした場合は、コードにプロジェクトの名前空間の構造を指定できます。

> [!NOTE]
> [Namespace ステートメント](https://msdn.microsoft.com/library/a31fbd95-9ace-4c3d-bbb1-51222a2272b2)で Global グローバル キーワードを使用する場合は、プロジェクトのルート名前空間以外の名前空間を定義できます。 **[ルート名前空間]** をクリアすると、`Global` は最上位レベルの名前空間になり、`Namespace` ステートメントの `Global` キーワードは不要になります。 詳細については、「[Visual Basic における名前空間](https://msdn.microsoft.com/library/cffac744-ab8c-4f1f-ba50-732c22ab4b88)」の「名前空間のステートメントでの Global キーワード」を参照してください。

 コードで名前空間を作成する方法については、「[Namespace ステートメント](https://msdn.microsoft.com/library/a31fbd95-9ace-4c3d-bbb1-51222a2272b2)」を参照してください。

 ルート名前空間プロパティの詳細については、「[/rootnamespace](https://msdn.microsoft.com/library/e9245edf-6bef-420d-a7c7-324117752783)」を参照してください。

 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.RootNamespace%2A>」を参照してください。

 **ターゲットフレームワーク (すべての構成)** アプリケーションが対象とする .NET Framework のバージョンを指定します。 このオプションの値は、コンピューター上にインストールされている .NET Framework のバージョンによって異なる場合があります。

 既定値は、 **[新しいプロジェクト]** ダイアログ ボックスで指定したターゲット フレームワークと一致します。

> [!NOTE]
> [[必須コンポーネント] ダイアログ ボックス](../../ide/reference/prerequisites-dialog-box.md)にリストされている必須コンポーネントのパッケージは、ダイアログ ボックスを初めて開いたときに自動的に設定されます。 その後、プロジェクトのターゲット フレームワークを変更した場合は、新しいターゲット フレームワークに合わせて必須コンポーネントを手動で指定する必要があります。

 詳細については、[ .NET Framework のバージョンをターゲットにする](../../ide/how-to-target-a-version-of-the-dotnet-framework.md)」と「[Visual Studio のマルチ ターゲットの概要](../../ide/visual-studio-multi-targeting-overview.md)」を参照してください。

 **アプリケーションの種類** ビルドするアプリケーションの種類を指定します。 [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] アプリの場合は、 **[Windows ストア アプリ]** 、 **[クラス ライブラリ]** 、または **[WinMD ファイル]** を指定できます。 他のほとんどのアプリケーションの種類では、 **[Windows アプリケーション]** 、 **[コンソール アプリケーション]** 、 **[クラス ライブラリ]** 、 **[Windows サービス]** 、または **[Web コントロール ライブラリ]** を指定できます。

 Web アプリケーション プロジェクトでは、 **[クラス ライブラリ]** を指定する必要があります。

 **[WinMD ファイル]** オプションを指定した場合、種類を Windows ランタイムのプログラミング言語に射影できます。 WinMD ファイルとしてプロジェクトの出力をパッケージ化することで、複数の言語でアプリケーションをコード化し、すべて同じ言語で記述した場合と同様に、コードを相互運用することができます。 [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] アプリを含む、Windows ランタイム ライブラリをターゲットとするソリューションに対して、 **[WinMD ファイル]** オプションを使用できます。 詳細については、「[C# および Visual Basic での Windows ランタイム コンポーネントの作成](https://msdn.microsoft.com/library/windows/apps/br230301(v=VS.85).aspx)」を参照してください。

> [!NOTE]
> Windows ランタイムでは、どの言語で使用される場合でも、ネイティブ オブジェクトとして表示されるように種類を射影できます。 たとえば、Windows ランタイムと対話する JavaScript アプリケーションでは JavaScript オブジェクト セットとして使用され、C# アプリケーションでは .NET オブジェクト コレクションとしてライブラリが使用されます。 WinMD ファイルとしてプロジェクトの出力をパッケージ化することで、Windows ランタイムで使用されるのと同じテクノロジを利用できます。

 **[アプリケーションの種類]** プロパティの詳細については、「[/target (Visual Basic)](https://msdn.microsoft.com/library/e0954147-548b-461f-9c4b-a8f88845616c)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.OutputType%2A>」を参照してください。

 **アイコン** プログラム アイコンとして使用する .ico ファイルを設定します。 **[\<参照...>]** を選択して、既存のグラフィックを参照します。 詳細については、「[/win32icon](https://msdn.microsoft.com/library/aecaab01-9353-46c5-941c-6edabd4eff92)」 (または「[/win32icon (C# コンパイラ オプション)](https://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138)」) を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>」を参照してください。

 スタートアップ**フォーム/スタートアップオブジェクト/スタートアップ URI**アプリケーションのスタートアップフォームまたはエントリポイントを指定します。

 **[アプリケーション フレームワークを有効にする]** が選択されている場合 (既定)、この一覧のタイトルは **[スタートアップ フォーム]** となり、フォームのみが表示されます。これは、アプリケーション フレームワークでは、オブジェクトではなく、スタートアップ フォームのみがサポートされるためです。

 プロジェクトが WPF ブラウザー アプリケーションの場合、この一覧のタイトルは **[スタートアップ URI]** となり、既定値は **Page1.xaml** となります。 **[スタートアップ URI]** 一覧では、アプリケーションの起動時に表示されるユーザー インターフェイス リソース (XAML 要素) を指定できます。 詳細については、「<xref:System.Windows.Application.StartupUri%2A>」を参照してください。

 **[アプリケーション フレームワークを有効にする]** の選択を解除すると、この一覧は **[スタートアップ オブジェクト]** になり、フォームと、`Sub Main` を含むクラスまたはモジュールの両方が表示されます。

 **[スタートアップ オブジェクト]** では、アプリケーションの読み込み時に呼び出されるようにエントリ ポイントを定義します。 通常、これは、アプリケーションのメイン フォーム、またはアプリケーションの起動時に実行する必要がある `Sub Main` プロシージャに設定されます。 クラス ライブラリにはエントリ ポイントがないため、このプロパティのオプションのみが **[(なし)]** になります。 詳細については、「[/main](https://msdn.microsoft.com/library/83fc339d-6652-415d-b205-b5133319b5b0)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.StartupObject%2A>」を参照してください。

 **アセンブリ情報**このボタンをクリックすると、[[アセンブリ情報] ダイアログボックス](../../ide/reference/assembly-information-dialog-box.md)が表示されます。

 **アプリケーションフレームワークを有効にする**プロジェクトがアプリケーションフレームワークを使用するかどうかを指定します。 このオプションの設定は、 **[スタートアップ フォーム]** / **[スタートアップ オブジェクト]** で使用できるオプションに影響します。

 このチェック ボックスがオンになっている場合、アプリケーションでは標準の `Sub Main` が使用されます。 このチェック ボックスをオンにすると、 **[Windows アプリケーション フレームワーク プロパティ]** セクションの機能が有効になります。その場合、スタートアップ フォームを選択する必要もあります。

 このチェック ボックスをオフにすると、アプリケーションでは、 **[スタートアップ フォーム]** で指定したカスタムの `Sub Main` が使用されます。 この場合、スタートアップ オブジェクト (メソッドまたはクラスのカスタム `Sub Main`) またはフォームを指定できます。 また、 **[Windows アプリケーション フレームワーク プロパティ]** セクションのオプションが使用できなくなります。

 **Windows の設定を表示**するこのボタンをクリックすると、アプリケーションマニフェストファイルが生成されて開きます。 Visual Studio ではこのファイルを使用して、アプリケーションのマニフェスト データを生成します。 その後、次のように、app.manifest の `<requestedExecutionLevel>` タグを変更し、UAC 要求実行レベルを設定します。

 `<requestedExecutionLevel level="asInvoker" />`

 ClickOnce は `asInvoker` のレベル、または仮想化モードで機能します (マニフェストは生成されません)。 仮想化モードを指定するには、app.manifest からタグ全体を削除します。

 マニフェストの生成の詳細については、「[Windows Vista の ClickOnce 配置](../../deployment/clickonce-deployment-on-windows-vista.md)」を参照してください。

## <a name="windows-application-framework-properties"></a>Windows アプリケーション フレームワーク プロパティ
 次の設定は、 **[Windows アプリケーション フレームワーク プロパティ]** セクションで使用できます。 これらのオプションは、 **[アプリケーション フレームワークを有効にする]** チェック ボックスがオンになっている場合にのみ使用できます。 この後に続くセクションでは、Windows Presentation Foundation (WPF) アプリケーションの **Windows アプリケーション フレームワーク プロパティ**の設定について説明します。

 **XP visual スタイルを有効にする**Windows xp の視覚スタイルを有効または無効にします ( *WINDOWS xp のテーマ*とも呼ばれます)。 Windows XP Visual スタイルを有効にすると、角が丸いコントロールや色が動的に切り替わるコントロールなどを使用できます。 既定ではオンです。 Windows XP Visual スタイルの詳細については、「[Windows XP の機能と Windows フォーム コントロール](https://msdn.microsoft.com/bc7fab94-fce9-4bf1-a8ad-a5837c91c3c0)」を参照してください。

 **単一インスタンスアプリケーションを作成**するユーザーがアプリケーションの複数のインスタンスを実行できないようにするには、このチェックボックスをオンにします。 既定では、このチェック ボックスはオフになっています。 この設定により、アプリケーションの複数のインスタンスを実行できるようになります。

 **シャットダウン時に設定を保存**するユーザーがコンピューターをシャットダウンしたときに、アプリケーションの `My.Settings` 設定を保存するように指定するには、このチェックボックスをオンにします。 この設定は既定で有効になります。 このオプションが無効になっている場合は、`My.Settings.Save` を呼び出して、アプリケーション設定を手動で保存できます。

 **認証モード**Windows 認証を使用して、現在ログオンしているユーザーを識別するには、 **[windows]** (既定値) を選択します。 `My.User` オブジェクトを使用すれば、実行時にこの情報を取得することができます。 既定の Windows 認証方法を使用せずに、独自のコードを指定してユーザーを認証する場合は、 **[アプリケーション定義]** を選択します。

 **シャットダウンモード**他のフォームが開いている場合でも、スタートアップフォームとして設定されたフォームを閉じるときにアプリケーションが終了するように指定するには、 **[スタートアップフォームを閉じるとき]** を選択します (既定)。 最後のフォームが閉じられたとき、または `My.Application.Exit` や `End` ステートメントが明示的に呼び出されたときにアプリケーションを終了するように指定する場合は、 **[最後のフォームが閉じるとき]** を選択します。

 `Shutdown` を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、 **[明示的にシャットダウンするとき]** を選択します。

 最後のウィンドウが閉じられたとき、または `Shutdown` を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、 **[最後のウィンドウを閉じるとき]** を選択します。 これは、既定の設定です。

 メイン ウィンドウが閉じられたとき、または `Shutdown` を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、 **[メイン ウィンドウを閉じるとき]** を選択します。

 **スプラッシュスクリーン**スプラッシュスクリーンとして使用するフォームを選択します。 フォームまたはテンプレートを使用して、事前にスプラッシュ スクリーンを作成しておく必要があります。 既定値は **[(なし)]** です。

 **アプリケーションイベントの表示**このボタンをクリックすると、イベントコードファイルが表示されます。このコードファイルには、`Startup`、`Shutdown`、`UnhandledException`、`StartupNextInstance` および `NetworkAvailabilityChanged`のアプリケーションフレームワークイベントのイベントを記述できます。 また、特定のアプリケーション フレームワーク メソッドをオーバーライドすることもできます。 たとえば、`OnInitialize` をオーバーライドして、スプラッシュ スクリーンの表示動作を変更することができます。

### <a name="windows-application-framework-properties-for-windows-presentation-foundation-wpf-applications"></a>Windows Presentation Foundation (WPF) アプリケーションの Windows アプリケーション フレームワーク プロパティ
 プロジェクトが Windows Presentation Foundation アプリケーションである場合は、**Windows アプリケーション フレームワーク プロパティ**で以下の設定を使用できます。 これらのオプションは、 **[アプリケーション フレームワークを有効にする]** チェック ボックスがオンになっている場合にのみ使用できます。 次の表にリストされているオプションは、WPF アプリケーションまたは WPF ブラウザー アプリケーションのみで使用できます。 WPF ユーザー コントロールやカスタム コントロール ライブラリでは使用できません。

 **シャットダウンモード**このプロパティは Windows Presentation Foundation アプリケーションにのみ適用されます。

 <xref:System.Windows.Application.Shutdown%2A> を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、 **[明示的にシャットダウンするとき]** を選択します。

 最後のウィンドウが閉じられたとき、または <xref:System.Windows.Application.Shutdown%2A> を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、 **[最後のウィンドウを閉じるとき]** を選択します。 これは、既定の設定です。

 メイン ウィンドウが閉じられたとき、または <xref:System.Windows.Application.Shutdown%2A> を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、 **[メイン ウィンドウを閉じるとき]** を選択します。

 この設定の使用方法の詳細については、「<xref:System.Windows.Application.Shutdown%2A>」を参照してください。

 **XAML の編集**このボタンをクリックすると、XAML エディターのアプリケーション定義ファイル (app.xaml) が開き、変更されます。 このボタンをクリックすると、アプリケーション定義ノードに Application.xaml が開きます。 リソースの定義などの特定のタスクを実行するには、このファイルを編集する必要があります。 アプリケーション定義ファイルが存在しない場合、プロジェクト デザイナーで作成されます。

 **アプリケーションイベントの表示**このボタンをクリックすると `Application` 部分クラスファイル (app.xaml) がコードエディターに表示されます。 ファイルが存在しない場合、プロジェクト デザイナーで、適切なクラス名と名前空間を使用して作成されます。

 特定のアプリケーション状態が変化すると (アプリケーション スタートアップやシャットダウンなどで)、<xref:System.Windows.Application> オブジェクトでイベントが発生します。 このクラスで公開されるイベントの完全な一覧については、「<xref:System.Windows.Application>」を参照してください。 これらのイベントは、`Application` 部分クラスのユーザー コード セクションで処理されます。

## <a name="see-also"></a>関連項目
[アプリケーションプロパティの管理](../../ide/application-properties.md) [Office ソリューションのコードの記述](https://msdn.microsoft.com/library/2d4d8fd0-e881-4829-976f-0d1a9221dec0)
