---
title: Visual Studio のワークロードとコンポーネント ID
titleSuffix: ''
description: ワークロード ID とコンポーネント ID を使用して、コマンドラインを使用して Visual Studio をインストールするか、VSIX マニフェストで依存関係として指定します。
keywords: ''
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.date: 09/23/2019
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.custom: seodec18
ms.assetid: 34e19ef1-abfb-44fd-aad2-33c5d7874482
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 05a5a1cb55356dbdd0d0d0127793abbd2e73e109
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114154"
---
# <a name="visual-studio-workload-and-component-ids"></a>Visual Studio のワークロードとコンポーネント ID

コマンド ラインを使用して Visual Studio をインストールする場合や、VSIX マニフェストで依存関係として指定する場合に必要となる使用可能なワークロードとコンポーネント ID を表示するには、以下の表のエディション名をクリックします。

::: moniker range="vs-2017"

**[15.9 リリース](/visualstudio/releasenotes/vs2017-relnotes/)の更新**

| **エディション** | **ID** | **説明** |
| ----------- | ------ | --------------- |
| [Visual&nbsp;Studio Enterprise&nbsp;2017](workload-component-id-vs-enterprise.md?vs-2017) | Microsoft.VisualStudio.Product.Enterprise | 任意の規模のチームにわたって生産性を高め調整を容易にする Microsoft DevOps ソリューションです。 |
| [Visual&nbsp;Studio Professional&nbsp;2017](workload-component-id-vs-professional.md?vs-2017) | Microsoft.VisualStudio.Product.Professional | 小規模なチームを対象としたプロフェッショナル開発者用ツールとサービスです。 |
| [Visual&nbsp;Studio Community&nbsp;2017](workload-component-id-vs-community.md) | Microsoft.VisualStudio.Product.Community | 学生、オープン ソース、個人の開発者向けの無料でフル機能の IDE です。 |
| [Visual&nbsp;Studio Team&nbsp;Explorer&nbsp;2017](workload-component-id-vs-team-explorer.md?vs-2017) | Microsoft.VisualStudio.Product.TeamExplorer | Visual Studio 開発者向けツールなしで Team Foundation Server および Azure DevOps Services を操作できます。 |
| [Visual Studio Desktop Express 2017](workload-component-id-vs-express.md?vs-2017) | Microsoft.VisualStudio.Product.WDExpress | 構文認識コード編集、ソース コード管理、作業項目管理を備える WPF、WinForms、Win32 などのネイティブおよびマネージド アプリケーションのビルド。 C#、Visual Basic、Visual C++ のサポートが含まれます。 |
| [Visual&nbsp;Studio Build&nbsp;Tools&nbsp;2017](workload-component-id-vs-build-tools.md?vs-2017) | Microsoft.VisualStudio.Product.BuildTools | Visual Studio Build Tools を使用すると、Visual Studio IDE を必要とせずに、MSBuild ベースのネイティブおよびマネージド アプリケーションをビルドできます。 Visual C++ コンパイラやライブラリ、MFC、ATL、C++/CLI サポートをインストールするオプションもあります。 |
| [Visual&nbsp;Studio Test&nbsp;Agent&nbsp;2017](workload-component-id-vs-test-agent.md?vs-2017)  | Microsoft.VisualStudio.Product.TestAgent | 自動テストとロード テストのリモートでの実行をサポートします。 |
| [Visual&nbsp;Studio Test&nbsp;Controller 2017](workload-component-id-vs-test-controller.md?vs-2017) | Microsoft.VisualStudio.Product.TestController | 複数のマシンに自動テストを配布します |
| [Visual&nbsp;Studio Test&nbsp;Professional&nbsp;2017](workload-component-id-vs-test-professional.md?vs-2017) | Microsoft.VisualStudio.Product.TestProfessional | Visual Studio Test Professional 2017 |
| [Visual&nbsp;Studio Feedback&nbsp;Client&nbsp;2017](workload-component-id-vs-feedback-client.md?vs-2017) | Microsoft.VisualStudio.Product.FeedbackClient | Visual Studio Feedback Client 2017 |

これらの ID の使用方法の詳細については、「[Use Command-Line Parameters to Install Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md?view=vs-2017)」(コマンドライン パラメーターを使用して Visual Studio 2017 をインストールする) ページと「[方法:機能拡張プロジェクトを Visual Studio 2017 に移行](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md?view=vs-2017)」ページを参照してください。

::: moniker-end

::: moniker range="vs-2019"

**[16.3 リリース](/visualstudio/releases/2019/release-notes/)の更新**

| **エディション** | **ID** | **説明** |
| ----------- | ------ | --------------- |
| [Visual&nbsp;Studio Enterprise&nbsp;2019](workload-component-id-vs-enterprise.md?vs-2019) | Microsoft.VisualStudio.Product.Enterprise | 任意の規模のチームにわたって生産性を高め調整を容易にする Microsoft DevOps ソリューションです。 |
| [Visual&nbsp;Studio Professional&nbsp;2019](workload-component-id-vs-professional.md?vs-2019) | Microsoft.VisualStudio.Product.Professional | 小規模なチームを対象としたプロフェッショナル開発者用ツールとサービスです。 |
| [Visual&nbsp;Studio Community&nbsp;2019](workload-component-id-vs-community.md?vs-2019) | Microsoft.VisualStudio.Product.Community | 学生、オープン ソース、個人の開発者向けの無料でフル機能の IDE です。 |
| [Visual&nbsp;Studio Team&nbsp;Explorer&nbsp;2019](workload-component-id-vs-team-explorer.md?vs-2019) | Microsoft.VisualStudio.Product.TeamExplorer | Visual Studio 開発者向けツールなしで Team Foundation Server および Azure DevOps Services を操作できます。 |
| [Visual&nbsp;Studio Build&nbsp;Tools&nbsp;2019](workload-component-id-vs-build-tools.md?vs-2019) | Microsoft.VisualStudio.Product.BuildTools | Visual Studio Build Tools を使用すると、Visual Studio IDE を必要とせずに、MSBuild ベースのネイティブおよびマネージド アプリケーションをビルドできます。 Visual C++ コンパイラやライブラリ、MFC、ATL、C++/CLI サポートをインストールするオプションもあります。 |
| [Visual&nbsp;Studio Test&nbsp;Agent&nbsp;2019](workload-component-id-vs-test-agent.md?vs-2019)  | Microsoft.VisualStudio.Product.TestAgent | 自動テストとロード テストのリモートでの実行をサポートします。 |
| [Visual&nbsp;Studio Load&nbsp;Test&nbsp;Controller 2019](workload-component-id-vs-test-controller.md?vs-2019) | Microsoft.VisualStudio.Product.TestController | 複数のマシンに自動テストを配布します |

これらの ID の使用方法の詳細については、「[Use Command-Line Parameters to Install Visual Studio](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019)」(コマンドライン パラメーターを使用して Visual Studio をインストールする) ページと[方法:機能拡張プロジェクトの Visual Studio への移行](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md?view=vs-2019)に関するページも参照してください。

> [!NOTE]
> 以前のバージョンのワークロードおよびコンポーネントの一覧については、[Visual Studio 2017 のワークロードおよびコンポーネント ID](workload-and-component-ids.md?view=vs-2017) に関するページを参照してください。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio の管理者ガイド](visual-studio-administrator-guide.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
  * [コマンド ライン パラメーターの例](command-line-parameter-examples.md)
* [Visual Studio のオフライン インストールを作成する](create-an-offline-installation-of-visual-studio.md)
