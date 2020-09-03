---
title: VSPackage 構造体 (ソース管理 VSPackage) |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80703807"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 構造 (ソース管理 VSPackage)

ソース管理パッケージ SDK は、ソース管理の実装者がソース管理機能を Visual Studio 環境と統合できるようにする VSPackage を作成するためのガイドラインを提供します。 VSPackage は、通常、レジストリエントリでパッケージによって提供されるサービスに基づいて、Visual Studio 統合開発環境 (IDE) によってオンデマンドで読み込まれる COM コンポーネントです。 すべての VSPackage はを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> ます。 VSPackage は、通常、Visual Studio IDE によって提供されるサービスを使用し、独自のサービスを提供します。

VSPackage は、そのメニュー項目を宣言し、vsct ファイルを介して既定の項目の状態を確立します。 Visual Studio IDE では、VSPackage が読み込まれるまで、この状態のメニュー項目が表示されます。 その後、VSPackage のメソッドの実装を呼び出して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メニュー項目を有効または無効にします。

## <a name="source-control-package-characteristics"></a>ソース管理パッケージの特性

ソース管理 VSPackage は、Visual Studio に緊密に統合されています。 VSPackage セマンティクスは次のとおりです。

- VSPackage (インターフェイス) であることによって実装されるインターフェイス `IVsPackage`

- UI コマンドの実装 (vsct ファイルとインターフェイスの実装 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> )

- VSPackage を Visual Studio に登録します。

ソース管理 VSPackage は、次のような他の Visual Studio エンティティと通信する必要があります。

- プロジェクト

- エディター

- ソリューション

- Windows

- 実行中のドキュメントテーブル

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>使用可能な Visual Studio 環境サービス

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

SVsRegisterScciProvider サービス

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>実装および呼び出される VSIP インターフェイス

ソース管理パッケージは VSPackage であるため、Visual Studio に登録されている他の Vspackage と直接やり取りできます。 ソース管理機能を最大限に活用するために、ソース管理 VSPackage は、プロジェクトまたはシェルによって提供されるインターフェイスを扱うことができます。

Visual studio のすべてのプロジェクトは <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> 、Visual STUDIO IDE 内でプロジェクトとして認識されるようにを実装する必要があります。 ただし、このインターフェイスは、ソース管理には特に特殊化されていません。 ソース管理下にあると予想されるプロジェクトは、を実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> します。 このインターフェイスは、ソース管理 VSPackage によって使用されます。このインターフェイスは、プロジェクトのコンテンツを照会し、そのコンテンツ (サーバーの場所とソース管理下にあるプロジェクトのディスクの場所との間の接続を確立するために必要な情報) を提供します。

ソース管理 VSPackage はを実装します <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 。これにより、プロジェクトはソース管理のために自身を登録し、状態のグリフを取得できます。

ソース管理 VSPackage で考慮する必要があるインターフェイスの完全な一覧については、「 [関連するサービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
