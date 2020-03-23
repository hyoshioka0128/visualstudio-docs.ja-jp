---
title: ビルド システムのカスタマイズ
description: この記事は、Visual Studio for Mac で利用される MSBuild ビルド システムの概要です
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/19/2019
ms.assetid: 6958B102-8527-4B40-BC65-3505DB63F9D3
ms.openlocfilehash: 0c511c448136210038f1034321a2828e5153add1
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "71128387"
---
# <a name="customizing-the-build-system"></a>ビルド システムのカスタマイズ

Microsoft Build Engine は、アプリケーションをビルドするためのプラットフォームです。 MSBuild とも呼ばれているこのエンジンは Microsoft によって開発され、.NET アプリケーションの構築を可能にします。 Mono フレームワークはまた、Microsoft のビルド エンジンを独自に実装しています。それが **xbuild** です。 ただし、現時点では xbuild は廃止となり、すべてのオペレーティング システムで MSBuild が使用されています。

**MSBuild** は、Visual Studio for Mac でプロジェクトのビルド システムとして使用されており、ソース ファイルなど、一連の入力を受け取ることで動作し、入力を実行可能ファイルなどの出力に変換し、コンパイラのようなツールを呼び出すことでその出力を実行します。 この出力は、コンパイラのようなツールを呼び出して行われます。

## <a name="msbuild-file"></a>MSBuild ファイル

MSBuild は、プロジェクト ファイルと呼ばれる XML ファイルを使用します。このファイルはプロジェクトの一部である*アイテム* (イメージ リソースなど) とプロジェクトのビルドに必要な*プロパティ*を定義します。 このプロジェクト ファイルのファイル拡張子は常に `proj` で終わります。たとえば、C# プロジェクトの場合、`.csproj` になります。

### <a name="viewing-the-msbuild-file"></a>MSBuild ファイルを表示する

MSBuild ファイルを見つけるには、プロジェクト名を右クリックし、 **[Finder に表示]** を選択します。 次の図のように、この Finder ウィンドウには、`.csproj` ファイルなど、プロジェクトに関連するすべてのファイルとフォルダーが表示されます。

![Finder での csproj の場所](media/customizing-build-system-image1.png)

Visual Studio for Mac で新しいタブに `.csproj` を表示するには、プロジェクト名を右クリックし、 **[ツール]、[ファイルの編集]** の順に選択します。

![ソース エディターで csproj を開く](media/customizing-build-system-image2.png)

### <a name="composition-of-the-msbuild-file"></a>MSBuild ファイルの構成

すべての MSBuild ファイルに、次のように必須のルート `Project` 要素が含まれています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="14.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
</Project>
```

通常、プロジェクトは `.targets` ファイルもインポートします。 このファイルには、さまざまなファイルを処理し、ビルドする方法を説明したルールがたくさん含まれています。 通常、このインポートは `proj` ファイルの下のほうに表示されます。C# プロジェクトの場合、次の画像のようになります。

```xml
<Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
```

ターゲット ファイルは別の MSBuild ファイルです。 このファイルに含まれる MSBuild コードは、複数のプロジェクトで再利用できます。 たとえば、`Microsoft.CSharp.targets` プロパティ (または変数) で表されるディレクトリにある `MSBuildBinPath` ファイルには、C# ソース ファイルから C# アセンブリをビルドするためのロジックが含まれています。

### <a name="items-and-properties"></a>項目とプロパティ

MSBuild には、*項目*と*プロパティ*という 2 つの基本データ型があります。詳細については後述します。

#### <a name="properties"></a>Properties

プロパティは、コンパイラ オプションなど、コンパイル設定を格納するための鍵と値のペアです。

プロパティは PropertyGroup を利用して設定されます。また、プロパティには、任意の数の PropertiesGroups を追加できます (PropertiesGroups にはさらに任意の数のプロパティを追加できます)。

たとえば、簡単なコンソール アプリケーションの PropertyGroup は次の XML のようになります。

```xml
<PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">x86</Platform>
    <ProjectGuid>{E248730E-1393-43CC-9183-FFA42F63BE81}</ProjectGuid>
    <OutputType>Exe</OutputType>
    <RootNamespace>refactoring</RootNamespace>
    <AssemblyName>refactoring</AssemblyName>
    <TargetFrameworkVersion>v4.5</TargetFrameworkVersion>
</PropertyGroup>
```

プロパティは `$()` 構文を利用して式から参照できます。 たとえば、`$(Foo)` は `Foo` プロパティの値として評価されます。 プロパティが設定されていない場合、エラーなしで、空の文字列として評価されます。

#### <a name="items"></a>アイテム

項目を利用することで、ビルド システムへの入力をリストやセットとして扱うことができます。項目は一般的にファイルを表します。 項目にはそれぞれ、項目の*種類*と*仕様*が与えられ、任意で*メタデータ*が指定されます。 MSBuild が個々の項目に対して機能することはありません。項目*セット*と呼ばれる、特定の種類のすべての項目に対して機能します。

項目は、`ItemGroup` を宣言することで作成されます。 任意の数の項目を含めた ItemGroups をさらに任意の数だけ作成できます。

たとえば、次のコード スニペットでは、iOS の起動画面が作成されます。 起動画面には、ビルドの種類 `BundleResource` と、イメージのパスの指定が表示されます。

```xml
 <ItemGroup>
    <BundleResource Include="Resources\Default-568h%402x.png" />
    <BundleResource Include="Resources\Default%402x.png" />
    <BundleResource Include="Resources\Default.png" />
    <BundleResource Include="Resources\Default-Portrait.png" />
    <BundleResource Include="Resources\Default-Portrait%402x.png" />
    <BundleResource Include="Resources\Default-Landscape%402x.png" />
  </ItemGroup>
 ```

 項目セットは、`@()` 構文を利用して式から参照できます。 たとえば、`@(BundleResource)` は BundleResource 項目セットとして評価されます。すべての BundleResource 項目を意味します。 この種類の項目がない場合、エラーなしで空になります。

## <a name="resources-for-learning-msbuild"></a>MSBuild の学習リソース

次のリソースで MSBuild についてさらに詳しく学習できます。

* [MSBuild の概要](/visualstudio/msbuild/msbuild)
* [MSBuild の概念](/visualstudio/msbuild/msbuild-concepts)
