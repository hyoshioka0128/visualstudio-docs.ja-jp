---
title: C# プロジェクトのプロパティの [アプリケーション] ページ
ms.date: 10/30/2018
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesApplicationWPF
- cs.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ef9a38fc13d0d9c9f6b912f4cb2b83971d105c29
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595827"
---
# <a name="application-page-project-designer-c"></a>[アプリケーション] ページ (プロジェクト デザイナー) (C#)

**プロジェクト デザイナー**の **[アプリケーション]** ページを使用して、プロジェクトのアプリケーション設定とプロパティを指定します。

**[アプリケーション]** ページにアクセスするには、**ソリューション エクスプローラー**のプロジェクト ノード ( **[ソリューション]** ノードではありません) を選択します。 その後、メニュー バーで **[プロジェクト]**  >  **[プロパティ]** を選択します。 **プロジェクト デザイナー**が表示されたら、 **[アプリケーション]** タブをクリックします。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="general-application-settings"></a>アプリケーションの全般設定

次のオプションでは、アプリケーションの全般設定を構成できます。

**アセンブリ名**

アセンブリ マニフェストを保持する出力ファイルの名前を指定します。 このプロパティを変更すると、 **[出力名]** プロパティも変更されます。

コマンド ラインから [/out (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/out-compiler-option) を使用して、変更することもできます。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.AssemblyName%2A>」を参照してください。

**既定の名前空間**

プロジェクトに追加されるファイルの基本の名前空間を指定します。

コードでの名前空間の作成の詳細については、[namespace](/dotnet/csharp/language-reference/keywords/namespace) に関するページを参照してください。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.RootNamespace%2A>」を参照してください。

**ターゲット フレームワーク**

アプリケーションが対象とする .NET のバージョンを指定します。 このオプションの値は、コンピューター上にインストールされている .NET のバージョンによって異なる場合があります。

.NET Framework プロジェクトの場合、既定値は、プロジェクトを作成するときに指定したターゲット フレームワークと一致します。

.NET Core をターゲットにするプロジェクトの場合、利用できるバージョンが次のように表示されることがあります。

![.NET Core プロジェクトのターゲット フレームワーク バージョン](../media/application-target-framework.png)

> [!NOTE]
> [[必須コンポーネント] ダイアログ ボックス](../../ide/reference/prerequisites-dialog-box.md)にリストされている必須コンポーネントのパッケージは、ダイアログ ボックスを初めて開いたときに自動的に設定されます。 その後、プロジェクトのターゲット フレームワークを変更した場合は、新しいターゲット フレームワークに合わせて必須コンポーネントを手動で選択する必要があります。

詳細については、[フレームワークのターゲット設定](../../ide/visual-studio-multi-targeting-overview.md)に関するページを参照してください。

**出力の種類**

ビルドするアプリケーションの種類を指定します。 値は、プロジェクトの種類によって異なります。 たとえば、**コンソール アプリ** プロジェクトの場合は、出力の種類として **[Windows アプリケーション]** 、 **[コンソール アプリケーション]** 、または **[クラス ライブラリ]** を指定できます。

Web アプリケーション プロジェクトでは、 **[クラス ライブラリ]** を指定する必要があります。

**出力の種類**プロパティの詳細については、「[/target (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/target-compiler-option)」をご覧ください。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.OutputType%2A>」を参照してください。

**バインド リダイレクトの自動生成**

アプリまたはそのコンポーネントで同じアセンブリの複数のバージョンが参照されている場合、バインド リダイレクトがプロジェクトに追加されます。 プロジェクト ファイルにおいて手動でバインド リダイレクトを定義したい場合は、 **[バインド リダイレクトの自動生成]** をオフにします。

リダイレクトの詳細については、「[アセンブリ バージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions)」をご覧ください。

**スタートアップ オブジェクト**

アプリケーションの読み込み時に呼び出されるようにエントリ ポイントを定義します。 通常、これは、アプリケーションのメイン フォーム、またはアプリケーションの起動時に実行する必要がある `Main` プロシージャに設定されます。 クラス ライブラリにはエントリ ポイントがないため、このプロパティのオプションのみが **[(設定なし)]** となります。

WPF アプリ プロジェクトでは、このオプションは既定で **[(設定なし)]** に設定されます。 その他のオプションは、<プロジェクト名>.App になります。 WPF プロジェクトでは、アプリケーションの起動時に UI リソースを読み込むようにスタートアップ URI を設定する必要があります。 これを行うには、プロジェクトで *Application.xaml* ファイルを開き、プロジェクトの *.xaml* ファイル (*Window1.xaml* など) を `StartupUri` プロパティに設定します。 指定できルート要素の一覧については、「<xref:System.Windows.Application.StartupUri%2A>」を参照してください。 プロジェクトのクラスで `public static void Main()` メソッドを定義する必要もあります。 このクラスは、 **[スタートアップ オブジェクト]** 一覧に *ProjectName.ClassName* として表示されます。 その後、スタートアップ オブジェクトとしてクラスを選択できます。

詳細については、「[/main (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/main-compiler-option)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.StartupObject%2A>」を参照してください。

**アセンブリ情報**

このボタンをクリックすると、[[アセンブリ情報]](../../ide/reference/assembly-information-dialog-box.md) ダイアログ ボックスが開きます。

## <a name="resources"></a>リソース

**[リソース]** オプションは、アプリ用のリソース設定の構成に役立ちます。

**アイコンとマニフェスト**

既定では、このオプション ボタンが選択され、 **[アイコン]** と **[マニフェスト]** オプションが有効になります。 したがって、独自のアイコンを選択することも、別のマニフェスト生成オプションを選択することもできます。 プロジェクトのリソース ファイルをプロビジョニングする場合を除き、このオプション ボタンは選択したままにしておいてください。

**アイコン**

プログラム アイコンとして使用する *.ico* ファイルを設定します。 **[参照]** をクリックして既存のグラフィックを参照するか、必要なファイルの名前を入力します。 詳細については、「[/win32icon (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)」を参照してください。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>」を参照してください。

アイコン作成の詳細は、「[アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)」を参照してください。

**Manifest**

Windows Vista 上で、ユーザー アカウント制御 (UAC) 下でアプリケーションを実行する場合に、マニフェスト生成オプションを選択します。 このオプションには、次の値を指定できます。

- **マニフェストを既定の設定で埋め込みます**。 Windows Vista での Visual Studio の標準的な操作方法がサポートされます。つまり、アプリケーションの実行可能ファイルにセキュリティ情報を埋め込む場合は、`requestedExecutionLevel` を `AsInvoker` に指定します。 これは、既定の設定です。

- **マニフェストなしでアプリケーションを作成します**。 このメソッドは*仮想化*といいます。 以前のアプリケーションとの互換性を保つために、このオプションを使用します。

- **Properties\app.manifest**。 このオプションは、ClickOnce または Registration-Free COM で配置されるアプリケーションで必要になります。 ClickOnce 配置を使用してアプリケーションを発行する場合、このオプションに自動的に**マニフェスト**が設定されます。

**リソース ファイル**

プロジェクトにリソース ファイルを提供する場合は、このオプション ボタンを選択します。 このオプションを選択すると、 **[アイコン]** と **[マニフェスト]** オプションが無効になります。

パス名を入力するか、参照ボタン ( **...** ) を使用して、Win32 リソース ファイルをプロジェクトに追加します。

詳細については、「[.NET アプリ用のリソース ファイルを作成する](/dotnet/framework/resources/creating-resource-files-for-desktop-apps)」を参照してください。
