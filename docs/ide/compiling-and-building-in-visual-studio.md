---
title: コンパイルとビルド
ms.date: 07/14/2017
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- builds [Visual Studio], about building in Visual Studio
- custom build steps, types of builds
ms.assetid: c7958821-285f-4e28-9e7a-b5d8b40336a1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 38d583553c0382598681ab3aa52ca3a41a27ed2c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585497"
---
# <a name="compile-and-build-in-visual-studio"></a>Visual Studio でのコンパイルとビルド

ソース コードをビルドすると、ビルド エンジンによってアセンブリと実行可能アプリケーションが作成されます。 基本的に、ビルド プロセスはどのプロジェクト タイプでも (Windows、ASP.NET、モバイル アプリなど)、よく似ています。 同様に、どのプログラミング言語でも (C#、Visual Basic、C++、F# など) ビルド プロセスは似ています。

コードを何度もビルドすることによって、構文の誤り、キーワードのスペルミス、型の不一致などのコンパイル時エラーをすばやく特定できます。 また、コードのデバッグ バージョンをビルドして実行することにより、ロジック エラーやセマンティック エラーなどの実行時エラーを検出して修正できます。

ビルドの成功とは、アプリケーションのソース コードの構文が正しいことと、ライブラリやアセンブリなどのコンポーネントへの静的参照をすべて解決できることの確認です。 アプリケーション実行可能ファイルが生成されます。[デバッグ環境](../debugger/index.yml)だけでなく、手動と自動のさまざまなテストを通して[コードの品質を検証](../test/improve-code-quality.md)して、正しく機能することをテストできます。 アプリケーションのテストが完了したら、リリース バージョンをコンパイルしてユーザーにリリースします。 このプロセスの入門資料については、「[チュートリアル:アプリケーションをビルドする](../ide/walkthrough-building-an-application.md)」を参照してください。

Visual Studio IDE、MSBuild コマンド ライン ツール、Azure Pipelines のいずれかの方法を使用して、アプリケーションをビルドすることができます。

| ビルド方法 | 利点 |
| --- |--- | --- |
| IDE |- ビルドを即座に作成してデバッガーでテストできます。<br />- マルチプロセッサ ビルドを実行します (C++ や C# のプロジェクトの場合)。<br />- ビルド システムのさまざまな面をカスタマイズできます。 |
| MSBuild コマンドライン| - Visual Studio をインストールせずにプロジェクトをビルドできます。<br />- すべてのプロジェクト タイプでマルチ プロセッサ ビルドを実行できます。<br />- ビルド システムのほとんどの部分をカスタマイズできます。|
| Azure Pipelines | - ビルド プロセスを継続的インテグレーション/継続的デリバリー パイプラインの一部として自動化できます。<br />- 自動テストをすべてのビルドに適用します。<br />- クラウド ベースのリソースをほぼ無制限にビルド プロセスに使用できます。<br />- ビルド ワークフローの変更やビルド アクティビティの作成が可能です。実行するタスクを大幅にカスタマイズできます。|

このセクションでは、IDE ベースのビルド プロセスを詳しく解説します。 他の方法の詳細については、「[MSBuild](../msbuild/msbuild.md)」と「[Azure Pipelines](/azure/devops/pipelines/index?view=vsts)」をそれぞれ参照してください。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[Visual Studio for Mac のコンパイルとビルド](/visualstudio/mac/compiling-and-building)」を参照してください。

## <a name="overview-of-building-from-the-ide"></a>IDE でのビルドの概要

Visual Studio でプロジェクトを作成すると、そのプロジェクトとプロジェクトが属するソリューションのための、既定のビルド構成が作成されます。  この構成は、ソリューションとプロジェクトをどのようにビルドして配置するかを定義するものです。 このうち、プロジェクト構成はターゲット プラットフォーム (たとえば Windows または Linux) とビルドの種類 (たとえばデバッグまたはリリース) ごとに固有です。 これらの構成は自由に編集でき、必要に応じて独自の構成を作成することもできます。

IDE の中でのビルド方法の入門資料については、「[チュートリアル:アプリケーションをビルドする](walkthrough-building-an-application.md)」を参照してください。

次に、「[Visual Studio でのプロジェクトとソリューションのビルドおよびクリーン](building-and-cleaning-projects-and-solutions-in-visual-studio.md)」を参照して、このプロセスに関してどのようなカスタマイズが可能かを把握してください。 カスタマイズの例としては、[出力ディレクトリの変更](how-to-change-the-build-output-directory.md)、[カスタム ビルド イベントの指定](specifying-custom-build-events-in-visual-studio.md)、[プロジェクト依存関係の管理](how-to-create-and-remove-project-dependencies.md)、[ビルド ログ ファイルの管理](how-to-view-save-and-configure-build-log-files.md)、[コンパイラ警告の抑制](how-to-suppress-compiler-warnings.md)などがあります。

その他に、次のようなタスクに関する情報も参照してください。
- [ビルド構成について](understanding-build-configurations.md)
- [ビルド プラットフォームについて](understanding-build-platforms.md)
- [プロジェクトおよびソリューションのプロパティの管理](managing-project-and-solution-properties.md)
- ビルド イベントの指定 ([C#](how-to-specify-build-events-csharp.md)、[Visual Basic](how-to-specify-build-events-visual-basic.md))
- [ビルド オプションの設定](reference/options-dialog-box-projects-and-solutions-build-and-run.md)
- [複数プロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)

## <a name="see-also"></a>関連項目

- [Web サイト プロジェクトのビルド (コンパイル)](https://msdn.microsoft.com/Library/a9cbb88c-8fff-4c67-848b-98fbfd823193)
- [コンパイルとビルド (Visual Studio for Mac)](/visualstudio/mac/compiling-and-building)
