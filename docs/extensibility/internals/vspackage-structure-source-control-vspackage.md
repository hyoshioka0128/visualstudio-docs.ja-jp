---
title: VS パッケージ構造 (ソース管理 VS パッケージ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b3f09b189e1e4b47187586e66c74315ee32495c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703807"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 構造 (ソース管理 VSPackage)

ソース管理パッケージ SDK では、ソース管理の実装者が Visual Studio 環境とソース管理機能を統合できるようにする VSPackage を作成するためのガイドラインを提供します。 VSPackage は、通常、Visual Studio 統合開発環境 (IDE) によって要求に応じて読み込まれる COM コンポーネントです。 すべての VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>は、 を実装する必要があります。 VSPackage は通常、Visual Studio IDE によって提供されるサービスを使用し、独自のサービスを提供します。

VSPackage は、そのメニュー項目を宣言し、.vsct ファイルを使用して既定の項目の状態を確立します。 VSPackage が読み込まれるまで、この状態でメニュー項目が表示されます。 その後、VSPackage の<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>メソッドの実装が呼び出され、メニュー項目を有効または無効にします。

## <a name="source-control-package-characteristics"></a>ソース管理パッケージの特性

ソース管理 VSPackage は、Visual Studio に深く統合されています。 VSPackage のセマンティクスには次のものがあります。

- VSPackage (インターフェイス) であることによって実装される`IVsPackage`インターフェイス

- UI コマンドの実装 (.vsct ファイル<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>とインターフェイスの実装)

- VS パッケージの登録を Visual Studio で行います。

ソース管理 VSPackage は、これらの他の Visual Studio エンティティと通信する必要があります。

- プロジェクト

- エディター

- ソリューション

- Windows

- 実行中のドキュメント テーブル

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>使用される可能性のある Visual Studio 環境サービス

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

サービスを提供します。

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>VSIP インターフェイスの実装と呼び出し

ソース管理パッケージは VSPackage であるため、Visual Studio に登録されている他の VSPackage と直接やり取りできます。 ソース管理の機能の完全な幅を提供するために、ソース管理 VSPackage プロジェクトまたはシェルによって提供されるインターフェイスを処理できます。

Visual Studio のすべてのプロジェクトは<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>、Visual Studio IDE 内のプロジェクトとして認識されるように実装する必要があります。 ただし、このインターフェイスはソース管理に十分な特殊化されていません。 ソース管理下にあると予想されるプロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>を実装します。 このインターフェイスは、ソース管理 VSPackage によって、その内容のプロジェクトを照会し、グリフとバインディング情報 (サーバーの場所とソース管理下にあるプロジェクトのディスクの場所との間の接続を確立するために必要な情報) を提供するために使用されます。

ソース管理の VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>は、ソース管理のために自分自身を登録し、その状態のグリフを取得するプロジェクトを実装します。

ソース管理 VSPackage で考慮する必要があるインターフェイスの完全な一覧については、「[関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
