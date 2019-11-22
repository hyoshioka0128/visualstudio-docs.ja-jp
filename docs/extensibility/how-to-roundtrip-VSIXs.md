---
title: How to Roundtrip Extensions
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
# <a name="how-to-make-extensions-compatible-with-visual-studio-2017-and-visual-studio-2015"></a>How to: Make extensions compatible with Visual Studio 2017 and Visual Studio 2015

このドキュメントでは、拡張機能プロジェクトを Visual Studio 2015 と Visual Studio 2017 間でラウンドトリップさせる方法について説明します。 このアップグレードを完了すると、Visual Studio 2015 と Visual Studio 2017 の両方でプロジェクトを開いてビルド、インストール、および実行できるようになります。 As a reference, some extensions that can round-trip between Visual Studio 2015 and Visual Studio 2017 can be found in the [VS SDK extensibility samples](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

If you only intend to build in Visual Studio 2017, but want the output VSIX to run in both Visual Studio 2015 and Visual Studio 2017, then refer to the [Extension migration document](how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

> [!NOTE]
> Due to changes in Visual Studio between versions, some things that worked in one version don't work in another. Ensure that the features you are trying to access are available in both versions or the extension will have unexpected results.

VSIX をラウンドトリップするためにこのドキュメントで実行する手順の概要を以下に示します。

1. 適切な NuGet パッケージをインポートします。
2. 拡張機能マニフェストを更新します。
    * インストールの対象
    * 必要条件
3. CSProj を更新します。
    * `<MinimumVisualStudioVersion>` を更新します。
    * `<VsixType>` プロパティを追加します。
    * デバッグ プロパティ `($DevEnvDir)` を 3 回追加します。
    * ビルド ツールをインポートするための条件と対象を追加します。

4. ビルドとテストを行います。

## <a name="environment-setup"></a>Environment setup

このドキュメントは、コンピューターに以下をインストール済みであることを前提としています。

* VS SDK がインストールされた Visual Studio 2015
* 拡張機能ワークロードがインストールされた Visual Studio 2017

## <a name="recommended-approach"></a>Recommended approach

このアップグレードは、Visual Studio 2017 ではなく、Visual Studio 2015 で開始することを強くお勧めします。 Visual Studio 2015 で開発を行う主な利点は、Visual Studio 2015 で利用できないアセンブリの参照を確実に排除できるという点です。 Visual Studio 2017 で開発を行うと、Visual Studio 2017 にのみ存在するアセンブリへの依存関係を導入してしまうリスクがあります。

## <a name="ensure-there-is-no-reference-to-projectjson"></a>project.json への参照を確実に排除する

Later in this document, we will insert conditional import statements in to your * *.csproj* file. This won't work if your NuGet references are stored in *project.json*. As such, it is advised to move all NuGet references to the *packages.config* file.
If your project contains a *project.json* file:

* Take a note of the references in *project.json*.
* From the **Solution Explorer**, delete the *project.json* file from the project. This deletes the *project.json* file and removes it from the project.
* Add the NuGet references back in to the project:
  * Right-click on the **Solution** and choose **Manage NuGet Packages for Solution**.
  * Visual Studio automatically creates the *packages.config* file for you.

> [!NOTE]
> If your project contained EnvDTE packages, they may need to be added by right clicking on **References** selecting **Add reference** and adding the appropriate reference. NuGet パッケージを使用すると、プロジェクトのビルドを試みたときにエラーが発生する可能性があります。

## <a name="add-appropriate-build-tools"></a>Add appropriate build tools

ビルドとデバッグを正しく実行できるビルド ツールを確実に追加する必要があります。 そのために、Microsoft は Microsoft.VisualStudio.Sdk.BuildTasks というアセンブリを作成しました。

Visual Studio 2015 と 2017 の両方で VSIXv3 をビルドして展開するには、次の NuGet パッケージが必要となります。

Version | ビルド ツール
--- | ---
Visual Studio 2015 | Microsoft.VisualStudio.Sdk.BuildTasks.14.0
Visual Studio 2017 | Microsoft.VSSDK.BuildTool

次の手順に従います。

* NuGet パッケージ Microsoft.VisualStudio.Sdk.BuildTasks.14.0 をプロジェクトに追加します。
* プロジェクトに Microsoft.VSSDK.BuildTools が含まれていない場合は、追加します。
* Microsoft.VSSDK.BuildTools のバージョンが 15.x 以上であることを確認します。

## <a name="update-extension-manifest"></a>Update extension manifest

### <a name="1-installation-targets"></a>1. Installation targets

VSIX をビルドする対象のバージョンを Visual Studio に指示する必要があります。 Typically, these references are either to version 14.0 (Visual Studio 2015), version 15.0 (Visual Studio 2017), or version 16.0 (Visual Studio 2019). ここでは、両方に対応する拡張機能をインストールする VSIX をビルドしたいので、両方のバージョンを対象にする必要があります。 14.0 より前のバージョンで VSIX をビルドおよびインストールしたい場合は、前のバージョン番号を設定すれば可能です。ただし、10.0 以前のバージョンはサポートされていません。

* Open the *source.extension.vsixmanifest* file in Visual Studio.
* **[Install Targets]\(インストールの対象)\** タブを開きます。
* Change the **Version Range** to [14.0, 17.0). '[' は、14.0 とそれより前のすべてのバージョンを含めるよう Visual Studio に指示します。 The  ')' tells Visual Studio to include all versions up to, but not including, version 17.0.
* すべての変更を保存し、Visual Studio のすべてのインスタンスを閉じます。

![インストールの対象の画像](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2. Adding Prerequisites to the *extension.vsixmanifest* file

We need the Visual Studio Core Editor as a prerequisite. Open Visual Studio and use the updated manifest designer to insert the prerequisites.

この操作を手動で行うには、次の手順に従います。

* エクスプローラーでプロジェクト ディレクトリに移動します。
* Open the *extension.vsixmanifest* file with a text editor.
* 次のタグを追加します。

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* ファイルを保存して閉じます。

> [!NOTE]
> You may need to manually edit the Prerequisite version to ensure it is compatible with all versions of Visual Studio 2017. なぜならば、デザイナーは最小バージョンをVisual Studio の現在のバージョンとして挿入するからです (例: 15.0.26208.0)。 しかし、他のユーザーがそれより前のバージョンを使用している可能性があるため、これを 15.0 に編集する必要があります。

この時点で、マニフェスト ファイルは次のようになります。

![必須コンポーネントの例](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>プロジェクト ファイル (myproject.csproj) を変更する

この手順を実行する間、変更した .csproj への参照を開いておくことを強くお勧めします。 [ここ](https://github.com/Microsoft/VSSDK-Extensibility-Samples)でいくつかの例を入手できます。 Select any extensibility sample, find the *.csproj* file for reference and execute the following steps:

* Navigate to the project directory in **File Explorer**.
* Open the *myproject.csproj* file with a text editor.

### <a name="1-update-the-minimumvisualstudioversion"></a>1. Update the MinimumVisualStudioVersion

* Visual Studio の最小バージョンを `$(VisualStudioVersion)` に設定し、その条件付きステートメントを追加します。 以下のタグが存在しない場合は、追加します。 タグが次のように設定されていることを確認してください。

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2. Add the VsixType property.

* プロパティ グループに次のタグ `<VsixType>v3</VsixType>` を追加します。

> [!NOTE]
> It is recommended to add this below the `<OutputType></OutputType>` tag.

### <a name="3-add-the-debugging-properties"></a>3. Add the debugging properties

* 次のプロパティ グループを追加します。

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartProgram>$(DevEnvDir)devenv.exe</StartProgram>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* Delete all instances of the following code example from the *.csproj* file and any *.csproj.user* files:

```xml
<StartAction>Program</StartAction>
<StartProgram>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartProgram>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4. Add conditions to the build tools imports

* Microsoft.VSSDK.BuildTools 参照を含んでいる `<import>` タグに、その他の条件付きステートメントを追加します。 Insert `'$(VisualStudioVersion)' != '14.0' And` at the front of the condition statement. これらのステートメントは、csproj ファイルのヘッダーとフッターに表示されます。

(例:

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* Microsoft.VisualStudio.Sdk.BuildTasks.14.0 を含んでいる `<import>` タグに、その他の条件付きステートメントを追加します。 Insert `'$(VisualStudioVersion)' == '14.0' And` at the front of the condition statement. これらのステートメントは、csproj ファイルのヘッダーとフッターに表示されます。

(例:

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* Microsoft.VSSDK.BuildTools 参照を含んでいる `<Error>` タグに、その他の条件付きステートメントを追加します。 これを行うには、条件付きステートメントの前に `'$(VisualStudioVersion)' != '14.0' And` を挿入します。 これらのステートメントは、csproj ファイルのフッターに表示されます。

(例:

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* Microsoft.VisualStudio.Sdk.BuildTasks.14.0 を含んでいる `<Error>` タグに、その他の条件付きステートメントを追加します。 Insert `'$(VisualStudioVersion)' == '14.0' And` at the front of the condition statement. これらのステートメントは、csproj ファイルのフッターに表示されます。

(例:

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* csproj ファイルを保存して閉じます。

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2017"></a>Visual Studio 2015 と Visual Studio 2017 で拡張機能のインストールをテストする

この時点で、プロジェクトは Visual Studio 2015 と Visual Studio 2017 の両方にインストール可能な VSIXv3 をビルドできる状態になっているはずです。

* Open your project in Visual Studio 2015.
* Build your project and confirm in the output that a VSIX builds correctly.
* Navigate to your project directory.
* Open the *\bin\Debug* folder.
* Double-click on the VSIX file and install your extension on Visual Studio 2015 and Visual Studio 2017.
* Make sure that you can see the extension in **Tools** > **Extensions and Updates** in the **Installed** section.
* Attempt to run/use the extension to check that it works.

![Find a VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> If your project hangs with the message **opening the file**, force shut down Visual Studio, navigate to your project directory, show hidden folders, and delete the *.vs* folder.
 