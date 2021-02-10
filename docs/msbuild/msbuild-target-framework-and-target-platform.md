---
title: MSBuild ターゲット フレームワークおよびターゲット プラットフォーム | Microsoft Docs
description: ターゲットのプラットフォームまたはソフトウェア アーキテクチャでターゲットの .NET Framework バージョンを実行する MSBuild プロジェクトを構築する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: df6517c5-edd6-4cc4-97ad-b3cdfc78e799
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f30308e2ccb66494251347c5fc29de5a115d8d77
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99878410"
---
# <a name="msbuild-target-framework-and-target-platform"></a>MSBuild ターゲット フレームワークおよびターゲット プラットフォーム

プロジェクトは *ターゲット フレームワーク* とターゲット プラットフォームで動作するようにビルドできます。ターゲット フレームワークとは .NET Framework の特定のバージョンを表し、*ターゲット プラットフォーム* とは特定のソフトウェア アーキテクチャを表します。  たとえば、80x86 プロセッサ ファミリ ("x86") と互換性のある 32 ビット プラットフォーム上の .NET Framework 2.0 で動作するアプリケーションを対象とすることができます。 ターゲット フレームワークとターゲット プラットフォームの組み合わせは *ターゲット コンテキスト* と呼ばれます。

> [!IMPORTANT]
> この記事では、ターゲット フレームワークを指定するための従来の方法を示します。 SDK スタイルのプロジェクトでは、netstandard のようなさまざまな TargetFrameworks が有効になります。 詳細については、「[ターゲット フレームワーク](/dotnet/standard/frameworks)」をご覧ください。

## <a name="target-framework-and-profile"></a>ターゲット フレームワークとプロファイル

 ターゲット フレームワークとは、ビルドするプロジェクトの実行対象とする .NET Framework の特定のバージョンを意味します。 ターゲット フレームワークの仕様は必須です。これは、ターゲット フレームワークの仕様によって、そのフレームワークのバージョン専用のコンパイラ機能とアセンブリ参照が利用可能になるためです。

 現在、.NET Framework については次のバージョンを使用できます。

- .NET Framework 2.0 (Visual Studio 2005 に付属)

- .NET Framework 3.0 (Windows Vista に付属)

- .NET Framework 3.5 (Visual Studio 2008 に付属)

- .NET Framework 4.5.2

- .NET Framework 4.6 (Visual Studio 2015 に付属)

- .NET Framework 4.6.1

- .NET Framework 4.6.2

- .NET Framework 4.7

- .NET Framework 4.7.1

- .NET Framework 4.7.2

- .NET Framework 4.8

.NET Framework の各バージョンでは、参照できるアセンブリの一覧がそれぞれ異なっています。 たとえば、WPF (Windows Presentation Foundation) アプリケーションをビルドするには、プロジェクトが .NET Framework のバージョン 3.0 以上 を対象としている必要があります。

ターゲット フレームワークは、プロジェクト ファイルの `TargetFrameworkVersion` プロパティで指定されます。 プロジェクトのターゲット フレームワークを変更するには、Visual Studio 統合開発環境 (IDE) でプロジェクトのプロパティ ページを使用します。 詳細については、[.NET Framework のターゲット バージョンを指定する](../ide/visual-studio-multi-targeting-overview.md)」を参照してください。 `TargetFrameworkVersion` に使用できる値は、`v2.0`、`v3.0`、`v3.5`、`v4.5.2`、`v4.6`、`v4.6.1`、`v4.6.2`、`v4.7`、`v4.7.1`、`v4.7.2`、および `v4.8` です。

```xml
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
```

 *目標一覧表* はターゲット フレームワークのサブセットです。 たとえば、.NET Framework 4 Client Profile には、MSBuild アセンブリへの参照が含まれていません。

 > [!NOTE]
 > ターゲット プロファイルは、[ポータブル クラス ライブラリ](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)にのみ適用されます。

 ターゲット プロファイルは、プロジェクト ファイルの `TargetFrameworkProfile` プロパティで指定されます。 目標一覧表を変更するには、IDE でプロジェクトのプロパティ ページにあるターゲット フレームワークのコントロールを使用します。

```xml
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
<TargetFrameworkProfile>Client</TargetFrameworkProfile>
```

## <a name="target-platform"></a>ターゲット プラットフォーム

 *プラットフォーム* は、特定のランタイム環境を定義するハードウェアとソフトウェアの組み合わせです。 たとえば、オブジェクトに適用された

- `x86` は、Intel 80x86 プロセッサまたはそれに相当するプロセッサで実行されている 32 ビット Windows オペレーティング システムを示しています。

- `x64` は、Intel x64 プロセッサまたはそれに相当するプロセッサで実行されている 64 ビット Windows オペレーティング システムを示しています。

- `Xbox` は、Microsoft Xbox 360 プラットフォームを示しています。

*ターゲット プラットフォーム* は、ビルドするプロジェクトの実行対象となる特定のプラットフォームです。 ターゲット プラットフォームは、プロジェクト ファイルの `PlatformTarget` ビルド プロパティで指定されます。 ターゲット プラットフォームを変更するには、IDE でプロジェクトのプロパティ ページまたは **[構成マネージャー]** を使用します。

```xml
<PropertyGroup>
   <PlatformTarget>x86</PlatformTarget>
</PropertyGroup>

```

*ターゲット構成* はターゲット プラットフォームのサブセットです。 たとえば、`x86` `Debug` 構成には、ほとんどのコード最適化が含まれていません。 ターゲット構成は、プロジェクト ファイルの `Configuration` ビルド プロパティで指定されます。 ターゲット構成を変更するには、プロジェクトのプロパティ ページまたは **[構成マネージャー]** を使用します。

```xml
<PropertyGroup>
   <PlatformTarget>x86</PlatformTarget>
   <Configuration>Debug</Configuration>
</PropertyGroup>

```

## <a name="see-also"></a>関連項目

- [マルチ ターゲット](../msbuild/msbuild-multitargeting-overview.md)
