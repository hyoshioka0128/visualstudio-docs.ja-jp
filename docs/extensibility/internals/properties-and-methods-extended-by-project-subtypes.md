---
title: プロジェクト サブタイプによって拡張されるプロパティとメソッド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9963f779055fcf1ed0efd8c47abbe1cce35631a6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706193"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>プロジェクト サブタイプによって拡張されるプロパティとメソッド
プロジェクトのサブタイプは、基本プロジェクトのアグリゲータとして構築されるため、プロジェクトの動作に影響を与える大きな力を持ちます。 このセクションでは、プロジェクトのサブタイプによって強化または変更できる機能の一部について説明します。

## <a name="features-gained-by-aggregation"></a>集約によって得られる機能
 次の表は、集計によってプロジェクトのサブタイプを基本プロジェクトでオーバーライドできるメソッドの多くを要約したものです。

|集計によってオーバーライドされるメソッド|プロジェクトのサブタイプ|
|---------------------------------------|---------------------|
|から<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|プロジェクトのサブタイプを有効にします。<br /><br /> - プロジェクトノードのキャプションとアイコンを変更します。<br />- プロジェクト`Browse`オブジェクトを完全にオーバーライドします。<br />- プロジェクトの名前を変更できるかどうかを制御します。<br />- 並べ替え順序を制御します。<br />- ダイナミック ヘルプのユーザー コンテキストを制御します。|
|から<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|プロジェクト のサブタイプを使用して、デザイナーとエディターに提供されるコンテキスト サービスを制御できます。|
|から<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|プロジェクトのサブタイプを有効にします。<br /><br /> - プロジェクト コマンドのコマンド ルーティングに参加します。<br />- プロジェクトアンビエントコマンドとソリューションエクスプローラのアクティブコマンドの両方を追加、削除、または無効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|プロジェクトのサブタイプが、ユーザーが [**新しい項目の追加]** ダイアログ ボックスに表示される内容をフィルター処理できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|プロジェクトのサブタイプを有効にします。<br /><br /> - ファイル拡張子を与えられたデフォルトのジェネレータを決定します。<br />- 人間が読めるジェネレータ名を COM オブジェクトにマップします。|

## <a name="properties-used-by-project-subtypes"></a>プロジェクト のサブタイプで使用されるプロパティ
 環境および基本プロジェクト システムでは、次の表<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID>に<xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2>示すプロパティと列挙型を使用して、プロジェクト のサブタイプがプロジェクト システムのさまざまな機能を制御できるようにします。

|プロパティ|プロジェクトのサブタイプ|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|プロジェクトのサブタイプで[**項目の追加]** ダイアログ ボックスの内容を制御できます。 プロジェクトサブタイプは、テンプレートディレクトリの新しい仕様を提供し、新しい種類の項目を追加し、既存の項目を削除し、基本プロジェクトの**項目の追加**ダイアログボックス内の項目のサブセットを再編成することができます。|
|`PropertyPagesCLSIDList`|プロジェクト サブタイプで、構成に依存しないプロパティ ページを追加または削除できます。|
|`CfgPropertyPagesCLSIDList`|プロジェクト のサブタイプで、構成に依存するプロパティ ページを追加または削除できます。|
|`ExtObjectCATID`|Extender CATID を知ることで、プロジェクトのサブタイプが、プロジェクトまたはプロジェクト項目オブジェクトのオートメーション エクステンダを提供できるようにします。 たとえば、プロジェクトのサブタイプは、カスタム`Project.Extender("<subtype>")`オブジェクトを提供できます。|
|`BrowseObjectCATID`|プロジェクトのサブタイプは、エクステンダー CATID`Browse`を知ることによって、オブジェクトのオートメーション エクステンダを提供できます。 たとえば、プロジェクトのサブタイプは、コレクションに追加のプロパティ<xref:EnvDTE.Project.Properties%2A>を追加できます。|
|`CfgBrowseObjectCATID`|プロジェクトのサブタイプに、プロジェクト構成参照オブジェクトのオートメーション エクステンダを提供できます。 たとえば、プロジェクトのサブタイプは、コレクションに追加のプロパティ<xref:EnvDTE.Configuration.Properties%2A>を追加できます。|
|`CfgExtObjectCATID`|プロジェクトのサブタイプに、構成オブジェクトのオートメーション エクステンダを提供できるようにします。|
|`DefaultPlatformName`|プロジェクトのサブタイプが、プロジェクトの構成オブジェクトのプラットフォーム名を決定できるようにします。|

 基本プロジェクトは、上記のプロパティの既定の実装を提供します。 基本プロジェクトは、最も外側`QueryInterface`の<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>プロジェクトサブタイプを呼び出すことによってこれらを取得するため、プロジェクトのサブタイプはプロパティの実装をオーバーライドできます。

## <a name="see-also"></a>関連項目
- [プロジェクト サブタイプのデザイン](../../extensibility/internals/project-subtypes-design.md)
