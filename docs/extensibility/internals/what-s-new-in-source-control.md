---
title: Visual Studio 2015 SDK のソース管理の新機能 |マイクロソフトドキュメント
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f90ae3e1d327b10e99713ad28aa2d5a06c0be34b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703409"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK のソース管理の新機能

[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]では、ソース管理 VSPackage を実装することで、深く統合されたソース管理ソリューションを提供できます。 このセクションでは、ソース管理 VSPackages の機能について説明し、実装手順の概要を示します。

## <a name="the-source-control-vspackage"></a>ソース管理 VS パッケージ

Visual Studio では、2 種類のソース管理ソリューションがサポートされています。 Visual Studio のすべてのバージョンでは、ソース管理プラグイン API ベースのプラグインを統合できます。 高度な高度化と自律性を必要とするソース管理ソリューションに適した、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]深い統合パスを提供するソース管理用の VSPackage を作成することもできます。

VSPackage は、ほとんどすべての種類の機能を Visual Studio に追加できます。 ソース管理 VSPackage は、ユーザーに提示された UI からソース管理システムとのバックエンド通信まで、Visual Studio の完全なソース管理機能を提供します。

ソース管理 VSPackage を実装するには、"すべてまたは何も" 戦略が必要です。 ソース管理 VSPackage の作成者は、ソース管理の機能全体だけでなく、Visual Studio との統合に必要なインターフェイスをカバーするソース管理インターフェイスと新しい UI 要素 (ダイアログ ボックス、メニュー、およびツール バー) の数を実装する際に、かなりの労力を投資する必要があります。

次の手順では、ソース管理パッケージを実装するために必要な内容の概要を示します。 詳細については、「[ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)」を参照してください。

1. プライベート ソース管理サービスを提供する VSPackage を作成します。

2. Visual Studio によって提供されるソース管理関連のサービス (および インターフェイスなど) に<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>実装します。

3. ソース管理の VSPackage を登録します。

4. メニュー項目、ダイアログ ボックス、ツールバー、コンテキスト メニューなど、すべてのソース管理 UI を実装します。

5. ソース管理関連のすべてのイベントは、アクティブな場合にソース管理 VSackage に渡され、VSPackage によって処理される必要があります。

6. ソース管理の VSPackage は<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>、インターフェイスを実装するイベントや (インターフェイスによって実装される) プロジェクト ドキュメント (TPD)<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>イベントの追跡などのイベントをリッスンし、必要なアクションを実行する必要があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概要](../../extensibility/internals/source-control-integration-overview.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
