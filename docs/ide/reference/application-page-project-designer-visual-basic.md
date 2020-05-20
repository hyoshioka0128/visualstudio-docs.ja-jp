---
title: VB プロジェクトのプロパティの [アプリケーション] ページ
ms.date: 10/30/2018
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesApplicationWPF
- vb.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fe303f86b282e7e803dacc1dd8f4d3c1d6b72121
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595814"
---
# <a name="application-page-project-designer-visual-basic"></a>Application Page, Project Designer (Visual Basic)

プロジェクト デザイナーの **[アプリケーション]** ページを使用して、プロジェクトのアプリケーション設定とプロパティを指定します。

**[アプリケーション]** ページにアクセスするには、**ソリューション エクスプローラー**のプロジェクト ノード (**[ソリューション]** ノードではありません) を選択します。 その後、メニュー バーで **[プロジェクト]**  >  **[プロパティ]** を選択します。 **プロジェクト デザイナー**が表示されたら、 **[アプリケーション]** タブを選択します。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="general-application-settings"></a>アプリケーションの全般設定

次のオプションでは、アプリケーションの全般設定を構成できます。

### <a name="assembly-name"></a>アセンブリ名

アセンブリ マニフェストが含まれる出力ファイルの名前を指定します。 このプロパティを変更すると、 **[出力名]** プロパティも変更されます。

[/out (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/out)コンパイラ スイッチを使用して、コマンド プロンプトから出力ファイルの名前を指定することもできます。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.AssemblyName%2A>」を参照してください。

### <a name="root-namespace"></a>ルート名前空間

プロジェクト内のすべてのファイルで使用する基本の名前空間を指定します。 たとえば、 **[ルート名前空間]** を `Project1` に設定し、コード内のいずれの名前空間にも存在しない `Class1` がある場合、その名前空間は `Project1.Class1` になります。 また、コード内の名前空間 `Order` に `Class2` がある場合、その名前空間は `Project1.Order.Class2` になります。

**[ルート名前空間]** をクリアした場合は、コードにプロジェクトの名前空間の構造を指定できます。

> [!NOTE]
> [Namespace ステートメント](/dotnet/visual-basic/language-reference/statements/namespace-statement)で `Global` キーワードを使用する場合は、プロジェクトのルート名前空間以外の名前空間を定義できます。 **[ルート名前空間]** をクリアすると、`Global` は最上位レベルの名前空間になり、`Namespace` ステートメントの `Global` キーワードは不要になります。 詳細については、「[Visual Basic における名前空間](/dotnet/visual-basic/programming-guide/program-structure/namespaces)」の「名前空間のステートメントでの Global キーワード」を参照してください。

コードで名前空間を作成する方法については、「[Namespace ステートメント](/dotnet/visual-basic/language-reference/statements/namespace-statement)」を参照してください。

ルート名前空間プロパティの詳細については、「[/rootnamespace](/dotnet/visual-basic/reference/command-line-compiler/rootnamespace)」を参照してください。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.RootNamespace%2A>」を参照してください。

### <a name="target-framework-all-configurations"></a>ターゲット フレームワーク (すべての構成)

アプリケーションが対象とする .NET のバージョンを指定します。 このオプションの値は、コンピューター上にインストールされている .NET のバージョンによって異なる場合があります。

.NET Framework プロジェクトの場合、既定値は、プロジェクトを作成するときに指定したターゲット フレームワークと一致します。

> [!NOTE]
> [[必須コンポーネント] ダイアログ ボックス](../../ide/reference/prerequisites-dialog-box.md)にリストされている必須コンポーネントのパッケージは、ダイアログ ボックスを初めて開いたときに自動的に設定されます。 その後、プロジェクトのターゲット フレームワークを変更した場合は、新しいターゲット フレームワークに合わせて必須コンポーネントを手動で指定する必要があります。

詳細については、[フレームワークのターゲット設定](../../ide/visual-studio-multi-targeting-overview.md)に関するページを参照してください。

### <a name="application-type"></a>アプリケーションの種類

ビルドするアプリケーションの種類を指定します。 値は、プロジェクトの種類によって異なります。 たとえば、**Windows フォーム アプリ** プロジェクトの場合は、 **[Windows フォーム アプリケーション]** 、 **[クラス ライブラリ]** 、 **[コンソール アプリケーション]** 、 **[Windows サービス]** 、または **[Web コントロール ライブラリ]** を指定できます。

Web アプリケーション プロジェクトでは、 **[クラス ライブラリ]** を指定する必要があります。

**[アプリケーションの種類]** プロパティの詳細については、「[/target (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/target)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.OutputType%2A>」を参照してください。

### <a name="auto-generate-binding-redirects"></a>バインド リダイレクトの自動生成

アプリまたはそのコンポーネントで同じアセンブリの複数のバージョンが参照されている場合、バインド リダイレクトがプロジェクトに追加されます。 プロジェクト ファイルにおいて手動でバインド リダイレクトを定義したい場合は、 **[バインド リダイレクトの自動生成]** をオフにします。

リダイレクトの詳細については、「[アセンブリ バージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions)」をご覧ください。

### <a name="startup-form--startup-object--startup-uri"></a>スタートアップ フォーム / スタートアップ オブジェクト / スタートアップ URI

アプリケーションのスタートアップ フォームまたはエントリ ポイントを指定します。

**[アプリケーション フレームワークを有効にする]** が選択されている場合 (既定)、この一覧のタイトルは **[スタートアップ フォーム]** となり、フォームのみが表示されます。これは、アプリケーション フレームワークでは、オブジェクトではなく、スタートアップ フォームのみがサポートされるためです。

プロジェクトが WPF ブラウザー アプリケーションの場合、この一覧のタイトルは **[スタートアップ URI]** となり、既定値は **Page1.xaml** となります。 **[スタートアップ URI]** 一覧では、アプリケーションの起動時に表示されるユーザー インターフェイス リソース (XAML 要素) を指定できます。 詳細については、「<xref:System.Windows.Application.StartupUri%2A>」を参照してください。

**[アプリケーション フレームワークを有効にする]** の選択を解除すると、この一覧は **[スタートアップ オブジェクト]** になり、フォームと、`Sub Main` を含むクラスまたはモジュールの両方が表示されます。

**[スタートアップ オブジェクト]** では、アプリケーションの読み込み時に呼び出されるようにエントリ ポイントを定義します。 通常、これは、アプリケーションのメイン フォーム、またはアプリケーションの起動時に実行する必要がある `Sub Main` プロシージャに設定されます。 クラス ライブラリにはエントリ ポイントがないため、このプロパティのオプションのみが **[(なし)]** になります。 詳細については、「[/main](/dotnet/visual-basic/reference/command-line-compiler/main)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.StartupObject%2A>」を参照してください。

### <a name="icon"></a>アイコン

プログラム アイコンとして使用する .ico ファイルを設定します。 **[\<参照...>]** を選択して、既存のグラフィックを参照します。 詳細については、「[/win32icon](/dotnet/visual-basic/reference/command-line-compiler/win32icon)」 (または「[/win32icon (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)」) を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>」を参照してください。

### <a name="assembly-information"></a>アセンブリ情報

このボタンをクリックすると、[[アセンブリ情報] ダイアログ ボックス](../../ide/reference/assembly-information-dialog-box.md)が表示されます。

### <a name="enable-application-framework"></a>アプリケーション フレームワークを有効にする

プロジェクトでアプリケーション フレームワークを使用するかどうかを指定します。 このオプションの設定は、 **[スタートアップ フォーム]** / **[スタートアップ オブジェクト]** で使用できるオプションに影響します。

このチェック ボックスがオンになっている場合、アプリケーションでは標準の `Sub Main` が使用されます。 このチェック ボックスをオンにすると、 **[Windows アプリケーション フレームワーク プロパティ]** セクションの機能が有効になります。その場合、スタートアップ フォームを選択する必要もあります。

このチェック ボックスをオフにすると、アプリケーションでは、**[スタートアップ フォーム]** で指定したカスタムの `Sub Main` が使用されます。 この場合、スタートアップ オブジェクト (メソッドまたはクラスのカスタム `Sub Main`) またはフォームを指定できます。 また、 **[Windows アプリケーション フレームワーク プロパティ]** セクションのオプションが使用できなくなります。

### <a name="view-windows-settings"></a>Windows 設定の表示

このボタンをクリックすると、*app.manifest* ファイルが生成されて開かれます。 Visual Studio ではこのファイルを使用して、アプリケーションのマニフェスト データを生成します。 その後、次のように、*app.manifest* の `<requestedExecutionLevel>` タグを変更し、UAC 要求実行レベルを設定します。

`<requestedExecutionLevel level="asInvoker" />`

ClickOnce は `asInvoker` のレベル、または仮想化モードで機能します (マニフェストは生成されません)。 仮想化モードを指定するには、app.manifest からタグ全体を削除します。

マニフェストの生成の詳細については、「[Windows Vista の ClickOnce 配置](../../deployment/clickonce-deployment-on-windows-vista.md)」を参照してください。

## <a name="windows-application-framework-properties"></a>Windows アプリケーション フレームワーク プロパティ

次の設定は、 **[Windows アプリケーション フレームワーク プロパティ]** セクションで使用できます。 これらのオプションは、 **[アプリケーション フレームワークを有効にする]** チェック ボックスがオンになっている場合にのみ使用できます。

> [!TIP]
> この後に続くセクションでは、Windows Presentation Foundation (WPF) アプリに固有の **Windows アプリケーション フレームワーク プロパティ**の設定について説明します。

### <a name="enable-xp-visual-styles"></a>XP Visual スタイルを有効にする

Windows XP Visual スタイル (*Windows XP テーマ*ともいう) を有効または無効にします。 Windows XP Visual スタイルを有効にすると、角が丸いコントロールや色が動的に切り替わるコントロールなどを使用できます。 既定値は有効です。

### <a name="make-single-instance-application"></a>単一インスタンスのアプリケーションを作成する

このチェック ボックスをオンにすると、ユーザーはアプリケーションの複数のインスタンスを実行できなくなります。 このチェック ボックスの既定の設定は*オフ*であり、これにより、アプリケーションの複数のインスタンスを実行できます。 詳細については、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> イベントを参照してください。

### <a name="save-mysettings-on-shutdown"></a>シャットダウン時に My.Settings を保存する

ユーザーがコンピューターをシャットダウンしたときにアプリケーションの `My.Settings` 設定が保存されるように指定する場合は、このチェック ボックスをオンにします。 この設定は既定で有効になります。 このオプションが無効になっている場合は、`My.Settings.Save` を呼び出して、アプリケーション設定を手動で保存できます。

### <a name="authentication-mode"></a>認証モード

現在ログオンしているユーザーを識別するために Windows 認証を使用するように指定する場合は、 **[Windows]** (既定) を選択します。 `My.User` オブジェクトを使用すれば、実行時にこの情報を取得することができます。 既定の Windows 認証方法を使用せずに、独自のコードを指定してユーザーを認証する場合は、 **[アプリケーション定義]** を選択します。

### <a name="shutdown-mode"></a>シャットダウン モード

他のフォームが開いている場合でも、スタートアップ フォームとして設定されているフォームが閉じられたときにアプリケーションを終了するように指定する場合は、 **[スタートアップ フォームが閉じるとき]** (既定) を選択します。 最後のフォームが閉じられたとき、または `My.Application.Exit` や `End` ステートメントが明示的に呼び出されたときにアプリケーションを終了するように指定する場合は、**[最後のフォームが閉じるとき]** を選択します。

`Shutdown` を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、**[明示的にシャットダウンするとき]** を選択します。

最後のウィンドウが閉じられたとき、または `Shutdown` を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、**[最後のウィンドウを閉じるとき]** を選択します。 これが既定の設定です。

メイン ウィンドウが閉じられたとき、または `Shutdown` を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、**[メイン ウィンドウを閉じるとき]** を選択します。

### <a name="splash-screen"></a>スプラッシュ スクリーン

スプラッシュ スクリーンとして使用するフォームを選択します。 フォームまたはテンプレートを使用して、事前にスプラッシュ スクリーンを作成しておく必要があります。 既定値は **[(なし)]** です。

### <a name="view-application-events"></a>アプリケーション イベントの表示

このボタンをクリックすると、イベント コード ファイルが表示され、アプリケーション フレームワーク イベント (`Startup`、`Shutdown`、`UnhandledException`、`StartupNextInstance` および `NetworkAvailabilityChanged`) に対してイベントを記述できます。 また、特定のアプリケーション フレームワーク メソッドをオーバーライドすることもできます。 たとえば、`OnInitialize` をオーバーライドして、スプラッシュ スクリーンの表示動作を変更することができます。

## <a name="windows-application-framework-properties-for-windows-presentation-foundation-wpf-apps"></a>Windows Presentation Foundation (WPF) アプリの Windows アプリ フレームワーク プロパティ

プロジェクトが Windows Presentation Foundation (WPF) アプリである場合は、**Windows アプリケーション フレームワーク プロパティ**で以下の設定を使用できます。 これらのオプションは、 **[アプリケーション フレームワークを有効にする]** チェック ボックスがオンになっている場合にのみ使用できます。 次の表にリストされているオプションは、WPF または WPF ブラウザー アプリケーションのみで使用できます。 WPF ユーザー コントロールやカスタム コントロール ライブラリでは使用できません。

### <a name="shutdown-mode"></a>シャットダウン モード

このプロパティは、Windows Presentation Foundation (WPF) アプリケーションにのみ適用されます。

<xref:System.Windows.Application.Shutdown%2A> を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、**[明示的にシャットダウンするとき]** を選択します。

最後のウィンドウが閉じられたとき、または <xref:System.Windows.Application.Shutdown%2A> を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、**[最後のウィンドウを閉じるとき]** を選択します。 これが既定の設定です。

メイン ウィンドウが閉じられたとき、または <xref:System.Windows.Application.Shutdown%2A> を明示的に呼び出したときにアプリケーションが終了するように指定する場合は、**[メイン ウィンドウを閉じるとき]** を選択します。

この設定の使用方法の詳細については、「<xref:System.Windows.Application.Shutdown%2A>」を参照してください。

### <a name="edit-xaml"></a>XAML の編集

このボタンをクリックすると、XAML エディターでアプリケーション定義ファイル (Application.xaml) が開きます。 このボタンをクリックすると、*Application.xaml* のアプリケーション定義ノードが開きます。 リソースの定義などの特定のタスクを実行するには、このファイルを編集する必要があります。 アプリケーション定義ファイルが存在しない場合、プロジェクト デザイナーで作成されます。

### <a name="view-application-events"></a>アプリケーション イベントの表示

このボタンをクリックすると、コード エディターで `Application` クラス ファイル (*Application.xaml.vb*) が開きます。 ファイルが存在しない場合、プロジェクト デザイナーで、適切なクラス名と名前空間を使用して作成されます。

特定のアプリケーション状態が変化すると (アプリケーション スタートアップやシャットダウンなどで)、<xref:System.Windows.Application> オブジェクトでイベントが発生します。 このクラスで公開されるイベントの完全な一覧については、「<xref:System.Windows.Application>」を参照してください。 これらのイベントは、`Application` 部分クラスのユーザー コード セクションで処理されます。
