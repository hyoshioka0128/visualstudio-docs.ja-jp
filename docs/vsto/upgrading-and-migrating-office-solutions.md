---
title: Office ソリューションのアップグレードと移行
description: 以前のバージョンの Visual studio で作成された Offince プロジェクトがある場合は、現在のバージョンの Visual Studio で使用するようにプロジェクトをアップグレードする必要があります。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], upgrading
- Office projects [Office development in Visual Studio], upgrading
- upgrading applications [Office development in Visual Studio]
- upgrading Office solutions in Visual Studio
- migrating Office solutions in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b18b61ad6854be654582fe8a8a76da185ec9d89e
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97526606"
---
# <a name="upgrade-and-migrate-office-solutions"></a>Office ソリューションのアップグレードと移行
  旧バージョンの Visual Studio で作成された Microsoft Office プロジェクトがある場合、現在のバーションの Visual Studio で使用するには、そのプロジェクトをアップグレードする必要があります。 Microsoft Office プロジェクトをアップグレードするには、Microsoft Office 開発ツールが含まれているバージョンの Visual Studio でそれを開きます。 Microsoft Office 開発者ツールを含む Visual Studio のバージョンの詳細については、「 [Office ソリューションを開発するためのコンピューターの構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

[!include[Add-ins note](includes/addinsnote.md)]

> [!NOTE]
> Visual Studio では、以前のバージョンの Visual Studio を使用して作成した InfoPath フォーム テンプレート プロジェクトはアップグレードできません。 これらの種類のプロジェクトは、Visual Studio の現在のリリースではサポートされていません。

## <a name="changes-to-upgraded-projects"></a>アップグレードされたプロジェクトに対する変更
 Microsoft Office プロジェクトをアップグレードするときに、次の項目を対象とするプロジェクトが Visual Studio によって変更されます。

- Visual Studio 2010 Tools for Office runtime。 詳細については、「 [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

- 現在のアセンブリ参照。

- このプロジェクトの種類でサポートされている .NET Framework のバージョン (Visual Studio 2013 にアップグレードする場合のみ)。

- このプロジェクトの種類でサポートされている Microsoft Office のバージョン (Visual Studio 2013 にアップグレードする場合のみ)。

## <a name="assembly-references"></a>アセンブリ参照
 Visual Studio は、プロジェクト内の次のアセンブリ参照をアップグレードします。

- Microsoft Office プライマリ相互運用機能アセンブリ (PIA)。

- [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]のアセンブリ。 これらのアセンブリの詳細については、「 [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

- 依存アセンブリの新バージョンまたは更新バージョン。

## <a name="targeted-net-framework"></a>対象の .NET Framework
 プロジェクトを Visual Studio 2013 にアップグレードすると、Visual Studio は [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] または [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]を対象とするようにプロジェクトを変更します。 プロジェクトが対象とする .NET Framework のバージョンは、自分のコンピューターにインストールされている Office のバージョンによって異なります。 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] がインストールされている場合は、 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]を対象とするように Visual Studio によってプロジェクトが変更されます。 それ以外の場合は、Visual Studio は [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]を対象とするようにプロジェクトを変更します。

> [!NOTE]
> 対象を変更されたソリューションを実行するために、開発用コンピューターとエンド ユーザーのコンピューターでいくつかの追加の手順が必要になることがあります。また、特定の機能を使用するプロジェクトはコンパイルされなくなります。 詳細については、「 [.NET Framework 4 以降への Office ソリューションの移行](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)」を参照してください。

 Office プロジェクトで [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする場合は、.NET Framework 3.5 を対象とする場合には使用できないいくつかの機能を使用できます。 詳細については、「 [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

## <a name="targeted-office-application"></a>対象の Office アプリケーション
 Office プロジェクトを Visual Studio 2013 にアップグレードすると、Visual Studio はプロジェクトの種類 (ドキュメント レベルのカスタマイズ プロジェクトや VSTO アドイン プロジェクトなど) によってサポートされている Microsoft Office のバージョンを対象とするようにプロジェクトを変更します。

 Visual Studio 2013 の Office プロジェクトは、 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] と [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] のアプリケーションを対象とすることができます。 Visual Studio はインストールされている Office の最新バージョンを対象とするようにプロジェクトを変更します。 Office のどのバージョンもインストールされていない場合、Visual Studio はプロジェクトをアップグレードしません。

> [!NOTE]
> VSTO アドインプロジェクトを以降を対象とするようにアップグレードする場合は [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 、 `ThisAddIn_Startup` vsto アドインのイベントハンドラーに、アプリケーション内のドキュメントにアクセスするコードが含まれていないことを確認してください。 詳細については、「 [Office アプリケーションの起動時にドキュメントにアクセスする](../vsto/programming-vsto-add-ins.md#AccessingDocuments)」を参照してください。

 ドキュメントレベルのカスタマイズの場合、は、 [!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] *.xls* や *.doc* の拡張子を持つドキュメントなど、バイナリ形式のプロジェクト内のドキュメントを、Office Open XML 形式に変換します。 Open XML の詳細については、「 [新しいファイル名拡張子とオープン xml 形式の概要](https://support.office.com/en-nz/article/Introduction-to-new-file-name-extensions-eca81dcb-5626-4e5b-8362-524d13ae4ec1)」を参照してください。

> [!NOTE]
> スマート タグは Excel 2010 および Word 2010 では非推奨とされます。 したがって、ソリューションでスマート タグを使用している場合は、Visual Studio 2013 または Visual Studio 2015 でソリューションをテストおよびデバッグするために、それらを削除する必要があります。

## <a name="upgrade-microsoft-office-2003-projects"></a>2003プロジェクト Microsoft Office アップグレード
 Microsoft Office 2003 を対象とするドキュメント レベルのカスタマイズおよび VSTO アドインをアップグレードする際には、追加の考慮事項がいくつかあります。

### <a name="document-level-projects"></a>ドキュメントレベルのプロジェクト
 プロジェクトのドキュメントに Windows フォーム コントロールが含まれている場合は、プロジェクトをアップグレードする前に、Visual Studio 2005 Tools for Office Second Edition Runtime がインストールされている必要もあります。 プロジェクトをアップグレードする前に、このバージョンのランタイムが開発用コンピューターにインストールされていない場合は、アップグレード後のプロジェクトでコンパイル エラーまたは実行時エラーが発生することがあります。 Visual Studio 2005 Tools for Office Second Edition Runtime は、他の Office ソリューションで使用されていない場合、プロジェクトのアップグレードが完了した後に開発用コンピューターからアンインストールできます。 このバージョンのランタイムは、Microsoft ダウンロード センターの「 [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 SE) (x86)](https://www.microsoft.com/download/details.aspx?id=2392)」から再頒布可能パッケージとしてダウンロードできます。

### <a name="vsto-add-in-projects"></a>VSTO アドイン プロジェクト
 元のプロジェクトのソリューション ファイルに、VSTO アドインをインストールするように構成されたセットアップ プロジェクトまたは InstallShield Limited Edition プロジェクトが含まれていた場合、Visual Studio はそのプロジェクトをアップグレードしますが、プロジェクトに対してそれ以外の変更は加えません。 引き続き Windows インストーラー ファイルを使用して VSTO アドインを配置するには、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]、Visual Studio 2010 Tools for Office Runtime、および必要な場合は VSTO アドインで参照されているプライマリ相互運用機能アセンブリなど、新しい必須コンポーネントをインストールするようにセットアップ プロジェクトまたは InstallShield Limited Edition プロジェクトを変更する必要があります。 詳細については、「 [Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

 ClickOnce を使用して VSTO アドインを配置する場合には、セットアップ プロジェクトまたは InstallShield Limited Edition プロジェクトを完全に削除できます。 ClickOnce を使用した VSTO アドインの配置の詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Office ソリューションをアップグレードする](/previous-versions/4bez6837(v=vs.140))
- [Office ソリューションを .NET Framework 4 以降に移行する](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [[プロジェクトのアップグレード] ([オプション] ダイアログボックス)](../vsto/project-upgrade-options-dialog-box.md)