---
title: Office ソリューションを開発するコンピューターの構成
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e559ddfec8570077a78fe980632366b4a57605de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930965"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>Office ソリューションを開発するコンピューターの構成

Microsoft Office の VSTO アドインおよびカスタマイズを作成するには、Visual Studio、.NET Framework、Microsoft Office のサポートされているバージョンをインストールします。

|ソフトウェア|サポートされているバージョン|
|--------------|------------------------|
|Visual Studio 2017|**Office/SharePoint 開発**ワークロードを含む任意のエディション|
|.NET Framework|- .NET Framework 4 以降|
|Microsoft Office|<ul><li>Office Professional Plus for Office 365 を含む Office のいずれかのスイート エディション</li><li>次のいずれかのスタンドアロン アプリケーション:<br /><br /> <ul><li>Excel</li><li>InfoPath (Office 2013 および Office 2010 のみ)</li><li>Outlook</li><li>PowerPoint</li><li>Project</li><li>Visio</li><li>Word</li></ul></li></ul><br /> Visual Basic for Applications (VBA) は Office の一部としてインストールされている必要があります。**重要:** Office 2010 アプリケーションのクイック実行バージョンはサポートされていません。|

詳細なインストール手順については、[Office ソリューションを開発するコンピューターを構成する方法](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)を参照してください。

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>プロジェクト テンプレートが表示されない、または Visual Studio で動作しない場合

サポートされているバージョンの Visual Studio、.NET Framework、および Microsoft Office をインストールしたが、Visual Studio の**新しいプロジェクト** ダイアログ ボックスで Office プロジェクト テンプレートが表示されないか場合、または、いずれかを使用しようとするとエラーが発生する場合、次を確認します。

- 使用するコンピューターに Microsoft Office Developer Tools がインストールされていることを確認します。

     Office Developer Tools は、Visual Studio のオプションのコンポーネントですが、Visual Studio と共に自動的にインストールされます。インストールする機能を指定して Visual Studio のインストールをカスタマイズする場合は、各種ツールをインストールするために、セットアップ時に必ず **[Microsoft Office Developer Tools]** を選択してください。

     これらのツールがインストールされていることを確認するために、Visual Studio のセットアップ プログラムを開始して、**変更**ボタンをクリックします。 **[Microsoft Office Developer Tools]** チェック ボックスをオンにして **[更新]** ボタンをクリックします。

- 実行で提供された Office のバージョンを実行していないことを確認します。「[Outlook がコンピューター上のクイック実行アプリケーションかどうかを確認する方法](/previous-versions/office/developer/office-2010/ff864733(v=office.14))」を参照してください。

- Microsoft Office の 1 つだけのバージョンを実行していることを確認します。

問題が発生する場合、「[Office ソリューションのエラーのための追加サポート](../vsto/additional-support-for-errors-in-office-solutions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office ソリューションを開発するコンピューターを構成する方法](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする方法](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Office プライマリ相互運用機能アセンブリをインストールする方法](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [Office アプリケーションおよびプロジェクトの種類で使用できる機能](../vsto/features-available-by-office-application-and-project-type.md)