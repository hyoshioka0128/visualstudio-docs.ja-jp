---
title: Visual Studio Tools for Office ランタイムのアセンブリ
description: Visual Studio によって Visual Studio Tools for Office ランタイムアセンブリに参照が自動的に追加されることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, assemblies
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 600408231e5085009e5edc546535ca8e5110fc6e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882558"
---
# <a name="assemblies-in-the-visual-studio-tools-for-office-runtime"></a>Visual Studio Tools for Office ランタイムのアセンブリ
  Office プロジェクトを作成すると、Visual Studio によって、そのプロジェクト タイプとプロジェクトの対象 .NET Framework に使用する [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] アセンブリの参照が自動的に追加されます。 .NET Framework 3.5、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]、 [!INCLUDE[net_v45](includes/net-v45-md.md)]の Office 拡張機能にさまざまなアセンブリがあります。 Office 拡張機能の詳細については、「 [Visual Studio Tools for Office ランタイムの概要](visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-4-and-the-net_v45"></a>.NET Framework 4 との Office 拡張機能のアセンブリ [!INCLUDE[net_v45](includes/net-v45-md.md)]
 次の表は、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] と [!INCLUDE[net_v45](includes/net-v45-md.md)]の Office 拡張機能に含まれているアセンブリをまとめたものです。 これらのアセンブリの名前空間と型に関するドキュメントについては、「 [Visual Studio での Office 開発のマネージリファレンス &#40;&#41;](managed-reference-office-development-in-visual-studio.md)」を参照してください。

|アセンブリ名|Description|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.dll|次の型を提供します。<br /><br /> -リボンのカスタマイズとスマートタグを作成するための型。 **注:**      スマートタグは、およびで非推奨とされ [!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] ます。<br />-ドキュメントレベルのカスタマイズと VSTO アドインのカスタム作業ウィンドウで操作ウィンドウを作成するための型。|
|Microsoft.Office.Tools.Excel.dll|Excel プロジェクトのホスト項目とホスト コントロールを表すインターフェイスとサポートする型を提供します。 詳細については、「 [拡張オブジェクトを使用](automating-excel-by-using-extended-objects.md)した Excel の自動化」を参照してください。|
|Microsoft.Office.Tools.Outlook.dll|Outlook VSTO アドインでカスタム フォーム領域の作成に使用できる型を提供します。|
|Microsoft.Office.Tools.Word.dll|Word プロジェクトのホスト項目とホスト コントロールを表すインターフェイスとサポートする型を提供します。 詳細については、「 [拡張オブジェクトを使用した Word の自動化](automating-word-by-using-extended-objects.md)」を参照してください。|
|Microsoft.Office.Tools.v4.0.Framework.dll|次の型を提供します。<br /><br /> -Visual Studio Tools for Office ランタイムによってスローされる可能性のある例外。<br />-Outlook フォーム領域を作成するときに使用できる属性。|
|Microsoft.Office.Tools.dll|Visual Studio Tools for Office Runtime インフラストラクチャに属し、コードから直接使用するものではない型を提供します。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.dll|次の型を提供します。<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性と <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> インターフェイス。ドキュメントレベルのカスタマイズでデータオブジェクトをキャッシュするために使用できます。 詳細については、「 [データのキャッシュ](caching-data.md)」を参照してください。<br />-この <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> インターフェイスを実装すると、Office ソリューションの ClickOnce インストーラーの最後の手順として追加のインストール手順を実行できます。 詳細については、「 [ClickOnce を使用した Office ソリューションの配置](deploying-an-office-solution-by-using-clickonce.md)」を参照してください。<br />-Visual Studio Tools for Office ランタイムによってスローされる可能性のある例外。<br />-Visual Studio Tools for Office ランタイムインフラストラクチャの一部であるその他の型は、コードから直接使用するためのものではありません。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll|次の型を提供します。<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> カスタマイズアセンブリをドキュメントにアタッチし、ドキュメント内のキャッシュされたデータにアクセスするために使用できるクラス。 詳細については、「 [ServerDocument クラスを使用してサーバー上のドキュメントを管理](managing-documents-on-a-server-by-using-the-serverdocument-class.md)する」を参照してください。<br />-ドキュメントレベルのカスタマイズでキャッシュされたデータの階層を表すいくつかのクラス。 詳細については、「 [サーバー上のドキュメントのデータにアクセス](accessing-data-in-documents-on-the-server.md)する」を参照してください。|

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](includes/net-v45-md.md)] を対象とするプロジェクトは次のアセンブリも参照します。 これらのアセンブリは再頒布可能な [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] に含まれません。 これらはむしろ、ソリューションで展開しなければならない従属アセンブリです。 既定では、プロジェクトのビルド出力フォルダーにコピーされます (これらのアセンブリの **[ローカル コピー]** プロパティは **True** に設定されます)。 ClickOnce を使用してプロジェクトを展開する場合、これらのアセンブリは生成されたパッケージに含まれます。

|アセンブリ名|Description|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v4.0.Utilities.dll|VSTO アドイン プロジェクトで生成される `ThisAddIn` クラスとすべてのプロジェクトで生成される Ribbon クラスの基底クラスを提供します。|
|Microsoft.Office.Tools.Excel.v4.0.Utilities.dll|次の型を提供します。<br /><br /> - `ThisWorkbook` `Sheet` Excel のドキュメントレベルのプロジェクトで生成されるクラスとクラスの基本クラス。<br />-Excel プロジェクトのワークシートで使用できるコントロール Windows フォームます。|
|Microsoft.Office.Tools.Outlook.v4.0.Utilities.dll|Outlook プロジェクトで生成される `ThisAddIn` とフォーム領域クラスの基本クラスを提供します。|
|Microsoft.Office.Tools.Word.v4.0.Utilities.dll|次の型を提供します。<br /><br /> - `ThisDocument` Word のドキュメントレベルのプロジェクトで生成されるクラスの基本クラス。<br />-Word プロジェクトのドキュメントで使用できるコントロールを Windows フォームします。|

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-35"></a>.NET Framework 3.5 用の Office 拡張機能のアセンブリ
 次の表は、.NET Framework 3.5 の Office 拡張機能に含まれているアセンブリをまとめたものです。 これらのアセンブリの名前空間とクラスに関するドキュメントについては、Visual Studio 2008 ドキュメントの「」を参照してください [http://go.microsoft.com/fwlink/?LinkId=160658](managed-reference-office-development-in-visual-studio.md) 。

|アセンブリ名|Description|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v9.0.dll|次の型を提供します。<br /><br /> -VSTO アドインの場合は、Microsoft. Office. .Addin 基底クラス。<br />-リボンのカスタマイズとスマートタグを作成するためのクラス。 **注:**      スマートタグは、およびで非推奨とされ [!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] ます。<br />-ドキュメントレベルのカスタマイズと VSTO アドインのカスタム作業ウィンドウで操作ウィンドウを作成するためのクラス。|
|Microsoft.Office.Tools.Excel.v9.0.dll|Excel ソリューションのホスト項目とホスト コントロールを提供します。 詳細については、「 [拡張オブジェクトを使用](automating-excel-by-using-extended-objects.md)した Excel の自動化」を参照してください。|
|Microsoft.Office.Tools.Outlook.v9.0.dll|Outlook VSTO アドインでカスタム フォーム領域の作成に使用できるクラスを提供します。|
|Microsoft.Office.Tools.Word.v9.0.dll|Word ソリューションのホスト項目とホスト コントロールを提供します。 詳細については、「 [拡張オブジェクトを使用した Word の自動化](automating-word-by-using-extended-objects.md)」を参照してください。|
|Microsoft.Office.Tools.v9.0.dll|次の型を提供します。<br /><br /> - [RemoteBindableComponent](/previous-versions/visualstudio/visual-studio-2008/bb546360(v=vs.90)) クラス。ドキュメントレベルのカスタマイズでホストコントロールのデータバインディング機能を提供します。<br />-Visual Studio Tools for Office ランタイムインフラストラクチャの一部であるその他の型は、コードから直接使用するためのものではありません。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v9.0.dll|次の型を提供します。<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性と <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> インターフェイス。ドキュメントレベルのカスタマイズでデータオブジェクトをキャッシュするために使用できます。 詳細については、「 [データのキャッシュ](caching-data.md)」を参照してください。<br />-Visual Studio Tools for Office ランタイムによってスローされる可能性のある例外。<br />-Visual Studio Tools for Office ランタイムインフラストラクチャの一部であるその他の型は、コードから直接使用するためのものではありません。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v10.0.dll|Office ソリューションの ClickOnce インストーラーの最後の手順として追加のインストール手順を実行するために実装できる <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> インターフェイスを提供します。 詳細については、「 [高度な Office ソリューションの配置](/previous-versions/visualstudio/visual-studio-2010/dd234217(v=vs.100))」を参照してください。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.v10.0.dll|次の型を提供します。<br /><br /> - <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラス。プログラムによってカスタマイズアセンブリをドキュメントに添付し、ドキュメント内のキャッシュされたデータにアクセスするために使用できます。 詳細については、「 [ServerDocument クラスを使用してサーバー上のドキュメントを管理](managing-documents-on-a-server-by-using-the-serverdocument-class.md)する」を参照してください。<br />-ドキュメントレベルのカスタマイズでキャッシュされたデータの階層を表すいくつかのクラス。 詳細については、「 [サーバー上のドキュメントのデータにアクセス](accessing-data-in-documents-on-the-server.md)する」を参照してください。|
|Microsoft.VisualStudio.Tools.Office.Runtime.v10.0.dll|次の型を提供します。<br /><br /> -VisualStudio クラスと VisualStudio クラス。このクラスを使用すると、.NET Framework 3.5 を対象とする Office ソリューションに信頼を付与するために、ユーザーによる一覧のエントリを作成できます。 UserInclusionList クラスを使用して、ユーザーの信頼のリストのエントリを作成することができます。<br />-Visual Studio Tools for Office ランタイムインフラストラクチャの一部であるその他の型は、コードから直接使用するためのものではありません。|

## <a name="see-also"></a>関連項目
- [Visual Studio Tools for Office ランタイムの概要](visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office ランタイムのインストールシナリオ](visual-studio-tools-for-office-runtime-installation-scenarios.md)
