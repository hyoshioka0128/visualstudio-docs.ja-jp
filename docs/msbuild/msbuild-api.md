---
title: MSBuild API | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e87ee95c4027d0513c78d3ce0386cf31d47baf94
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862684"
---
# <a name="use-the-msbuild-api"></a>MSBuild API を使用する

MSBuild は、プログラムがビルドを実行してプロジェクトを検査できるように、パブリック API サーフェスを提供します。 最新バージョンの MSBuild API は、次の NuGet パッケージで見つけることができます。

| パッケージ名 | 説明 |
| ------------ | ----------- |
| [Microsoft.Build](https://www.nuget.org/packages/Microsoft.Build) | MSBuild プロジェクトの作成、編集、評価に使用される、Microsoft.Build アセンブリが含まれています。|
| [Microsoft.Build.Framework](https://www.nuget.org/packages/Microsoft.Build.Framework)| 他の MSBuild アセンブリによって使用される、共通の MSBuild フレームワーク アセンブリが含まれています。 |
| [Microsoft.Build.Runtime](https://www.nuget.org/packages/Microsoft.Build.Runtime) | MSBuild の完全な実行可能ファイルのコピーを提供します。 このパッケージは、MSBuild のインストールを必要とすることなく、アプリケーションでプロジェクトを読み込んだり、インプロセス ビルドを実行したりする必要がある場合にのみ参照してください。 このパッケージを使用してプロジェクトを評価するには、追加のコンポーネント (コンパイラなど) をアプリケーション ディレクトリに集約する必要があります。 |
| [Microsoft.Build.Tasks.Core](https://www.nuget.org/packages/Microsoft.Build.Tasks.Core) | MSBuild の一般的に使用されるタスクを実装する、Microsoft.Build.Tasks アセンブリが含まれています。 |
| [Microsoft.Build.Utilities.Core](https://www.nuget.org/packages/Microsoft.Build.Utilities.Core) | カスタム MSBuild タスクを実装するために使用される、Microsoft.Build.Utilities アセンブリが含まれています。 |

さらに、NuGet ではレガシ アセンブリの [Microsoft.Build.Engine](https://www.nuget.org/packages/Microsoft.Build.Engine) もホストしています。これは非推奨とされています。

MSBuild API にはいくつかの異なるバージョンがあります。バージョン 15 と 16 では、NuGet パッケージ内に異なる形式のアセンブリが 2 つあります。1 つは .NET Framework でコンパイルされ、もう 1 つは .NET Framework API サーフェスのサブセットである .NET Core でコンパイルされたものです。  .NET Core バージョンの MSBuild は、`dotnet` コマンドを呼び出すとき、Mac および Linux システムで MSBuild を使用するときに使用されます。

MSBuild API のドキュメントは、[.NET API ブラウザー](/dotnet/api)を使用するか、次の一覧の名前空間を参照することによって見つけることができます。

::: moniker range="vs-2017"
| 名前空間 | 対象 | 説明 |
|-----------| -----------| ----------- |
| [Microsoft.Build.Construction](/dotnet/api/Microsoft.Build.Construction?view=msbuild-15&preserve-view=true) | すべて |  評価されていない値を使ってプロジェクト ルートを構築するために、MSBuild オブジェクト モデルによって使用される型が含まれています。 各プロジェクト ルートは、プロジェクトまたはターゲット ファイルに対応します。 |
| [Microsoft.Build.Definition](/dotnet/api/Microsoft.Build.Definition?view=msbuild-15&preserve-view=true) | すべて | プロジェクトの構築をサポートする `ProjectOptions` クラスが含まれています。 |
| [Microsoft.Build.Evaluation](/dotnet/api/Microsoft.Build.Evaluation?view=msbuild-15&preserve-view=true) | すべて | プロジェクトを評価するために、MSBuild オブジェクト モデルによって使用される型が含まれています。 各プロジェクトは、1 つまたは複数のプロジェクト ルートに関連付けられています。 |
| [Microsoft.Build.Evaluation.Context](/dotnet/api/Microsoft.Build.Evaluation.Context?view=msbuild-15&preserve-view=true) | すべて | 呼び出し全体で評価状態を格納するために使用される `EvaluationContext` クラスが含まれています。 |
| [Microsoft.Build.Exceptions](/dotnet/api/Microsoft.Build.Exceptions?view=msbuild-15&preserve-view=true) | すべて | ビルド プロセス中にスローされる可能性がある例外の種類が含まれています。 |
| [Microsoft.Build.Execution](/dotnet/api/Microsoft.Build.Execution?view=msbuild-15&preserve-view=true) | すべて | プロジェクトをビルドするために、MSBuild オブジェクト モデルによって使用される型が含まれています。 |
| [Microsoft.Build.Framework](/dotnet/api/Microsoft.Build.Framework?view=msbuild-15&preserve-view=true) | すべて | タスクおよびロガーから MSBuild エンジンとやりとりする方法を定義する型が含まれています。|
| [Microsoft.Build.Framework.Profiler](/dotnet/api/Microsoft.Build.Framework.Profiler?view=msbuild-15&preserve-view=true) | すべて | パフォーマンス プロファイルをサポートする型が含まれています。 |
| [Microsoft.Build.Framework.XamlTypes](/dotnet/api/Microsoft.Build.Framework.XamlTypes?view=msbuild-15&preserve-view=true) | .NET Framework のみ | ファイル、ルール、その他のソースから解析された XAML 型を表すために使用されるクラスが含まれています。 |
| [Microsoft.Build.Globbing](/dotnet/api/Microsoft.Build.Globbing?view=msbuild-15&preserve-view=true) | すべて | ワイルドカードの処理をサポートするクラスが含まれています。 |
| [Microsoft.Build.Globbing.Extensions](/dotnet/api/Microsoft.Build.Globbing.Extensions?view=msbuild-15&preserve-view=true) | すべて | ワイルドカードの処理に対する拡張機能をサポートする型が含まれています。 |
| [Microsoft.Build.Graph](/dotnet/api/Microsoft.Build.Graph?view=msbuild-15&preserve-view=true) | すべて | `-graph` MSBuild スイッチをサポートする型が含まれています。 |
| [Microsoft.Build.Logging](/dotnet/api/Microsoft.Build.Logging?view=msbuild-15&preserve-view=true) | すべて | ビルドの進行状況のログに記録するために使用される型が含まれています。 |
| [Microsoft.Build.ObjectModelRemoting](/dotnet/api/Microsoft.Build.ObjectModelRemoting?view=msbuild-15&preserve-view=true) | すべて | MSBuild でのリモート処理をサポートする型が含まれています。 |
| [Microsoft.Build.Tasks](/dotnet/api/Microsoft.Build.Tasks?view=msbuild-15&preserve-view=true) | すべて | MSBuild に付属するすべてのタスクの実装が含まれています。 |
| [Microsoft.Build.Tasks.Deployment.Bootstrapper](/dotnet/api/Microsoft.Build.Tasks.Deployment.Bootstrapper?view=msbuild-15&preserve-view=true) | .NET Framework のみ | MSBuild によって内部的に使用されるクラスが含まれています。 |
| [Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/Microsoft.Build.Tasks.Deployment.ManifestUtilities?view=msbuild-15&preserve-view=true) | .NET Framework のみ | MSBuild によって使用されるクラスが含まれています。|
| [Microsoft.Build.Tasks.Hosting](/dotnet/api/Microsoft.Build.Tasks.Hosting?view=msbuild-15&preserve-view=true) | すべて | MSBuild によって内部的に使用されるクラスが含まれています。 |
| [Microsoft.Build.Tasks.Xaml](/dotnet/api/Microsoft.Build.Tasks.Xaml?view=msbuild-15&preserve-view=true) | .NET Framework のみ | XAML ビルド タスクに関連するクラスが含まれています。 |
| [Microsoft.Build.Utilities](/dotnet/api/Microsoft.Build.Utilities?view=msbuild-15&preserve-view=true) | すべて | 独自の MSBuild のロガーとタスクを作成するために使用できるヘルパー クラスが含まれています。|
:::moniker-end
:::moniker range=">=vs-2019"
| 名前空間 | 対象 | 説明 |
|-----------| -----------| ----------- |
| [Microsoft.Build.Construction](/dotnet/api/Microsoft.Build.Construction?view=msbuild-16&preserve-view=true) | すべて |  評価されていない値を使ってプロジェクト ルートを構築するために、MSBuild オブジェクト モデルによって使用される型が含まれています。 各プロジェクト ルートは、プロジェクトまたはターゲット ファイルに対応します。 |
| [Microsoft.Build.Definition](/dotnet/api/Microsoft.Build.Definition?view=msbuild-16&preserve-view=true) | すべて | プロジェクトの構築をサポートする `ProjectOptions` クラスが含まれています。 |
| [Microsoft.Build.Evaluation](/dotnet/api/Microsoft.Build.Evaluation?view=msbuild-16&preserve-view=true) | すべて | プロジェクトを評価するために、MSBuild オブジェクト モデルによって使用される型が含まれています。 各プロジェクトは、1 つまたは複数のプロジェクト ルートに関連付けられています。 |
| [Microsoft.Build.Evaluation.Context](/dotnet/api/Microsoft.Build.Evaluation.Context?view=msbuild-16&preserve-view=true) | すべて | 呼び出し全体で評価状態を格納するために使用される `EvaluationContext` クラスが含まれています。 |
| [Microsoft.Build.Exceptions](/dotnet/api/Microsoft.Build.Exceptions?view=msbuild-16&preserve-view=true) | すべて | ビルド プロセス中にスローされる可能性がある例外の種類が含まれています。 |
| [Microsoft.Build.Execution](/dotnet/api/Microsoft.Build.Execution?view=msbuild-16&preserve-view=true) | すべて | プロジェクトをビルドするために、MSBuild オブジェクト モデルによって使用される型が含まれています。 |
| [Microsoft.Build.Framework](/dotnet/api/Microsoft.Build.Framework?view=msbuild-16&preserve-view=true) | すべて | タスクおよびロガーから MSBuild エンジンとやりとりする方法を定義する型が含まれています。|
| [Microsoft.Build.Framework.Profiler](/dotnet/api/Microsoft.Build.Framework.Profiler?view=msbuild-16&preserve-view=true) | すべて | パフォーマンス プロファイルをサポートする型が含まれています。 |
| [Microsoft.Build.Framework.XamlTypes](/dotnet/api/Microsoft.Build.Framework.XamlTypes?view=msbuild-16&preserve-view=true) | .NET Framework のみ | ファイル、ルール、その他のソースから解析された XAML 型を表すために使用されるクラスが含まれています。 |
| [Microsoft.Build.Globbing](/dotnet/api/Microsoft.Build.Globbing?view=msbuild-16&preserve-view=true) | すべて | ワイルドカードの処理をサポートするクラスが含まれています。 |
| [Microsoft.Build.Globbing.Extensions](/dotnet/api/Microsoft.Build.Globbing.Extensions?view=msbuild-16&preserve-view=true) | すべて | ワイルドカードの処理に対する拡張機能をサポートする型が含まれています。 |
| [Microsoft.Build.Graph](/dotnet/api/Microsoft.Build.Graph?view=msbuild-16&preserve-view=true) | すべて | `-graph` MSBuild スイッチをサポートする型が含まれています。 |
| [Microsoft.Build.Logging](/dotnet/api/Microsoft.Build.Logging?view=msbuild-16&preserve-view=true) | すべて | ビルドの進行状況のログに記録するために使用される型が含まれています。 |
| [Microsoft.Build.ObjectModelRemoting](/dotnet/api/Microsoft.Build.ObjectModelRemoting?view=msbuild-16&preserve-view=true) | すべて | MSBuild でのリモート処理をサポートする型が含まれています。 |
| [Microsoft.Build.Tasks](/dotnet/api/Microsoft.Build.Tasks?view=msbuild-16&preserve-view=true) | すべて | MSBuild に付属するすべてのタスクの実装が含まれています。 |
| [Microsoft.Build.Tasks.Deployment.Bootstrapper](/dotnet/api/Microsoft.Build.Tasks.Deployment.Bootstrapper?view=msbuild-16&preserve-view=true) | .NET Framework のみ | MSBuild によって内部的に使用されるクラスが含まれています。 |
| [Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/Microsoft.Build.Tasks.Deployment.ManifestUtilities?view=msbuild-16&preserve-view=true) | .NET Framework のみ | MSBuild によって使用されるクラスが含まれています。|
| [Microsoft.Build.Tasks.Hosting](/dotnet/api/Microsoft.Build.Tasks.Hosting?view=msbuild-16&preserve-view=true) | すべて | MSBuild によって内部的に使用されるクラスが含まれています。 |
| [Microsoft.Build.Tasks.Xaml](/dotnet/api/Microsoft.Build.Tasks.Xaml?view=msbuild-16&preserve-view=true) | .NET Framework のみ | XAML ビルド タスクに関連するクラスが含まれています。 |
| [Microsoft.Build.Utilities](/dotnet/api/Microsoft.Build.Utilities?view=msbuild-16&preserve-view=true) | すべて | 独自の MSBuild のロガーとタスクを作成するために使用できるヘルパー クラスが含まれています。|
:::moniker-end

前の表の "対象" 列にある "すべて" は、MSBuild API の .NET Framework と .NET Core の両方のバージョンで名前空間の型を使用できることを意味します。
