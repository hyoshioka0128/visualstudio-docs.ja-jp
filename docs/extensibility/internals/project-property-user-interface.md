---
title: プロジェクト プロパティユーザー インターフェイス |マイクロソフトドキュメント
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4634eb5edaab16752bc5df82d70371a580845d28
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706399"
---
# <a name="project-property-user-interface"></a>プロジェクト プロパティのユーザー インターフェイス

プロジェクトのサブタイプでは、基本プロジェクトから提供されるプロジェクト**の [プロパティ ページ**] ダイアログ ボックスの項目を使用したり、コントロールやページ全体を表示または非表示にしたり、指定されたようにページ全体を作成したり、プロジェクト のサブタイプ固有のページを **[プロパティ ページ]** ダイアログ ボックスに追加したりできます。

## <a name="extending-the-project-property-dialog-box"></a>[プロジェクト プロパティの拡張] ダイアログ ボックス

プロジェクト サブタイプは、オートメーション エクステンダとプロジェクト構成参照オブジェクトを実装します。 これらのエクステンダは<xref:EnvDTE.IFilterProperties>、特定のプロパティを非表示または読み取り専用にするインターフェイスを実装します。 基本プロジェクトによって実装される基本プロジェクトの [**プロパティ ページ**] ダイアログ ボックスは、オートメーション エクステンダーによって実行されるフィルター処理を受け入れます。

[**プロジェクト プロパティ]** ダイアログ ボックスを拡張する手順の概要を以下に示します。

- 基本プロジェクトは、インターフェイスを実装することによって、プロジェクトのサブタイプからエクステン<xref:EnvDTE80.IInternalExtenderProvider>ダーを取得します。 基本プロジェクトの参照オブジェクト、プロジェクトオートメーションオブジェクト、およびプロジェクト構成参照オブジェクトはすべて、このインタフェースを実装します。

- プロジェクト<xref:EnvDTE80.IInternalExtenderProvider>参照オブジェクトおよびプロジェクトオートメーションオブジェクトの実装は、プロジェクトのサブタイプア<xref:EnvDTE80.IInternalExtenderProvider>グリゲーター (つまり、`QueryInterface`<xref:EnvDTE80.IInternalExtenderProvider><xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>プロジェクトオブジェクトに対する) の実装に委ねられます。

- 基本プロジェクト構成参照オブジェクトは、プロジェクトの<xref:EnvDTE80.IInternalExtenderProvider>サブタイプ構成オブジェクトからオートメーション エクステンダに直接ワイヤリングを実装します。 その実装は、プロジェクト<xref:EnvDTE80.IInternalExtenderProvider>のサブタイプ アグリゲーターによって実装されるインターフェイスにデリゲートします。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>プロジェクト構成の参照オブジェクトによって実装され、オブジェクトを<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>返します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>プロジェクト構成の参照オブジェクトによっても実装され、オブジェクトを<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>返します。

- プロジェクトのサブタイプは、次<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>の値を取得することによって、実行時に基本プロジェクトのさまざまな拡張可能なオブジェクトに対して適切な CATID を決定できます。

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_ExtObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_BrowseObjectCATID>

  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2.VSHPROPID_CfgBrowseObjectCATID>

プロジェクト スコープの CATID を決定するために、プロジェクト サブタイプは VSITEMID の上記のプロパティを取得[します。からルート](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)を`VSITEMID typedef`取得します。 プロジェクトのサブタイプでは、構成に依存する構成と構成に依存しない、プロジェクトに対して表示される **[プロパティ ページ**] ダイアログ ボックスのページを制御することもできます。 プロジェクトのサブタイプによっては、組み込みのページを削除し、プロジェクトのサブタイプ固有のページを追加する必要がある場合があります。 これを有効にするために、マネージ クライアント プロジェクトは、次<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>のプロパティのメソッドを呼び出します。

- `VSHPROPID_PropertyPagesCLSIDList`— 構成に依存しないプロパティ ページの CLID のセミコロンで区切られたリスト。

- `VSHPROPID_CfgPropertyPagesCLSIDList —`構成依存プロパティ ページの CLID のセミコロン区切りのリスト。

プロジェクトのサブタイプはオブジェクトを<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>集計するため、これらのプロパティの定義をオーバーライドして、表示するプロパティ**ページ**ダイアログ ボックスを制御できます。 プロジェクトのサブタイプは、内部基本プロジェクトからこれらのプロパティを取得し、必要に応じて CLID を追加または削除できます。

プロジェクトのサブタイプによって追加された新しいプロパティ ページには、基本プロジェクトの実装からプロジェクト構成参照オブジェクトが渡されます。 このプロジェクト構成の参照オブジェクトは、オートメーション エクステンダーをサポートします。 オートメーションエクステンダーの詳細については、「[オートメーション エクステンダーの実装と使用](https://msdn.microsoft.com/Library/0d5c218c-f412-4b28-ab0c-33a611f62356)」を参照してください。 基本プロジェクトの構成参照オブジェクトを拡張する独自の<xref:EnvDTE.Project.Extender%2A>プロジェクト サブタイプ構成参照オブジェクトを取得するために、プロジェクトのサブタイプ呼び出しによって実装されるプロパティ ページ。

## <a name="see-also"></a>関連項目

- <xref:EnvDTE.IFilterProperties>
- [[プロパティ ページ] ダイアログ ボックス](/previous-versions/visualstudio/visual-studio-2010/as5chysf(v=vs.100))
