---
title: ラウンドトリップ拡張機能について
ms.date: 06/25/2017
ms.topic: conceptual
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: madsk
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: 44b5c5c58c46017730f06142548505c628894a11
ms.sourcegitcommit: b04c603ce73b993d042ebdf7f3722cf4fe2ef7f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74316486"
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-2017-and-visual-studio-2015"></a>方法: 拡張機能を Visual Studio 2017 および Visual Studio 2015 と互換性を持たせる

このドキュメントでは、拡張機能プロジェクトを Visual Studio 2015 と Visual Studio 2017 間でラウンドトリップさせる方法について説明します。 このアップグレードを完了すると、Visual Studio 2015 と Visual Studio 2017 の両方でプロジェクトを開いてビルド、インストール、および実行できるようになります。 参照として、Visual Studio 2015 と Visual Studio 2017 間でラウンドトリップできる一部の拡張機能については、 [VS SDK の機能拡張のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)を参照してください。

Visual Studio 2017 でビルドするだけで、出力 VSIX を Visual Studio 2015 と Visual Studio 2017 の両方で実行する場合は、[拡張機能の移行](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)に関するドキュメントを参照してください。

> [!NOTE]
> Visual Studio のバージョン間の変更により、1つのバージョンで動作していたものが、別のバージョンでは機能しません。 アクセスしようとしている機能が両方のバージョンで利用可能であること、または拡張機能に予期しない結果が含まれていることを確認してください。

VSIX をラウンドトリップするためにこのドキュメントで実行する手順の概要を以下に示します。

1. 適切な NuGet パッケージをインポートします。
2. 拡張機能マニフェストを更新します。
    * インストールの対象
    * 前提条件
3. CSProj を更新します。
    * `<MinimumVisualStudioVersion>` を更新します。
    * `<VsixType>` プロパティを追加します。
    * デバッグ プロパティ `($DevEnvDir)` を 3 回追加します。
    * ビルド ツールをインポートするための条件と対象を追加します。

4. ビルドとテストを行います。

## <a name="environment-setup"></a>環境のセットアップ

このドキュメントは、コンピューターに以下をインストール済みであることを前提としています。

* VS SDK がインストールされた Visual Studio 2015
* 拡張機能ワークロードがインストールされた Visual Studio 2017

## <a name="recommended-approach"></a>推奨される方法

このアップグレードは、Visual Studio 2017 ではなく、Visual Studio 2015 で開始することを強くお勧めします。 Visual Studio 2015 で開発を行う主な利点は、Visual Studio 2015 で利用できないアセンブリの参照を確実に排除できるという点です。 Visual Studio 2017 で開発を行うと、Visual Studio 2017 にのみ存在するアセンブリへの依存関係を導入してしまうリスクがあります。

## <a name="ensure-there-is-no-reference-to-projectjson"></a>project.json への参照を確実に排除する

このドキュメントの後半で、* *.csproj*ファイルに条件付きインポートステートメントを挿入します。 これは、NuGet の参照が*プロジェクトの json*に格納されている場合には機能しません。 そのため、すべての NuGet 参照を*パッケージの .config*ファイルに移動することをお勧めします。
プロジェクトに*プロジェクトの json*ファイルが含まれている場合:

* *プロジェクトの json*で参照をメモしておきます。
* **ソリューションエクスプローラー**から、プロジェクトから*プロジェクトの json*ファイルを削除します。 これにより、*プロジェクトの json*ファイルが削除され、プロジェクトから削除されます。
* NuGet の参照をプロジェクトに再び追加します。
  * **ソリューション**を右クリックし、 **[ソリューションの NuGet パッケージの管理]** を選択します。
  * 自動的に*パッケージの .config*ファイルが作成されます。

> [!NOTE]
> プロジェクトに EnvDTE パッケージが含まれている場合は、参照を右クリックし **、[参照**の**追加**] を選択して適切な参照を追加することで、追加する必要がある場合があります。 NuGet パッケージを使用すると、プロジェクトのビルドを試みたときにエラーが発生する可能性があります。

## <a name="add-appropriate-build-tools"></a>適切なビルドツールを追加する

ビルドとデバッグを正しく実行できるビルド ツールを確実に追加する必要があります。 そのために、Microsoft は Microsoft.VisualStudio.Sdk.BuildTasks というアセンブリを作成しました。

Visual Studio 2015 と 2017 の両方で VSIXv3 をビルドして展開するには、次の NuGet パッケージが必要となります。

バージョン | ビルド ツール
--- | ---
Visual Studio 2015 | Microsoft.VisualStudio.Sdk.BuildTasks.14.0
Visual Studio 2017 | Microsoft.VSSDK.BuildTool

次の手順に従います。

* NuGet パッケージ Microsoft.VisualStudio.Sdk.BuildTasks.14.0 をプロジェクトに追加します。
* プロジェクトに Microsoft.VSSDK.BuildTools が含まれていない場合は、追加します。
* Microsoft.VSSDK.BuildTools のバージョンが 15.x 以上であることを確認します。

## <a name="update-extension-manifest"></a>拡張機能マニフェストの更新

### <a name="1-installation-targets"></a>1. インストールターゲット

VSIX をビルドする対象のバージョンを Visual Studio に指示する必要があります。 通常、これらの参照は、バージョン 14.0 (Visual Studio 2015)、バージョン 15.0 (Visual Studio 2017)、またはバージョン 16.0 (Visual Studio 2019) のいずれかになります。 ここでは、両方に対応する拡張機能をインストールする VSIX をビルドしたいので、両方のバージョンを対象にする必要があります。 14.0 より前のバージョンで VSIX をビルドおよびインストールしたい場合は、前のバージョン番号を設定すれば可能です。ただし、10.0 以前のバージョンはサポートされていません。

* Visual Studio で*source.extension.vsixmanifest*ファイルを開きます。
* **[Install Targets]\(インストールの対象)\** タブを開きます。
* **バージョン範囲**を [14.0, 17.0) に変更します。 '[' は、14.0 とそれより前のすべてのバージョンを含めるよう Visual Studio に指示します。 ') ' は、バージョン17.0 までのすべてのバージョンを含むように Visual Studio に指示します。
* すべての変更を保存し、Visual Studio のすべてのインスタンスを閉じます。

![インストールの対象の画像](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2. *source.extension.vsixmanifest*ファイルに必須コンポーネントを追加する

前提条件として、Visual Studio コアエディターが必要です。 Visual Studio を開き、更新されたマニフェストデザイナーを使用して、前提条件を挿入します。

この操作を手動で行うには、次の手順に従います。

* エクスプローラーでプロジェクト ディレクトリに移動します。
* テキストエディターを使用して*source.extension.vsixmanifest*ファイルを開きます。
* 次のタグを追加します。

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* ファイルを保存して閉じます。

> [!NOTE]
> Visual Studio 2017 のすべてのバージョンと互換性があることを確認するために、前提条件のバージョンを手動で編集することが必要になる場合があります。 なぜならば、デザイナーは最小バージョンをVisual Studio の現在のバージョンとして挿入するからです (例: 15.0.26208.0)。 しかし、他のユーザーがそれより前のバージョンを使用している可能性があるため、これを 15.0 に編集する必要があります。

この時点で、マニフェスト ファイルは次のようになります。

![必須コンポーネントの例](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>プロジェクト ファイル (myproject.csproj) を変更する

この手順を実行する間、変更した .csproj への参照を開いておくことを強くお勧めします。 [ここ](https://github.com/Microsoft/VSSDK-Extensibility-Samples)でいくつかの例を入手できます。 拡張機能のサンプルを選択し、参照用の *.csproj*ファイルを見つけて、次の手順を実行します。

* **エクスプローラー**でプロジェクトディレクトリに移動します。
* テキストエディターを使用して*myproject*ファイルを開きます。

### <a name="1-update-the-minimumvisualstudioversion"></a>1. MinimumVisualStudioVersion を更新します。

* Visual Studio の最小バージョンを `$(VisualStudioVersion)` に設定し、その条件付きステートメントを追加します。 以下のタグが存在しない場合は、追加します。 タグが次のように設定されていることを確認してください。

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2. VsixType プロパティを追加します。

* プロパティ グループに次のタグ `<VsixType>v3</VsixType>` を追加します。

> [!NOTE]
> `<OutputType></OutputType>` タグの下に追加することをお勧めします。

### <a name="3-add-the-debugging-properties"></a>3. デバッグプロパティを追加する

* 次のプロパティ グループを追加します。

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartProgram>$(DevEnvDir)devenv.exe</StartProgram>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* *.Csproj*ファイルと *.csproj*ファイルから、次のコード例のすべてのインスタンスを削除します。

```xml
<StartAction>Program</StartAction>
<StartProgram>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartProgram>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4. ビルドツールのインポートに条件を追加する

* Microsoft.VSSDK.BuildTools 参照を含んでいる `<import>` タグに、その他の条件付きステートメントを追加します。 Condition ステートメントの前に `'$(VisualStudioVersion)' != '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのヘッダーとフッターに表示されます。

例 :

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* Microsoft.VisualStudio.Sdk.BuildTasks.14.0 を含んでいる `<import>` タグに、その他の条件付きステートメントを追加します。 Condition ステートメントの前に `'$(VisualStudioVersion)' == '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのヘッダーとフッターに表示されます。

例 :

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* Microsoft.VSSDK.BuildTools 参照を含んでいる `<Error>` タグに、その他の条件付きステートメントを追加します。 これを行うには、条件付きステートメントの前に `'$(VisualStudioVersion)' != '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのフッターに表示されます。

例 :

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* Microsoft.VisualStudio.Sdk.BuildTasks.14.0 を含んでいる `<Error>` タグに、その他の条件付きステートメントを追加します。 Condition ステートメントの前に `'$(VisualStudioVersion)' == '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのフッターに表示されます。

例 :

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* csproj ファイルを保存して閉じます。

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2017"></a>Visual Studio 2015 と Visual Studio 2017 で拡張機能のインストールをテストする

この時点で、プロジェクトは Visual Studio 2015 と Visual Studio 2017 の両方にインストール可能な VSIXv3 をビルドできる状態になっているはずです。

* Visual Studio 2015 でプロジェクトを開きます。
* プロジェクトをビルドし、VSIX が正しくビルドされたことを出力で確認します。
* プロジェクトディレクトリに移動します。
* *\Bin\debug*フォルダーを開きます。
* VSIX ファイルをダブルクリックし、Visual Studio 2015 および Visual Studio 2017 に拡張機能をインストールします。
* **[インストール済み]** セクションの [**ツール** > の**拡張機能と更新プログラム**] に拡張機能が表示されていることを確認してください。
* 拡張機能を実行または使用して、機能することを確認します。

![VSIX の検索](media/finding-a-VSIX-example.png)

> [!NOTE]
> **ファイルを開い**たメッセージでプロジェクトがハングした場合は、Visual Studio を強制的にシャットダウンし、プロジェクトディレクトリに移動して、隠しフォルダーを表示し、 *vs*フォルダーを削除します。
 