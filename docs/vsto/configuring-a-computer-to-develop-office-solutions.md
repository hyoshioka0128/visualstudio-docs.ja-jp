---
title: Office ソリューションを開発するようにコンピューターを構成する
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
ms.openlocfilehash: 7a0304c217599e790b8cfa9e738245927336470e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88801842"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>Office ソリューションを開発するようにコンピューターを構成する

Microsoft Office の VSTO アドインおよびカスタマイズを作成するには、Visual Studio、.NET Framework、Microsoft Office のサポートされているバージョンをインストールします。

|ソフトウェア|サポートされているバージョン|
|--------------|------------------------|
|Visual Studio 2017| **Office/SharePoint 開発**ワークロードを含む任意のエディション。|
|.NET Framework|-.NET Framework 4 以降。|
|Microsoft Office|<ul><li>Enterprise 用の Microsoft 365 アプリを含む Office のスイートエディション。</li><li>次のいずれかのスタンドアロン アプリケーション:<br /><br /> <ul><li>Excel</li><li>InfoPath (Office 2013 および Office 2010 のみ)</li><li>Outlook</li><li>PowerPoint</li><li>Project</li><li>Visio</li><li>Word</li></ul></li></ul><br /> Visual Basic for Applications (VBA) は Office の一部としてインストールされている必要があります。 **重要:** Office 2010 アプリケーションの実行時のバージョンはサポートされていません。|

インストール手順の詳細については、「 [方法: Office ソリューションを開発するようにコンピューターを構成](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)する」を参照してください。

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>プロジェクトテンプレートが表示されない場合、または Visual Studio でプロジェクトテンプレートが動作しない場合

サポートされているバージョンの Visual Studio、.NET Framework、Microsoft Office をインストールしても、Office プロジェクトテンプレートが Visual Studio の [ **新しいプロジェクト** ] ダイアログボックスに表示されない場合、または、使用しようとしたときにエラーが表示される場合は、次のことを確認してください。

- 使用するコンピューターに Microsoft Office Developer Tools がインストールされていることを確認します。

     Office developer tools は Visual Studio のオプションコンポーネントですが、Visual Studio と共に自動的にインストールされます。 インストールする機能を指定して Visual Studio のインストールをカスタマイズする場合は、各種ツールをインストールするために、セットアップ時に必ず **[Microsoft Office Developer Tools]** を選択してください。

     これらのツールがインストールされていることを確認するには、Visual Studio セットアッププログラムを起動し、[ **変更** ] ボタンをクリックします。 **[Microsoft Office Developer Tools]** チェック ボックスをオンにして **[更新]** ボタンをクリックします。

- 実行時に配信されたバージョンの Office を実行していないことを確認します。 「 [方法: Outlook がコンピューター上で実行中のアプリケーションであるかどうかを確認する](/previous-versions/office/developer/office-2010/ff864733(v=office.14))」を参照してください。

- Microsoft Office の1つのバージョンのみを実行していることを確認します。

引き続き問題が発生する場合は、「 [Office ソリューションでのエラーの追加サポート](../vsto/additional-support-for-errors-in-office-solutions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Visual Studio で &#40;Office 開発を開始する&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [方法: Office ソリューションを開発するようにコンピューターを構成する](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [方法: Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [方法: Office プライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)