---
title: プロジェクトのサブタイプによって拡張されたプロパティとメソッド |Microsoft Docs
description: プロジェクトのサブタイプで拡張または変更できる機能について説明します。これにより、Visual Studio のプロジェクトシステムの動作をカスタマイズできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d5d81135a2571db3c84b67acb2fa08e4f83f57d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970063"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>プロジェクト サブタイプによって拡張されるプロパティとメソッド
プロジェクトのサブタイプは、基本プロジェクトのアグリゲーターとして構築されるため、プロジェクトの動作に大きな影響を与えます。 このセクションでは、プロジェクトのサブタイプによって強化または変更できる機能の一部をまとめます。

## <a name="features-gained-by-aggregation"></a>集計によって得られる機能
 次の表は、集計によってプロジェクトのサブタイプが基本プロジェクトでオーバーライドできる多くのメソッドをまとめたものです。

|集計によってオーバーライドされるメソッド|プロジェクトのサブタイプ|
|---------------------------------------|---------------------|
|開始 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> :<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|プロジェクトのサブタイプを<br /><br /> -プロジェクトノードのキャプションとアイコンを変更します。<br />-プロジェクトオブジェクトを完全にオーバーライド `Browse` します。<br />-プロジェクトの名前を変更できるかどうかを制御します。<br />-制御の並べ替え順序。<br />-ダイナミックヘルプのユーザーコンテキストを制御します。|
|開始 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> :<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|デザイナーおよびエディターに提供されるコンテキストサービスをプロジェクトのサブタイプで制御できるようにします。|
|開始 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> :<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|プロジェクトのサブタイプを<br /><br /> -Project コマンドのコマンドルーティングに参加します。<br />-プロジェクトのアンビエントコマンドとソリューションエクスプローラーアクティブなコマンドの両方を追加、削除、または無効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|[ **新しい項目の追加** ] ダイアログボックスでユーザーに表示される内容をプロジェクトのサブタイプでフィルター処理できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|プロジェクトのサブタイプを<br /><br /> -ファイル拡張子が指定された既定のジェネレーターを特定します。<br />-人間が判読できるジェネレーター名を COM オブジェクトにマップします。|

## <a name="properties-used-by-project-subtypes"></a>プロジェクトのサブタイプで使用されるプロパティ
 環境と基本プロジェクトシステムでは、次の表に示すプロパティと列挙型を使用して、プロジェクト <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> のサブタイプがプロジェクトシステムのさまざまな機能を制御できるようにすることができます。

|VSHPROPID プロパティ|プロジェクトのサブタイプ|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|プロジェクトのサブタイプで [ **項目の追加** ] ダイアログボックスの内容を制御できるようにします。 プロジェクトのサブタイプでは、テンプレートディレクトリの新しい仕様を指定したり、新しい種類の項目を追加したり、既存の項目を削除したり、基本プロジェクトの [ **項目の追加** ] ダイアログボックスで項目のサブセットを再編成したりできます。|
|`PropertyPagesCLSIDList`|プロジェクトのサブタイプが、構成に依存しないプロパティページを追加または削除できるようにします。|
|`CfgPropertyPagesCLSIDList`|プロジェクトのサブタイプが、構成に依存するプロパティページを追加または削除できるようにします。|
|`ExtObjectCATID`|プロジェクトのサブタイプが、エクステンダーの CATID を知って、プロジェクトまたはプロジェクト項目オブジェクトのオートメーションエクステンダーを提供できるようにします。 たとえば、プロジェクトのサブタイプは、カスタムオブジェクトを提供でき `Project.Extender("<subtype>")` ます。|
|`BrowseObjectCATID`|Extender の CATID を知って、プロジェクトのサブタイプがオブジェクトのオートメーションエクステンダーを提供できるようにし `Browse` ます。 たとえば、プロジェクトのサブタイプでは、コレクションに追加のプロパティを追加でき <xref:EnvDTE.Project.Properties%2A> ます。|
|`CfgBrowseObjectCATID`|プロジェクトのサブタイプが、プロジェクト構成参照オブジェクトのオートメーションエクステンダーを提供できるようにします。 たとえば、プロジェクトのサブタイプでは、コレクションに追加のプロパティを追加でき <xref:EnvDTE.Configuration.Properties%2A> ます。|
|`CfgExtObjectCATID`|プロジェクトのサブタイプが構成オブジェクトのオートメーションエクステンダーを提供できるようにします。|
|`DefaultPlatformName`|プロジェクトの構成オブジェクトのプラットフォーム名をプロジェクトのサブタイプで判断できるようにします。|

 基本プロジェクトは、上記のプロパティの既定の実装を提供します。 基本プロジェクトは、最も外側のプロジェクトのサブタイプに対してを呼び出すことによってこれらの値を取得し `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。これにより、プロジェクトのサブタイプでプロパティの実装をオーバーライドできるようになります。

## <a name="see-also"></a>関連項目
- [プロジェクト サブタイプのデザイン](../../extensibility/internals/project-subtypes-design.md)
