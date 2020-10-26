---
title: InfoPath ソリューション
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], InfoPath
- templates [Office development in Visual Studio], InfoPath
- InfoPath [Office development in Visual Studio]
- Office development in Visual Studio, InfoPath solutions
- projects [Office development in Visual Studio], InfoPath
- Office solutions [Office development in Visual Studio], InfoPath
- Office projects [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7eda46c04cdbe5ba73e32e124486cfc391e5ac17
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985744"
---
# <a name="infopath-solutions"></a>InfoPath ソリューション
  Visual Studio には、Microsoft Office InfoPath 2013 および InfoPath 2010 の VSTO アドインの作成に使用できるプロジェクト テンプレートが用意されています。 InfoPath は、Office 2016 では使用できません。

> [!NOTE]
> Office 2016 がインストールされている場合でも、InfoPath 用の VSTO アドインを作成することはできます。 InfoPath 2013 または Office 2013 を Office 2016 とサイドバイサイドにインストールするだけです。

 [!INCLUDE[appliesto_infoallapp](../vsto/includes/appliesto-infoallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 InfoPath 用の VSTO アドインは、他の Microsoft Office アプリケーションの VSTO アドインと似ています。 このようなソリューションは、アプリケーションが読み込むアセンブリで構成されます。 エンド ユーザーは、どのフォームまたはフォーム テンプレートが開いているかに関係なく、このアセンブリの機能にアクセスできます。 VSTO アドインの詳細については、「vsto アドインの [プログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md) 」と「 [Vsto アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

> [!NOTE]
> Visual Studio 2015 には、以前のバージョンの Visual Studio で提供されていた InfoPath フォーム テンプレート プロジェクトは含まれていません。 また、Visual Studio 2015 を使用して、以前のバージョンの Visual Studio で作成した InfoPath フォーム テンプレート プロジェクトを開いて編集することもできません。 ただし、Visual Studio Tools for Applications を使用すると、InfoPath フォーム テンプレート プロジェクトを開いて編集できます。 詳細については、「 [InfoPath 2010 での VSTO 2008 プロジェクト](https://blogs.msdn.microsoft.com/infopath/2011/04/14/working-with-vsto-2008-projects-in-infopath-2010/)の使用」を参照してください。

## <a name="automate-infopath-by-using-an-add-in"></a>アドインを使用して InfoPath を自動化する
 Visual Studio の Office 開発ツールを使用して作成した Office VSTO アドインから InfoPath オブジェクト モデルにアクセスするには、プロジェクトの `Application` クラスの `ThisAddIn` フィールドを使用します。 `Application` フィールドは InfoPath の現在のインスタンスを表す <xref:Microsoft.Office.Interop.InfoPath.Application> オブジェクトを返します。 詳細については、「 [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)」を参照してください。

 VSTO アドインから InfoPath オブジェクトモデルを呼び出すときは、InfoPath のプライマリ相互運用機能アセンブリに用意されている型を使用します。 プライマリ相互運用機能アセンブリは、VSTO アドインのマネージド コードと InfoPath の COM オブジェクト モデルとの仲介役を果たします。 InfoPath プライマリ相互運用機能アセンブリ内の型は、すべて <xref:Microsoft.Office.Interop.InfoPath> 名前空間に定義されています。 InfoPath プライマリ相互運用機能アセンブリの詳細については、「 [Microsoft Office infopath プライマリ相互運用機能アセンブリについ](https://msdn.microsoft.com/1b3ae03c-6951-49e4-a489-4712d3f7ba72)て」を参照してください。 一般的なプライマリ相互運用機能アセンブリの詳細については、「 [office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md) と [office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)」を参照してください。

## <a name="customize-the-user-interface-of-infopath-by-using-an-add-in"></a>アドインを使用して InfoPath のユーザーインターフェイスをカスタマイズする
 InfoPath 用の VSTO アドインを作成する場合、いくつかの異なる UI カスタマイズオプションがあります。 次の表は、主なカスタマイズ方法を示しています。

|タスク|詳細情報|
|----------|--------------------------|
|カスタム作業ウィンドウを作成する。|[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)|
|InfoPath のリボンにカスタム タブを追加する。|[InfoPath のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-infopath.md)|

 InfoPath およびその他の Microsoft Office アプリケーションの UI をカスタマイズする方法の詳細については、「 [OFFICE ui のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [Microsoft Office の InfoPath プライマリ相互運用機能アセンブリについて](https://msdn.microsoft.com/1b3ae03c-6951-49e4-a489-4712d3f7ba72)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office 開発における InfoPath 2010](/previous-versions/office/developer/office-2010/ff604966(v=office.14))
