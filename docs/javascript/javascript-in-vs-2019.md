---
title: Visual Studio 2019 の JavaScript および TypeScript
ms.date: 03/16/2020
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.openlocfilehash: 199a27dbfef2b7297563e87d973137e2acd9c745
ms.sourcegitcommit: eef26de3d7a5c971baedbecf3b4941fb683ddb2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81544290"
---
# <a name="javascript-and-typescript-in-visual-studio-2019"></a>Visual Studio 2019 の JavaScript および TypeScript

## <a name="overview"></a>概要

Visual Studio 2019 は、JavaScript 開発のサポートが充実しており、JavaScript を直接使用することも、[TypeScript プログラミング言語](http://www.typescriptlang.org/)を使用することもできます。TypeScript プログラミング言語は、特に大規模なプロジェクトの開発で、JavaScript 開発の生産性や楽しさが向上するように作成されています。 Visual Studio では、多くのアプリケーション タイプやサービス用に JavaScript または TypeScript コードを記述できます。

## <a name="javascript-language-service"></a>JavaScript 言語サービス

Visual Studio 2019 の JavaScript エクスペリエンスは、TypeScript サポートを提供するのと同じエンジンで実現されています。 このため、機能のサポートや豊富さが向上し、統合も簡単に行えるようになっています。

レガシ JavaScript 言語サービスに復元するオプションは、利用できなくなりました。 現在は、すぐに利用できる新しい JavaScript 言語サービスが用意されています。 新しい言語サービスは、静的分析によって強化された TypeScript 言語サービスのみをベースにしています。 これによりツールの機能が向上するため、JavaScript コードは型定義に基づく高度な IntelliSense の恩恵を受けられるようになります。 新しいサービスは軽量で、消費メモリがレガシ サービスより少ないため、コード サイズが大きくなっても、優れたパフォーマンスが得られます。 また、より大きなプロジェクトを処理するために、言語サービスのパフォーマンスが向上しています。

## <a name="typescript-support"></a>TypeScript のサポート

Visual Studio 2019 では、TypeScript のコンパイルをプロジェクトに統合するためのオプションが複数用意されています。

* [TypeScript NuGet パッケージ](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)。 TypeScript 3.2 以降の NuGet パッケージがプロジェクトにインストールされているときは、対応するバージョンの TypeScript 言語サービスがエディターに読み込まれます。
* [TypeScript npm パッケージ](https://www.npmjs.com/package/typescript)。 TypeScript 2.1 以降の npm パッケージがプロジェクトにインストールされているときは、対応するバージョンの TypeScript 言語サービスがエディターに読み込まれます。
* Visual Studio のインストーラーで既定で使用可能な TypeScript SDK、および [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.typescript-331-vs2017) からダウンロードされたスタンドアロンの SDK。

> [!TIP]
> プロジェクトが Visual Studio 2019 で開発されている場合は、TypeScript NuGet または TypeScript npm パッケージを使用することをお勧めします。これにより、さまざまなプラットフォームや環境の間で移植性が向上します。

NuGet パッケージの一般的な使用方法の 1 つは、.NET Core CLI を使用して TypeScript をコンパイルすることです。 TypeScript SDK インストールからビルド ターゲットをインポートするように、プロジェクト ファイルを手動で編集しない限り、NuGet パッケージが `dotnet build` や `dotnet publish` などの .NET Core CLI コマンドを使用して TypeScript コンパイルを有効にする唯一の方法です。

## <a name="remove-default-imports-aspnet-core-projects"></a>既定のインポートの削除 (ASP.NET Core プロジェクト)

[非 SDK スタイルの形式](https://docs.microsoft.com/nuget/resources/check-project-format)を使用する以前のプロジェクトでは、一部のプロジェクト ファイルの要素を削除する必要がある場合があります。

プロジェクトの MSBuild サポートに NuGet パッケージを使用している場合、プロジェクト ファイルで `Microsoft.TypeScript.Default.props` または `Microsoft.TypeScript.targets` をインポートしないでください。 ファイルは NuGet パッケージによってインポートされるため、個別に含めると、意図しない動作が発生する可能性があります。

1. プロジェクトを右クリックして **[プロジェクトのアンロード]** を選択します。

1. プロジェクトを右クリックし、 **[\<*プロジェクト ファイル名*\> の編集]** を選択します。

   プロジェクト ファイルが開きます。

1. `Microsoft.TypeScript.Default.props` および `Microsoft.TypeScript.targets` への参照を削除します。

   削除するインポートは、次のようになります。

   ```xml
   <Import
      Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.Default.props"
      Condition="Exists('$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.Default.props')" />

   <Import
      Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.targets"
      Condition="Exists('$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.targets')" />
   ```

## <a name="projects"></a>プロジェクト

Visual Studio 2019 で、UWP JavaScript アプリはサポートされなくなりました。 JavaScript UWP プロジェクト (拡張子が *.jsproj* のファイル) は、作成することも、開くこともできません。 詳細については、Windows 上で適切に実行される[プログレッシブ Web アプリ (PWA) の作成](/microsoft-edge/progressive-web-apps/get-started)に関するドキュメントを参照してください。
