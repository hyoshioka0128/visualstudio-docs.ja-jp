---
title: '[アプリケーション] ページ (プロジェクト デザイナー) (C#) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesApplicationWPF
- cs.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
ms.assetid: f13701a8-4e2e-4474-9d60-bb43decbe0c1
caps.latest.revision: 61
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dcd9b9d5e336bfa0595ddd6d70032f7ba7fe780a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299394"
---
# <a name="application-page-project-designer-c"></a>[アプリケーション] ページ (プロジェクト デザイナー) (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー**の **[アプリケーション]** ページを使用して、プロジェクトのアプリケーション設定とプロパティを指定します。

 **[アプリケーション]** ページにアクセスするには、**ソリューション エクスプローラー**のプロジェクト ノード ( **[ソリューション]** ノードではありません) を選択します。 その後、メニュー バーで **[プロジェクト]** 、 **[プロパティ]** の順に選択します。 プロジェクト デザイナーが表示されたら、 **[アプリケーション]** タブをクリックします。

 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

## <a name="general-application-settings"></a>アプリケーションの全般設定
 次のオプションでは、アプリケーションの全般設定を構成できます。

 **アセンブリ マニフェスト** アセンブリ マニフェストを保持する出力ファイルの名前を指定します。 このプロパティを変更すると、 **[出力名]** プロパティも変更されます。 コマンド ラインから [/out (C# コンパイラ オプション)](https://msdn.microsoft.com/library/70d91d01-7bd2-4aea-ba8b-4e9807e9caa5) を使用して、変更することもできます。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.AssemblyName%2A>」を参照してください。

 **既定の名前空間** プロジェクトに追加されるファイルの基本の名前空間を指定します。

 コードでの名前空間の作成の詳細については、[namespace](https://msdn.microsoft.com/library/0a788423-9110-42e0-97d9-bda41ca4870f) に関するページを参照してください。

 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.RootNamespace%2A>」を参照してください。

 **ターゲット フレームワーク** アプリケーションが対象とする .NET Framework のバージョンを指定します。 このオプションの値は、コンピューター上にインストールされている .NET Framework のバージョンによって異なる場合があります。

 既定では、この値は、 **[新しいプロジェクト]** ダイアログ ボックスで選択したターゲット フレームワークと同じです。

> [!NOTE]
> [[必須コンポーネント] ダイアログ ボックス](../../ide/reference/prerequisites-dialog-box.md)にリストされている必須コンポーネントのパッケージは、ダイアログ ボックスを初めて開いたときに自動的に設定されます。 その後、プロジェクトのターゲット フレームワークを変更した場合は、新しいターゲット フレームワークに合わせて必須パッケージを手動で選択する必要があります。

 詳細については、「[方法: .NET Framework のバージョンをターゲットにする](../../ide/how-to-target-a-version-of-the-dotnet-framework.md)」と「[Visual Studio のマルチ ターゲットの概要](../../ide/visual-studio-multi-targeting-overview.md)」を参照してください。

 **アプリケーションの種類** ビルドするアプリケーションの種類を指定します。 [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] アプリの場合は、 **[Windows ストア アプリ]** 、 **[クラス ライブラリ]** 、または **[WinMD ファイル]** を指定できます。 他のほとんどのアプリケーションの種類では、 **[Windows アプリケーション]** 、 **[コンソール アプリケーション]** 、 **[クラス ライブラリ]** 、 **[Windows サービス]** 、または **[Web コントロール ライブラリ]** を指定できます。

 Web アプリケーション プロジェクトでは、 **[クラス ライブラリ]** を指定する必要があります。

 **[WinMD ファイル]** オプションを指定した場合、種類を Windows ランタイムのプログラミング言語に射影できます。 WinMD ファイルとしてプロジェクトの出力をパッケージ化することで、複数の言語でアプリケーションをコード化し、すべて同じ言語で記述した場合と同様に、コードを相互運用することができます。 [!INCLUDE[win8_appname_long](../../includes/win8-appname-long-md.md)] アプリを含む、Windows ランタイム ライブラリをターゲットとするソリューションに対して、このオプションを指定できます。 詳細については、「[C# および Visual Basic での Windows ランタイム コンポーネントの作成](https://go.microsoft.com/fwlink/?LinkId=231895)」を参照してください。

> [!NOTE]
> Windows ランタイムでは、どの言語で使用される場合でも、ネイティブ オブジェクトとして表示されるように種類を射影できます。 たとえば、Windows ランタイムと対話する JavaScript アプリケーションでは JavaScript オブジェクト セットとして使用され、C# アプリケーションでは .NET オブジェクト コレクションとしてライブラリが使用されます。 WinMD ファイルとしてプロジェクトの出力をパッケージ化することで、Windows ランタイムで使用されるのと同じテクノロジを利用できます。

 **[アプリケーションの種類]** プロパティの詳細については、「[/target (C# コンパイラ オプション)](https://msdn.microsoft.com/library/a18bbd8e-bbf7-49e7-992c-717d0eb1f76f)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.OutputType%2A>」を参照してください。

 **アセンブリ情報** このボタンをクリックすると、[[アセンブリ情報] ダイアログ ボックス](../../ide/reference/assembly-information-dialog-box.md)が表示されます。

 **[スタートアップ オブジェクト]** では、アプリケーションの読み込み時に呼び出されるようにエントリ ポイントを定義します。 通常、これは、アプリケーションのメイン フォーム、またはアプリケーションの起動時に実行する必要がある `Main` プロシージャに設定されます。 クラス ライブラリにはエントリ ポイントがないため、このプロパティのオプションのみが **[(設定なし)]** となります。

 WPF ブラウザー アプリケーション プロジェクトでは、このオプションは既定で **[(設定なし)]** となります。 その他のオプションは、*プロジェクト名*.App となります。 この種のプロジェクトでは、アプリケーションの起動時に UI リソースを読み込むようにスタートアップ UI を設定する必要があります。 これを行うには、プロジェクトで Application.xaml ファイルを開き、プロジェクトの .xaml ファイル (Window1.xaml など) に `StartupUri` プロパティを設定します。 指定できルート要素の一覧については、「<xref:System.Windows.Application.StartupUri%2A>」を参照してください。 プロジェクトのクラスに `public static void Main()` メソッドを定義する必要もあります。 このクラスは、 **[スタートアップ オブジェクト]** 一覧に *ProjectName.ClassName* として表示されます。 その後、スタートアップ オブジェクトとしてクラスを選択できます。

 詳細については、「[/main (C# コンパイラ オプション)](https://msdn.microsoft.com/library/975cf4d5-36ac-4530-826c-4aad0c7f2049)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.StartupObject%2A>」を参照してください。

## <a name="resources"></a>リソース
 次のオプションでは、アプリケーションの全般設定を構成できます。

 **アイコンとマニフェスト** 既定では、このオプション ボタンが選択され、 **[アイコン]** と **[マニフェスト]** オプションが有効になります。 したがって、独自のアイコンを選択することも、別のマニフェスト生成オプションを選択することもできます。 プロジェクトのリソース ファイルをプロビジョニングする場合を除き、このオプション ボタンは選択したままにしておいてください。

 **アイコン** プログラム アイコンとして使用する .ico ファイルを設定します。 省略記号ボタンをクリックして既存のグラフィックを参照するか、必要なファイルの名前を入力します。 詳細については、「[/win32icon (C# コンパイラ オプション)](https://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138)」を参照してください。 プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>」を参照してください。

 **マニフェスト** Windows Vista 上で、ユーザー アカウント制御 (UAC) 下でアプリケーションを実行する場合に、マニフェスト生成オプションを選択します。 このオプションには、次の値を指定できます。

- **マニフェストを既定の設定で埋め込みます**。 Windows Vista での Visual Studio の標準的な操作方法がサポートされます。つまり、アプリケーションの実行可能ファイルにセキュリティ情報を埋め込む場合は、`requestedExecutionLevel` を `AsInvoker` に指定します。 これは、既定の設定です。

- **マニフェストなしでアプリケーションを作成します**。 このメソッドは*仮想化*といいます。 以前のアプリケーションとの互換性を保つために、このオプションを使用します。

- **Properties\app.manifest**。 このオプションは、ClickOnce または Registration-Free COM で配置されるアプリケーションで必要になります。 ClickOnce 配置を使用してアプリケーションを発行する場合、このオプションに自動的に**マニフェスト**が設定されます。

  **リソース ファイル** プロジェクトのリソース ファイルをプロビジョニングする場合は、このオプション ボタンを選択します。 このオプションを選択すると、 **[アイコン]** と **[マニフェスト]** オプションが無効になります。

  パス名を入力するか、参照ボタン ( **...** ) を使用して、Win32 リソース ファイルをプロジェクトに追加します。

## <a name="see-also"></a>関連項目
[アプリケーション プロパティの管理](../../ide/application-properties.md) [Office ソリューションのコードの記述](https://msdn.microsoft.com/library/2d4d8fd0-e881-4829-976f-0d1a9221dec0)
