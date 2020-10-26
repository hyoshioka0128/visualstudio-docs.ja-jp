---
title: プロジェクトの移植、移行、およびアップグレード | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- Win8ExpressDesktopBlock
- w8trefactor
- VS.ReviewProjectAndSolutionChangesDialog.UpgradeRetarget
- ProjectCompatibilityDlgHelpTopic
- VS.ReviewProjectAndSolutionChangesDialog.Upgrade
helpviewer_keywords:
- conversion, projects
- asset compatibility
- projects, conversion
ms.assetid: bee759bd-6ff5-4c2e-913a-ea7d3c906c29
caps.latest.revision: 108
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 3361b04900e549d037338abfba0911b232c9e1bd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75919100"
---
# <a name="port-migrate-and-upgrade-visual-studio-projects"></a>Visual Studio プロジェクトのポート、移行、アップグレード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio に関する最新のドキュメントについては、「[Visual Studio のプロジェクトの移行とアップグレードのリファレンス](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects)」をご覧ください。

Visual Studio の新しいバージョンに移行するかどうかを検討している場合は、この記事を使用して、Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 で作成したソリューション、プロジェクト、ファイル、その他の資産のうち、どれが変更なしで Visual Studio 2013 および Visual Studio 2015 で実行できるのかを確認できます。 または、お使いの Visual Studio のバージョンでサポートされていないプロジェクトや、Azure SDK for .NET などの SDK または拡張機能が必要なプロジェクトを開こうとして、エラー メッセージが表示された場合にも、このページが表示されることがあります。

広く使用されている多くの資産は、Visual Studio 2015、Visual Studio 2013、およびそれ以前の 2 つのバージョンでも同じように動作します。 たとえば、Visual Studio 2015 では、Visual Studio 2013 または Visual Studio 2012 で作成されたプロジェクトを開いて変更した後、Visual Studio 2015 で再度開くことができます。 変更は保持され、プロジェクトは以前のバージョンでの動作と同じように動作します。 これは、Visual Studio 2010 SP1 で作成した多くの資産にも当てはまります。

Visual Basic の場合、Visual Studio 2015 では、Visual Studio 2013 で作成された Visual Basic アプリのコンパイルを妨げる変更は導入されていません。 Visual Studio 2015 を使用して再コンパイルされた Visual Basic アプリの実行時の動作は変化しません。

Visual Studio 2015 を Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 と共に使用する場合は、これらのバージョンのいずれでもプロジェクトとファイルを作成および変更できます。 1 つ以上のバージョンでサポートされていない機能を追加しない限り、バージョン間でプロジェクトとファイルを移行できます。

## <a name="projects"></a><a name="project"></a> イベント

次の一覧では、Visual Studio 2012 または Visual Studio 2010 SP1 で作成されたプロジェクトに対する Visual Studio 2015 および Visual Studio 2013 のサポートについて説明します。 この一覧を使用して、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 でプロジェクトを "そのままの状態で" 開くことができるか、または互換性を確保するために変更する必要があるかを確認します。

|プロジェクトの種類|互換性|
|---------------------|-------------------|
|ユニバーサル Windows プラットフォーム アプリ|ユニバーサル Windows アプリ用ツールをインストールするには、Visual Studio のセットアップで **[カスタム]** または **[変更]** を選択し、 **[ユニバーサル Windows アプリ開発ツール]** を選択します。<br /><br /> Windows 10 向けのユニバーサル Windows プラットフォーム (UWP) アプリの開発は、Windows 10 または [!INCLUDE[win81](../includes/win81-md.md)] 上の Visual Studio 2015 でのみサポートされています。|
|Windows ストア アプリ|Windows 8.1 と Windows Phone 8.1 の両方を対象とするユニバーサル アプリを含む、Windows ストア アプリの開発は、 [!INCLUDE[win81](../includes/win81-md.md)] と Windows 10 でサポートされています。 既存の [!INCLUDE[win8](../includes/win8-md.md)] プロジェクトは引き続き使用できますが、新しい [!INCLUDE[win8](../includes/win8-md.md)] プロジェクトは作成できません。 [!INCLUDE[win81](../includes/win81-md.md)] プロジェクトは、特定の種類の参照のみに依存できます。 詳細については、「[プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)」を参照してください。 **注: Visual Studio 2015 または Visual Studio 2013 を使用して作成した **  [!INCLUDE[win81](../includes/win81-md.md)] プロジェクトを Visual Studio 2012 で開くことはできません。 これは、Visual Studio 2015 および Visual Studio 2013 を使用して作成した [!INCLUDE[win81](../includes/win81-md.md)] プロジェクトはそのバージョンを対象とするのに対し、Visual Studio 2012 では [!INCLUDE[win8](../includes/win8-md.md)] を対象とする [!INCLUDE[win8](../includes/win8-md.md)] プロジェクトしかサポートされていないためです。|
|[!INCLUDE[net_v451](../includes/net-v451-md.md)]|適切なマルチターゲット パックをインストールした後、Visual Studio 2015 および Visual Studio 2013 でこれらのプロジェクトを作成および使用することができます。 これらのプロジェクトは、Visual Studio 2010 SP1 ではサポートされていません。|
|[!INCLUDE[net_v45](../includes/net-v45-md.md)]|これらのプロジェクトは、Visual Studio 2015、Visual Studio 2013、Visual Studio 2012 では作成したり開いたりできますが、Visual Studio 2010 SP1 ではできません。|
|BizTalk|BizTalk サーバー プロジェクトは、Visual Studio 2015 または Visual Studio 2013 と互換性がありません。|
|C#/Visual Basic Silverlight 4 アプリケーションまたはクラス ライブラリ|Visual Studio でプロジェクトを自動的に更新することを許可した場合は、Visual Studio 2013、Visual Studio 2012 のいずれかでこれを開くことができます。|
|C#/Visual Basic Webform または Windows フォーム|Visual Studio 2013 および Visual Studio 2012 でプロジェクトを開くことができます。|
|Visual Basic 6 および Visual C++ 6|Visual Studio 2012 と Visual Studio 2013 では、Visual Basic 6 または Visual C++ 6 を使用して作成したアプリケーションのデバッグがサポートされていません。これらのアプリケーションをデバッグするには、以前のバージョンの Visual Studio をお使いください。|
|コード化された UI テスト|Visual Studio によるプロジェクトの自動更新を許可する場合は、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でこれを開くことができます。|
|F#|Visual Studio 2010 SP1 で作成されたプロジェクトを Visual Studio でアップグレードすることを許可した場合は、Visual Studio 2013 および Visual Studio 2012 でこれを開くことができます。 ただし、Visual Studio の古いバージョンで作成された Silverlight プロジェクトを Visual Studio 2013 にアップグレードすることはできません。 代わりに、Visual Studio 2013 で Silverlight プロジェクトを作成した後、それにコードをコピーする必要があります。 Visual Studio 2013 で作成した Silverlight プロジェクトは、Silverlight 5 を対象とします。|
|LightSwitch|Visual Studio でプロジェクトを自動的にアップグレードすることを許可した場合は、Visual Studio 2013 でのみこれを開くことができます。|
|ローカル データベース キャッシュ|ローカル データベース キャッシュ テンプレートおよび **[データ同期の構成]** ダイアログ ボックスは、Visual Studio 2013 には含まれていません。 Microsoft Synchronization Services v1.0 がインストールされている場合は、Visual Studio 2013 を使用して、[!INCLUDE[vs2010](../includes/vs2010-md.md)] で作成されたプロジェクトを開いて実行できます。ただし、それを Visual Studio 2013 で更新する場合は、コード内のすべての変更を手動で行う必要があります。 代わりに、引き続き [!INCLUDE[vs2010](../includes/vs2010-md.md)] を使用して、これらのプロジェクトを管理および更新することもできます。  新たに開発する場合は、Microsoft Sync Framework によって提供される新しい同期モデルを対象とします。 詳細については、「 [Microsoft Sync Framework Developer Center (Microsoft Sync Framework デベロッパー センター)](https://msdn.microsoft.com/sync/default)」をご覧ください。|
|モデル ビュー コントローラー フレームワーク|Visual Studio 2010 SP1 では MVC 2 と MVC 3 のみが、Visual Studio 2012 では MVC 3 と MVC 4 のみが、Visual Studio 2013 では MVC 4 のみがサポートされています。 MVC 2 から MCV 3 に自動的にアップグレードする方法については、「 [ASP.NET MVC 3 Application Upgrader (ASP.NET MVC 3 アプリケーション アップグレード プログラム)](https://aspnet.codeplex.com/releases/view/59008)」を参照してください。 MVC 2 から MVC 3 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update (ASP.NET MVC 2 プロジェクトから ASP.NET MVC 3 Tools Update へのアップグレード)](https://aspnet.codeplex.com/releases/view/59008)」を参照してください。 MVC 3 から MVC 4 に手動でアップグレードする方法については、「 [Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4 (ASP.NET MVC 3 プロジェクトから ASP.NET MVC 4 へのアップグレード)](/aspnet/whitepapers/mvc4-release-notes)」を参照してください。 .NET Framework 3.5 SP1 を対象とするプロジェクトの場合は、.NET Framework 4 を使用するようにプロジェクトの対象を変更する必要があります。|
|モデリング|Visual Studio によるプロジェクトの自動更新を許可する場合は、Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 でこれを開くことができます。<br /><br /> Team Foundation でモデリング プロジェクトをビルドすると、Team Foundation はプロジェクト内のレイヤーの検証を試みます。 Visual Studio 2013 では、Visual Studio 2010 SP1 で作成されたモデリング プロジェクトに関するレイヤーを Team Foundation ビルドで検証することはできません。 ただし、Visual Studio 2010 SP1 では、Visual Studio 2013 で作成されたモデリング プロジェクト内のレイヤーを Team Foundation ビルドで検証することができます。|
|MPI/クラスター デバッガー|Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 を稼働しているコンピューターに同じバージョンのランタイムまたはツールがインストールされている場合は、3 つのバージョンすべてでこのプロジェクトを開くことができます。|
|MSI セットアップ (.vdproj)|Visual Studio 2013 では、このプロジェクト タイプがサポートされていないため、このプロジェクトを開くことができません。 ほとんどの Windows プラットフォームおよびアプリケーション ランタイムを直接サポートする無料の配置ソリューションである InstallShield Limited Edition for Visual Studio (ISLE) を使用することをお勧めします。 また、ISLE を使用して、Visual Studio インストーラー プロジェクトからデータと設定をインポートすることもできます。 .|
|Office 2007 VSTO|プロジェクトをアップグレードして、Office 2013 と .NET Framework 4 を対象にすると、Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 でこのプロジェクトを開くことができます。|
|Office 2010 VSTO|プロジェクトが .NET Framework 4 を対象としている場合は、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でこれを開くことができます。 他のすべてのプロジェクトは、一方向のアップグレードが必要です。|
|リッチ インターネット アプリケーション|プロジェクトをアップグレードすると、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でこれを開くことができます。|
|SharePoint 2007|Visual Studio 2013 でこのプロジェクトを開くことはできません。 ただし、プロジェクトを SharePoint 2010 に手動でアップグレードすると、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でこれを開くことができます。 SharePoint 2007 をアップグレードする方法の詳細については、「[Migrating from SharePoint 2007 to SharePoint 2010 for the IT Pro (IT プロフェッショナルのための SharePoint 2007 から SharePoint 2010 への移行)](https://channel9.msdn.com/Blogs/matthijs/Migrating-from-SharePoint-2007-to-SharePoint-2010-for-the-IT-Pro)」と「[SharePoint Enterprise Search Migration Tool for SharePoint Server 2010 (SharePoint Server 2010 用の SharePoint エンタープライズ検索移行ツール)](/previous-versions/office/developer/sharepoint-2010/ee556856(v%3Doffice.14))」をご覧ください。|
|SharePoint 2010|Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でプロジェクトを開くことができます。|
|SketchFlow|Visual Studio でプロジェクトを WPF 4.5/Silverlight 5 にアップグレードすることを許可した場合は、Visual Studio 2012 および Visual Studio 2013 でこれを開くことができます。|
|[!INCLUDE[ssKatmai_exp](../includes/sskatmai-exp-md.md)] データベース|Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でプロジェクトを開くことができます。 SQL Server の以前のバージョンで作成されたデータベース ファイル (.mdf) がある場合は、SQL Server Express LocalDB でファイルを使用する前に [!INCLUDE[sql_Denali_long](../includes/sql-denali-long-md.md)] にアップグレードする必要があります。ただし、そのデータベースはもう、SQL Server の以前のバージョンとの互換性がなくなります。 アップグレードしない場合は、同じコンピューター上に [!INCLUDE[ssKatmai_exp](../includes/sskatmai-exp-md.md)] をインストールして使用することで、Visual Studio 2013 で引き続きデータベースを使用できます。 詳細については、「[Upgrade .mdf files (.mdf ファイルのアップグレード)](../data-tools/upgrade-dot-mdf-files.md)」を参照してください。|
|[!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] Express|Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 を稼働しているコンピューター上に [!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] Express がインストールされている場合は、3 つのバージョンすべてでプロジェクトを開くことができます。|
|SQL Server レポート プロジェクト|Visual Studio 2013 および Visual Studio 2012 でプロジェクトを開くことができます。 ローカル モードの場合のみ (つまり、SQL Server に接続されていない場合)、 [!INCLUDE[vs2010](../includes/vs2010-md.md)]のビューアーに関連付けられているコントロールをデザイン時に操作することはできませんが、プロジェクトは実行時に適切に機能します。 **注意:** Visual Studio 2013 に固有の機能を追加すると、レポート スキーマが自動的にアップグレードされ、Visual Studio 2012 でプロジェクトを開くことができなくなります。|
|単体テスト|Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 で [!INCLUDE[TCMext](../includes/tcmext-md.md)] を使用して、これらのバージョンのいずれかで作成されたテストを開くことができます。|
|Visual C++|Visual Studio 2013 を使用して、Visual Studio 2012 または Visual Studio 2010 SP1 で作成された C++ プロジェクトを開くことができます。 Visual Studio 2013 ビルド環境を使用して、Visual Studio 2012 で作成されたプロジェクトをビルドする場合は、同じコンピューター上に両方のバージョンの Visual Studio がインストールされている必要があります。 詳細については、「[方法: Visual C++ プロジェクトを Visual Studio 2015 にアップグレードする](../porting/how-to-upgrade-visual-cpp-projects-to-visual-studio-2015.md)」と「[Visual C++ 移植とアップグレードのガイド](https://msdn.microsoft.com/library/f5fbcc3d-aa72-41a6-ad9a-a706af2166fb)」を参照してください。|
|Visual Studio 2010 Web|Visual Studio がプロジェクトを自動的にアップグレードすることを許可する場合は、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でこれを開くことができます。|
|Visual Studio 2010 データベース (.dbproj)|プロジェクトを SQL Server Data Tools データベース プロジェクトに変換した場合、Visual Studio 2013 でそれを開くことができます。 ただし、Visual Studio 2013 では次の成果物はサポートされていません。<br /><br /> -   単体テスト<br />-   データ生成計画<br />-   データ比較ファイル<br />-   スタティック コード分析用のカスタム規則の拡張機能<br />-   server.sqlsettings<br />-   .sqlcmd ファイル<br />-   カスタム配置の拡張機能<br />-   部分プロジェクト (.files)<br /><br /> SQL Server Data Tools をインストールすると、プロジェクトを変換した後に Visual Studio 2010 SP1 で開くことができます。 詳細については、「 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)」を参照してください。|
|Visual Studio 2010 Visual Database Tools|このプロジェクトは、Visual Studio 2013、Visual Studio 2012、Visual Studio 2010 SP1 で開くことができます。|
|Visual Studio Lab Management|[!INCLUDE[TCMext](../includes/tcmext-md.md)]、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 を使用して、これらのバージョンのいずれかで作成された環境を開くことができます。 ただし、環境を作成するには、使用している Microsoft Test Manager のバージョンが Team Foundation Server のバージョンと一致する必要があります。|
|Visual Studio マクロ|Visual Studio 2013 では、このプロジェクト タイプがサポートされていないため、このプロジェクトを開くことができません。|
|Visual Studio SDK/VSIX|Visual Studio SDK プロジェクトを Visual Studio 2013 にアップグレードした後、それを Visual Studio 2012 で開くことはできません。 詳細については、「[How to: Migrate Extensibility Projects to Visual Studio 2015 (方法: 機能拡張プロジェクトを Visual Studio 2015 に移行する)](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md)」をご覧ください。|
|Microsoft Azure Tools for Visual Studio|Microsoft Azure Tools for Visual Studio Version 2.1 を使用している場合は、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でプロジェクトを開くことができます。 以前のバージョンを対象とするプロジェクトの場合、Visual Studio でプロジェクトをバージョン2.1 にアップグレードすることを許可すると、Visual Studio 2013、Visual Studio 2012、および Visual Studio 2010 SP1 でこれを開くことができます。|
|Windows Communication Foundation、Windows Presentation Foundation|このプロジェクトは、Visual Studio 2013、Visual Studio 2012、Visual Studio 2010 SP1 で開くことができます。|
|Windows Mobile|Visual Studio 2013 では、このプロジェクト タイプがサポートされていないため、このプロジェクトを開くことができません。|
|Windows Phone 7.1|Visual Studio でプロジェクトを Windows Phone 8.0 にアップグレードすることを許可した場合は、Visual Studio 2012 および Visual Studio 2013 でこれを開くことができます。|
|その他|その他のタイプのプロジェクトのほとんどは、Visual Studio 2012、Visual Studio 2013、Visual Studio 2010 SP1 で開くことができます。|
|FrontPage Web サイト|Visual Studio 2013 では、このプロジェクト タイプがサポートされていないため、このプロジェクトを開くことができません。|
|ポータブル クラス ライブラリ|Visual Studio によるプロジェクトの自動更新を許可する場合は、Visual Studio 2013、Visual Studio 2012、または Visual Studio 2010 SP1 でこれを開くことができます。<br /><br /> -   Silverlight 4 を対象としていたプロジェクトは、Silverlight 5 を対象とするようになります。<br />-   Windows Phone 7.0 または Windows Phone 7.5 を対象としていたプロジェクトは、Windows Phone 8 を対象とするようになります。<br />-   Xbox 360 を対象としていたプロジェクトは、もう Xbox 360 を対象にしなくなります。|
|クラウド サービス プロジェクト (.ccproj 拡張子) などの Azure プロジェクト、および .deployproj 拡張子の Azure Resource Manager プロジェクト (クラウド配置プロジェクト)|これらの種類のプロジェクトを開くには、最初に [Azure SDK for .NET](https://azure.microsoft.com/downloads/)をインストールした後、プロジェクトを開きます。|

## <a name="troubleshooting-project-compatibility-issues"></a>プロジェクトの互換性の問題のトラブルシューティング
 ここでは、Visual Studio 2015 または Visual Studio 2013 でプロジェクトを開くことができない場合に実行できる、いくつかの対処方法を示します。

- Visual Studio 2015 または Visual Studio 2013 でサポートされていないプロジェクトを開こうとするときに、そのプロジェクトに関連付けられているバージョンの Visual Studio がインストールされていない場合は、そのプロジェクト タイプがサポートされていないことを示すメッセージが表示され、**[サポートされていないプロジェクト]** の下の **[プロジェクトとソリューションの変更をレビュー]** ダイアログ ボックスにそのプロジェクト タイプがリストされることがあります。 この問題を解決するには、Windows の **コントロール パネル**を開き、 **[Visual Studio]**、 **[変更]**、 **[修復]** の順に選択します。 ここで、必要なバージョンをインストールできます。

- [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)]でデスクトップ アプリのプロジェクトを開こうとすると、エラーが発生し、"このエディションの Visual Studio は、 [!INCLUDE[win81](../includes/win81-md.md)] アプリのみをサポートします。" または "このプロジェクトは、Visual Studio の現在のエディションと互換性がありません。" というメッセージが表示されます。 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] は、Windows 8.1 向けに設計された Windows ストア アプリの開発、テスト、展開用に制限されています。 デスクトップ アプリ プロジェクトを開くには、そのプロジェクトの種類をサポートしている Visual Studio のエディションを使用する必要があります。

   Visual Studio のエディションに関する詳細については、「 [Microsoft Visual Studio Products (Microsoft Visual Studio 製品)](https://visualstudio.microsoft.com/products/)」をご覧ください。

- [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] Desktop で Windows ストア アプリ プロジェクトを開こうとすると、エラーが発生します。 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)] Desktop を使用して Windows ストア アプリをビルドできません。 Windows ストア アプリをビルドするには、 [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)]をインストールします。 または、Microsoft のすべてのプラットフォームと Web 用のアプリを開発するには、Visual Studio Professional 2013 を試してください。

- Visual Studio 2013 に固有の機能がプロジェクトに必要な場合は、以前のバージョンでそのプロジェクトを開くことはできません。

- Visual Studio 2012 を使用しているときに、Visual Studio 2013 で作成されたプロジェクトを開く必要がある場合は、プロジェクト システムをカスタマイズして、Visual Studio 2013 の機能を組み込むことができる場合があります。 これを行う方法について詳しくは、「[カスタム プロジェクトでのバージョンの認識](../misc/making-custom-projects-version-aware.md)」を参照してください。

  追加のトラブルシューティング情報については、サポート技術情報の「 ["Visual Studio 2013 Compatibility (Visual Studio 2013 の互換性)](https://support.microsoft.com/help/2863286/roundtrip-issues-for-visual-studio-2012-and-visual-studio-2013-preview) 」を参照してください。

## <a name="files"></a><a name="file"></a> ファイル

次の一覧では、Visual Studio 2013 で各ファイルの種類がサポートされているかどうか、Visual Studio 2012 と Visual Studio 2010 SP1 でファイルを開くことができるかどうか、および互換性を保持するために変更を加える必要があるかどうかを確認できます。

|ファイルの種類|互換性|
|------------------|-------------------|
|AppManifest、Inbrowsersettings、OutOfBrowserSettings (.xml ファイル)|Visual Studio 2012、Visual Studio 2013、Visual Studio 2010 SP1 でこれらのファイルを開くことができます。|
|BizTalk フラット ファイル スキーマ|Visual Studio 2013 でこれらのスキーマを BizTalk 2013 プロジェクトに追加できます。 Visual Studio 2013 を、フラット ファイル スキーマを持つ BizTalk 2010 プロジェクトと組み合わせて使用するには、Visual Studio 2013 があるコンピューターに BizTalk 2013 をインストールします。 BizTalk 2010 プロジェクトは、最初に開いたときに自動的に BizTalk 2013 または Visual Studio 2013 プロジェクト システムにアップグレードされます。|
|クライアント レポート定義 (.rdlc) ファイル|これらのファイルは Visual Studio 2013 で開くことができます。Visual Studio 2013 の機能やコントロールを追加すると、スキーマが自動的にアップグレードされます。|
|コード分析規則セット|Visual Studio 2012、Visual Studio 2013、Visual Studio 2010 SP1 でこれらのファイルを開くことができます。|
|データ層アプリケーション パッケージ ファイル|これらのファイルがバージョン 2.0 またはバージョン 2.5 の場合は、Visual Studio 2013 で開くことができます。|
|デバッガー ダンプ ファイル|Visual Studio 2012、Visual Studio 2013、Visual Studio 2010 SP1 でこれらのファイルを開くことができます。|
|Directed Graph Markup Language (DGML) 図ファイル|ファイルを変更することなく、Visual Studio 2012、Visual Studio 2013、Visual Studio 2010 SP1 でこれらのファイルを開くことができます。|
|エンティティ データ モデル (EDMX) ファイル|Visual Studio 2013 では、ファイルを変更せずに、.NET Framework 4.5 または .NET Framework 4 を対象とする EDMX ファイルを開くことができます。|
|プロファイラー レポート ファイル|プロファイラー レポート ファイル (.vsp、.vsps、.psess、および .vspf) は、Visual Studio 2012 および Visual Studio 2013 で開くことができます。 .vspx ファイルを Visual Studio 2010 SP1 で開くことはできません。|
|ソリューション (.suo) ファイル|Visual Studio 2013 を使用して、Visual Studio 2012 または Visual Studio 2010 SP1 で作成されたソリューション ファイルを開くことができます|
|SQL Server Compact Edition|Visual Studio 2013 では、SQL Server Compact エディションはサポートされていません。|
|SQLX ファイル|Visual Studio 2013 でこれらのファイルを開くには、一方向のアップグレードを実行し、対象バージョンの Visual Studio で .sqlx ファイルを配置した後、ファイルを .dacpac 形式でリビルドする必要があります。|
|[!INCLUDE[vs2010](../includes/vs2010-md.md)] の IntelliTrace ログ ファイル|Visual Studio 2012、Visual Studio 2013、Visual Studio 2010 SP1 でこれらのファイルを開くことができます。|
|JavaScript メモリ アナライザー (.diagsession) ファイル|以前のバージョンの Visual Studio で作成されたファイルは、Visual Studio 2013 で表示できます。 ただし、収集された情報によっては、Visual Studio 2013 で作成されたファイルを Visual Studio 2012 または Visual Studio 2010 SP1 で開くことができない場合があります。|

## <a name="integration-assets"></a><a name="integration"></a> 統合資産

Visual Studio Team Foundation Server の異なるバージョンのクライアントおよびサーバーを使用する場合は、互換性の問題が発生する可能性があります。

|統合の種類|互換性|
|-------------------------|-------------------|
|コード レビューおよび担当作業|[!INCLUDE[esprfound](../includes/esprfound-md.md)] クライアントを [!INCLUDE[vstsTfsRosarioLong](../includes/vststfsrosariolong-md.md)]に接続した場合は、コード レビュー機能および担当作業機能を使用できません。|
|[!INCLUDE[vs_dev11_expwin_long](../includes/vs-dev11-expwin-long-md.md)]|MSBuild や [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] などの 64 ビット環境を使用して、 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] で作成した [!INCLUDE[vs_dev12_expwin](../includes/vs-dev12-expwin-md.md)]アプリをビルドすることはできません。|

## <a name="see-also"></a>関連項目

- [カスタム プロジェクトでのバージョンの認識](../misc/making-custom-projects-version-aware.md)
