---
title: Visual Studio 2015 SDK のソース管理の新機能 |Microsoft Docs
description: ソース管理 Vspackage の機能について説明し、実装手順の概要を確認します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a7df9af8dbd4af708483b638c0a86470a7d2220
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940047"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK のソース管理の新機能

では、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ソース管理 VSPackage を実装することで、緊密に統合されたソース管理ソリューションを提供できます。 ここでは、ソース管理 Vspackage の機能について説明し、実装手順の概要を示します。

## <a name="the-source-control-vspackage"></a>ソース管理 VSPackage

Visual Studio では、2種類のソース管理ソリューションがサポートされています。 Visual Studio のすべてのバージョンで、ソース管理プラグイン API ベースのプラグインを統合できます。 また、高度な統合を提供し、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 高度なレベルと自律性を必要とするソース管理ソリューションに適したパスを提供する、ソース管理用の VSPackage を作成することもできます。

VSPackage を使用すると、ほぼすべての種類の機能を Visual Studio に追加できます。 ソース管理 VSPackage は、ユーザーに表示される UI からソース管理システムとのバックエンド通信まで、Visual Studio の完全なソース管理機能を提供します。

ソース管理 VSPackage を実装するには、"すべて" または "なし" の戦略が必要です。 ソース管理 VSPackage の作成者は、ソース管理インターフェイスと新しい UI 要素 (ダイアログボックス、メニュー、およびツールバー) を実装するために多くの労力を費やす必要があります。これに加えて、Visual Studio に正常に統合するために必要なインターフェイスだけでなく、ソース管理機能全体に対応できます。

次の手順では、ソース管理パッケージを実装するために必要な作業の概要を説明します。 詳細については、「 [ソース管理の作成 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)」を参照してください。

1. プライベートソース管理サービスを作成する VSPackage を作成します。

2. Visual Studio によって proffered されるソース管理関連サービス (やインターフェイスなど) にインターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> ます。

3. ソース管理 VSPackage を登録します。

4. メニュー項目、ダイアログボックス、ツールバー、およびコンテキストメニューを含む、すべてのソース管理 UI を実装します。

5. ソース管理に関連するすべてのイベントは、アクティブであり、VSPackage によって処理される必要がある場合に、ソース管理 VSackage に渡されます。

6. ソース管理 VSPackage は、インターフェイスを実装するイベント <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> や、(インターフェイスによって実装される) プロジェクトドキュメント (TPD) イベントを追跡し、必要なアクションを実行するなどのイベントをリッスンする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> ます。

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概要](../../extensibility/internals/source-control-integration-overview.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
