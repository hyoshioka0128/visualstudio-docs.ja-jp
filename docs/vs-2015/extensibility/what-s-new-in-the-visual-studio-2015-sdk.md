---
title: Visual Studio 2015 SDK の新機能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c64aac80-a411-463f-b7bd-8b7607a52ece
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d47e40a5c38eeb7898aa179282fa55bbe17ef1d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75917330"
---
# <a name="what39s-new-in-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK の新機能&#39;
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual studio SDK には、Visual Studio 2015、visual Studio 2015 更新済み、および Visual Studio 2017 の新機能と更新された機能があります。

## <a name="visual-studio-2017"></a>Visual Studio 2017

Visual Studio 2017 以降では、プロジェクトと項目のカスタム テンプレートのスキャンは実行されなくなりました。 代わりに、拡張機能で、これらのテンプレートのインストール場所を記述するテンプレート マニフェスト ファイルを提供する必要があります。 Visual Studio 2017 を使用して VSIX 拡張機能を更新できます。 MSI を使用して拡張機能を展開する場合は、テンプレート マニフェスト ファイルを手動で生成する必要があります。 詳細については、「 [カスタム Visual Studio のプロジェクトと項目テンプレート2017のアップグレード](/visualstudio/extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017?view=vs-2015)」を参照してください。 テンプレートマニフェストスキーマは、「 [Visual Studio テンプレートマニフェストスキーマリファレンス](/visualstudio/extensibility/visual-studio-template-manifest-schema-reference)」に記載されています。

## <a name="vs-2015-sdk-update-1"></a>VS 2015 SDK 更新プログラム1
 Update 1 には、拡張機能が配色テーマと Visual Studio image service に適した機能を提供するためのツールが含まれています。

 これらのトピックについては、「 [Vssdk Utilities](../extensibility/internals/vssdk-utilities.md) 」セクションを参照してください。

- [配色テーマツール](../extensibility/internals/color-theming-tools.md)は、Visual Studio のカスタム色を作成および編集するのに役立ちます。

- [Image Service Tools](../extensibility/internals/image-service-tools.md)を使用すると、Visual Studio のイメージマニフェストファイルを操作できます。

## <a name="new-way-to-add-the-visual-studio-sdk-to-visual-studio"></a>Visual Studio SDK を Visual Studio に追加するための新しい方法
 Visual Studio 2015 以降では、Visual Studio SDK を個別にダウンロードする必要はありません。 代わりに、通常のインストールプロセスの一部としてインストールすることも、後でインストールすることもできます。 VSIX ソリューションを開いたり作成したりすると、Visual Studio によって Visual Studio Extensibility Tools をインストールするように求めるメッセージが表示されます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="new-ways-of-creating-extensions"></a>拡張機能を作成するための新しい方法
 Visual Studio 2015 SDK 以降では、使用しているプログラミング言語に応じて、拡張機能を作成するためのさまざまなオプションが用意されています。

### <a name="visual-c-and-visual-basic"></a>Visual C# および Visual Basic
 C# および Visual Basic には、Vspackage、メニューコマンド、ツールウィンドウ、エディター分類子、エディターの装飾、エディターの余白拡張機能を作成するためのプロジェクト項目テンプレートが豊富に用意されています。 これらのいずれかまたはすべてを標準の VSIX プロジェクトに追加できます。 詳細については、次を参照してください。

- [メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)

- [ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)

- [エディターの項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- [VSPackage を使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-vspackage.md)

     VSPackage ウィザードでは、C# または Visual Basic に拡張機能が作成されなくなりました。

### <a name="c"></a>C++
 C++ の場合、VSPackage ウィザードでは、メニューコマンド、ツールウィンドウ、およびカスタムエディターがサポートされています。 **Visual C++/機能拡張**の [**新しいプロジェクト**] ダイアログで検索します。

## <a name="vs-sdk-reference-assemblies-via-nuget"></a>NuGet を使用した VS SDK 参照アセンブリ
 拡張機能プロジェクトの移植性と共有を強化するために、VS SDK 参照アセンブリの NuGet バージョンを使用できます。  これらは、 [VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility)によって発行された[nuget.org](https://www.nuget.org/)で使用でき、Visual Studio の [参照] **/[nuget パッケージの管理**] ダイアログボックスを使用して簡単にプロジェクトまたはソリューションに追加できます。 VS SDK [メタパッケージ](https://www.nuget.org/packages/VSSDK_Reference_Assemblies)を使用して、特定の機能拡張アセンブリに個別の参照を追加したり、すべての vs sdk 参照アセンブリを一度に追加したりできます。 NuGet の詳細については、「 [nuget の概要](/nuget/) 」および「 [ダイアログを使用した Nuget パッケージの管理](/nuget/consume-packages/install-use-packages-visual-studio)」を参照してください。

 VS SDK 参照アセンブリの NuGet バージョンを使用する場合、プロジェクトを開いてビルドするために、別のユーザーが VS SDK をインストールする必要はありません。  NuGet 参照アセンブリと VS SDK ビルドツールは、そのプロジェクトのコンピューターに自動的にインストールされます。

 VS SDK 項目テンプレートでは、その参照とビルドツールに NuGet が使用されるため、既定で NuGet の利点を得ることができます。

> [!NOTE]
> (\ VSSDK\VisualStudioIntegration\Common\Assemblies の下にある) プロジェクトと共に VS SDK のインストール済みの参照アセンブリを引き続き使用できます \<Visual Studio Install Location> 。また、NuGet パッケージを使用するために、既存の機能拡張プロジェクトをアップグレードする必要はありません。  [プロジェクト **参照]/[参照の追加** ] ダイアログでは、VS SDK がインストールした参照アセンブリが引き続き使用されます。
>
> NuGet を使用するように既存のプロジェクトを変更する場合は、「 [How to: Migrate vspackage To Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md) 」を参照してください。これには、機能拡張プロジェクトを nuget パッケージに更新するためのセクションがあります。

## <a name="light-bulbs"></a>電球
 拡張コードを記述する最も魅力的な新しい方法の1つは、Roslyn プロジェクトによって提供されます。 詳細については、「 [Roslyn](https://github.com/dotnet/Roslyn)」を参照してください。

 電球は、VSSDK に付属する新機能です。 これらは、Visual Studio エディターで使用されるアイコンであり、コードのリファクタリングアクションのセットまたは組み込みコードアナライザーによって識別された問題の修正を表示するために展開されます。 詳細については、「 [チュートリアル: 電球の提案を表示](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)する」を参照してください。

## <a name="updated-user-experience-guidelines"></a>更新されたユーザーエクスペリエンスガイドライン
 Visual Studio の新しい拡張機能または機能の設計 更新され、拡張された [Visual Studio ユーザーエクスペリエンスガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)を確認してください。  ここでは、新しい UI を Visual Studio とシームレスに統合するために必要な、 [カラートークン](../extensibility/ux-guidelines/shared-colors-for-visual-studio.md)、 [フォントサイズ](../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)、 [ダイアログレイアウトの仕様](../extensibility/ux-guidelines/layout-for-visual-studio.md)、およびその他のガイダンスについて説明します。
