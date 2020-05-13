---
title: Office アプリケーションおよびプロジェクトの種類で使用できる機能
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio]
- Office development in Visual Studio, features
- Ribbon [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], features available
- document-level customizations [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], features available
- add-ins [Office development in Visual Studio]
- form regions [Office development in Visual Studio], features available
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: df645fc7f53bbcd0ad5294182d13e96b57b5d42d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431586"
---
# <a name="features-available-by-office-application-and-project-type"></a>Office アプリケーションおよびプロジェクトの種類で使用できる機能
  Visual Studio には、次のように、Microsoft Office アプリケーションのさまざまなビジネス シナリオをサポートするプロジェクト テンプレートがいくつか用意されています。

- ドキュメントレベルのカスタマイズ。

- VSTO アドイン。

  すべてのプロジェクトの種類を使用できないアプリケーションもあります。 たとえば、ドキュメントレベルのプロジェクトは、Microsoft Office Word と Microsoft Office Excel でのみ使用できます。 同様に、一部の機能は、特定の種類のプロジェクトまたはアプリケーションでのみ使用できます。 たとえば、操作ウィンドウは、ドキュメントレベルのプロジェクトでのみ使用できます。また、リボンの拡張機能は、一部のアプリケーションでのみ使用できます。 別のプロジェクトの種類の詳細については、[Office ソリューション開発の概要&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)を参照してください。

> [!NOTE]
> Office プロジェクト テンプレートは、一部のエディションの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でのみ使用できます。 詳細については、[Office ソリューションの開発のためのコンピューター構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)を参照してください。

## <a name="project-types-available-for-different-microsoft-office-applications"></a>プロジェクトの種類別の Microsoft Office アプリケーションで利用できます。
 プロジェクトの種類ごとに使用できるアプリケーションを次の表に示します。

|プロジェクトの種類|Microsoft Office アプリケーション|
|-------------------|----------------------------------|
|ドキュメント レベルのカスタマイズ|Excel<br /><br /> Word|
|VSTO アドイン|Excel<br /><br /> InfoPath (InfoPath 2013 と InfoPath 2010 のみ)<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Visio<br /><br /> Word<br /><br /> Excel|

## <a name="features-available-in-different-project-types"></a>異なる種類のプロジェクトで使用できる機能
 プロジェクトの種類ごとに異なる機能を次の表に示します。

|機能|機能を提供するプロジェクトの種類|関連項目|
|-------------|--------------------------------------------|---------------------|
|操作ウィンドウ|ドキュメントレベルのプロジェクト|[操作ウィンドウの概要](../vsto/actions-pane-overview.md)|
|ClickOnce 配置|VS およびドキュメントレベルのプロジェクト|[Office ソリューションのデプロイ](../vsto/deploying-an-office-solution.md)|
|カスタム作業ウィンドウ|次のアプリケーション用の VSTO アドイン プロジェクト:<br /><br /> -   Excel<br />-   InfoPath (InfoPath 2013 と InfoPath 2010 のみ)<br />-   Outlook<br />-   PowerPoint<br />-   Word|[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)|
|カスタム XML 部分。|ドキュメントレベルのプロジェクト<br /><br /> 次のアプリケーション用のアプリケーション レベルのプロジェクト:<br /><br /> -   Excel<br />-   PowerPoint<br />-   Word|[カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)|
|データ キャッシュ。|ドキュメントレベルのプロジェクト|[ドキュメント レベルのカスタマイズでキャッシュされたデータ](../vsto/cached-data-in-document-level-customizations.md)|
|他の Microsoft Office ソリューションへの VSTO アドイン内のオブジェクトの公開|VSTO アドイン プロジェクト|[他の Office ソリューションから VSTO アドイン内のコードを呼び出す](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)|
|次のホスト コントロール:<br /><br /> -   Chart<br />-   ListObject<br />-   NamedRange<br />-   コンテンツ コントロール<br />-ブックマーク|ドキュメントレベルのプロジェクト<br /><br /> Word と Excel 用の VSTO アドイン プロジェクト。|[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)|
|次のホスト コントロール:<br /><br /> -   XMLMappedRange<br />-   XMLNode<br />-   XMLNodes|ドキュメントレベルのプロジェクト|[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)|
|複数プロジェクトの配置|ドキュメントレベルのプロジェクト<br /><br /> VSTO アドイン プロジェクト|[チュートリアル: 単一の ClickOnce インストーラーでの複数の Office ソリューションのデプロイ](https://msdn.microsoft.com/051223c0-4082-4799-b78b-a4763a9def55)|
|Outlook フォーム領域|Outlook の VSTO アドイン プロジェクト|[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)|
|配置後の動作。|ドキュメントレベルのプロジェクト<br /><br /> VSTO アドイン プロジェクト|[チュートリアル: ClickOnce インストール後のドキュメントのエンドユーザーのコンピューターへのコピー](https://msdn.microsoft.com/100090f7-bc63-4152-b3e1-19b48bc27466)|
|リボンのカスタマイズ。|ドキュメントレベルのプロジェクト<br /><br /> 次のアプリケーション用の VSTO アドイン プロジェクト:<br /><br /> -   Excel<br />-   InfoPath (InfoPath 2013 と InfoPath 2010 のみ)<br />-   Outlook<br />-   PowerPoint<br />-   Project<br />-   Visio<br />-   Word|[リボンの概要](../vsto/ribbon-overview.md)|
|視覚的なドキュメント デザイナー|ドキュメントレベルのプロジェクト|[Visual Studio 環境における office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)|

## <a name="see-also"></a>関連項目
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office ソリューション開発の概要&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ドキュメント レベルのカスタマイズでキャッシュされたデータ](../vsto/cached-data-in-document-level-customizations.md)
- [Office ソリューションのデプロイ](../vsto/deploying-an-office-solution.md)
