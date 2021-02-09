---
title: Office プライマリ相互運用機能アセンブリ
description: プライマリ相互運用機能アセンブリ (PIA) を使用して、Office プロジェクトから Microsoft Office アプリケーションの機能にアクセスする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies
- assemblies [Office development in Visual Studio], primary interop assemblies
- Office primary interop assemblies
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2041c1d8b39f88f611cee09f17c498ea54130122
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892061"
---
# <a name="office-primary-interop-assemblies"></a>Office プライマリ相互運用機能アセンブリ

Office プロジェクトから Microsoft Office アプリケーションの機能を使用するには、アプリケーションのプライマリ相互運用機能アセンブリ (PIA: Primary Interop Assembly) を使用することが必要です。 PIA によって、Microsoft Office アプリケーションの COM ベースのオブジェクト モデルと対話するマネージド コードを作成できるようになります。

[!include[Add-ins note](includes/addinsnote.md)]

新しい Office プロジェクトを作成すると、Visual Studio により、そのプロジェクトのビルドに必要な PIA への参照が追加されます。 場合によっては、その他の PIA への参照を追加することが必要になります (たとえば、Microsoft Office Excel 用のプロジェクトで Microsoft Office Word の機能を使用する場合など)。

このトピックでは、Office プロジェクトでの Microsoft Office PIA の使用に関する次の側面について説明します。

- [プロジェクトをビルドおよび実行するためのプライマリ相互運用機能アセンブリの分離](#separateassemblies)

- [1つのプロジェクトで複数の Microsoft Office アプリケーションの機能を使用する](#usingfeatures)

- [Microsoft Office アプリケーション プライマリ相互運用機能アセンブリの完全な一覧](#pialist)

プライマリ相互運用機能アセンブリの詳細については、「 [プライマリ相互運用機能アセンブリ](/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))」を参照してください。

<a name="separateassemblies"></a>

## <a name="separate-primary-interop-assemblies-to-build-and-run-projects"></a>プロジェクトをビルドおよび実行するためのプライマリ相互運用機能アセンブリの分離

Visual Studio では、開発用コンピューターで PIA のさまざまなセットを使用します。 これらのアセンブリ セットは、次の場所に配置されます。

- Program files ディレクトリ内のフォルダー

  これらのアセンブリのコピーは、コードを記述してプロジェクトをビルドするときに使用されます。 これらのアセンブリは、Visual Studio によって自動的にインストールされます。

- グローバルアセンブリキャッシュ

  これらのアセンブリのコピーは、プロジェクトの実行やデバッグを行うときなど、一部の開発タスクで使用されます。 これらのアセンブリのインストールと登録は、Visual Studio では行われません。手動で行う必要があります。

### <a name="primary-interop-assemblies-in-the-program-files-directory"></a>Program files ディレクトリ内のプライマリ相互運用機能アセンブリ

Visual Studio をインストールすると、ファイル システム内の場所 (グローバル アセンブリ キャッシュ外部) に PIA が自動的にインストールされます。 新しいプロジェクトを作成すると、Visual Studio により、これらの PIA のコピーへの参照がプロジェクトに自動的に追加されます。 Visual Studio は、グローバル アセンブリ キャッシュ内のアセンブリではなく、これらの PIA のコピーを使用して、プロジェクトの開発やビルドを行うときに型参照を解決します。

PIA のコピーを使用することで、Visual Studio は、異なるバージョンの PIA がグローバル アセンブリ キャッシュに登録されている場合に発生することのある開発上の問題を回避できます。

Visual Studio 2017 以降では、これらの Pia のコピーは、開発用コンピューター上の次の共有場所にインストールされます。

- `%ProgramFiles%\Microsoft Visual Studio\Shared\Visual Studio Tools for Office\PIA\`

- (または `%ProgramFiles(x86)%\Microsoft Visual Studio\Shared\Visual Studio Tools for Office\PIA\` 64 ビットオペレーティングシステム)

> [!NOTE]
> 以前のバージョンの Visual Studio では、これらの Pia は、 `%ProgramFiles%` そのバージョンの Visual studio のフォルダーの下にある Office\PIA フォルダーの Visual Studio Tools にインストールされます。
> 例えば： `%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Visual Studio Tools for Office\PIA\`

### <a name="primary-interop-assemblies-in-the-global-assembly-cache"></a>グローバルアセンブリキャッシュ内のプライマリ相互運用機能アセンブリ

開発タスクを実行するには、開発用コンピューターのグローバル アセンブリ キャッシュに PIA をインストールし、登録する必要があります。 通常、開発用コンピューターに Office をインストールすると、自動的に PIA がインストールされます。 詳細については、「 [Office ソリューションを開発するためのコンピューターの構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

Office PIA は、 Office ソリューションを実行するエンド ユーザーのコンピューターには必要ありません。 詳細については、「 [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

<a name="usingfeatures"></a>

## <a name="use-features-of-multiple-microsoft-office-applications-in-a-single-project"></a>1つのプロジェクトで複数の Microsoft Office アプリケーションの機能を使用する

Visual Studio の各 Office プロジェクト テンプレートは、単一の Microsoft Office アプリケーションと連動するようになっています。 複数の Microsoft Office アプリケーションの機能を使用したり、Visual Studio 内にプロジェクトが含まれないアプリケーションやコンポーネントの機能を使用したりするには、必要な PIA への参照を追加しなければなりません。

ほとんどの場合、ディレクトリの下に Visual Studio によってインストールされた Pia への参照を追加する必要があり `%ProgramFiles(x86)%\Microsoft Visual Studio\Shared\Visual Studio Tools for Office\PIA\` ます。 これらのバージョンのアセンブリは、[**参照マネージャー** ] ダイアログボックスの [**フレームワーク**] タブに表示されます。 詳細については、「 [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)」を参照してください。

グローバル アセンブリ キャッシュに PIA をインストールして登録すると、これらのバージョンのアセンブリは、 **[参照マネージャー]** ダイアログ ボックスの **[COM]** タブに表示されます。 これらのバージョンのアセンブリを使用すると開発上の問題が発生するため、これらのアセンブリに参照を追加することは避ける必要があります。 たとえば、異なるバージョンの PIA がグローバル アセンブリ キャッシュに登録されている場合、 **[参照マネージャー]** ダイアログ ボックスの **[COM]** タブで別のバージョンのアセンブリを指定しても、プロジェクトは最後に登録されたバージョンのアセンブリにバインドします。

> [!NOTE]
> アセンブリによっては、参照元のアセンブリを追加すると、参照先のアセンブリも自動的に追加される場合があります。 たとえば、およびアセンブリへの参照は、 `Office.dll` `Microsoft.Vbe.Interop.dll` Word、Excel、Outlook、Microsoft Forms、または Graph アセンブリへの参照を追加すると、自動的に追加されます。

<a name="pialist"></a>

## <a name="primary-interop-assemblies-for-microsoft-office-applications"></a>Microsoft Office アプリケーションのプライマリ相互運用機能アセンブリ

次の表に、、、およびで使用できるプライマリ相互運用機能アセンブリの一覧を示し [!INCLUDE[Office_16_short](../vsto/includes/office-16-short-md.md)] [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] ます。

<br/>

|Office アプリケーションまたはコンポーネント|プライマリ相互運用機能アセンブリの名前|
|-------------------------------------|-----------------------------------|
|Microsoft Access 14.0 Object Library<br /><br /> Microsoft Access 15.0 Object Library|Microsoft.Office.Interop.Access.dll|
|Microsoft Office 14.0 Access Database Engine Object Library<br /><br /> Microsoft Office 15.0 Access Database Engine Object Library|Microsoft.Office.Interop.Access.Dao.dll|
|Microsoft Excel 14.0 Object Library<br /><br /> Microsoft Excel 15.0 Object Library|[Microsoft.Office.Interop.Excel.dll](/dotnet/api/microsoft.office.interop.excel?view=excel-pia&preserve-view=true)|
|Microsoft Graph 14.0 Object Library (PowerPoint、Access、および Word のグラフで使用)<br /><br /> Microsoft Graph 15.0 Object Library|Microsoft.Office.Interop.Graph.dll|
|Microsoft InfoPath 2.0 Type Library (InfoPath 2007 専用)|[Microsoft.Office.Interop.InfoPath.dll](/dotnet/api/microsoft.office.interop.infopath?view=infopath-form&preserve-view=true)|
|Microsoft InfoPath XML 相互運用機能アセンブリ (InfoPath 2007 専用)|Microsoft.Office.Interop.InfoPath.Xml.dll|
|Microsoft Office 14.0 Object Library (Office の共有機能)<br /><br /> Microsoft Office 15.0 Object Library (Office の共有機能)|office.dll|
|Microsoft Office Outlook View Control (受信トレイにアクセスする Web ページおよびアプリケーションで使用可能)|Microsoft.Office.Interop.OutlookViewCtl.dll|
|Microsoft Outlook 14.0 Object Library<br /><br /> Microsoft Outlook 15.0 Object Library|[Microsoft.Office.Interop.Outlook.dll](/dotnet/api/microsoft.office.interop.outlook?view=outlook-pia&preserve-view=true)|
|Microsoft PowerPoint 14.0 Object Library<br /><br /> Microsoft PowerPoint 15.0 Object Library|Microsoft.Office.Interop.PowerPoint.dll|
|Microsoft Project 14.0 Object Library<br /><br /> Microsoft Project 15.0 Object Library|[Microsoft.Office.Interop.MSProject.dll](/dotnet/api/microsoft.office.interop.msproject?view=office-project-server&preserve-view=true)|
|Microsoft Publisher 14.0 Object Library<br /><br /> Microsoft Publisher 15.0 Object Library|Microsoft.Office.Interop.Publisher.dll|
|Microsoft SharePointDesigner 14.0 Web Object Reference Library|Microsoft.Office.Interop.SharePointDesigner.dll|
|Microsoft SharePointDesigner 14.0 Page Object Reference Library|Microsoft.Office.Interop.SharePointDesignerPage.dll|
|Microsoft スマートタグ2.0 タイプライブラリ **メモ:**  スマートタグは、およびで非推奨とされ [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)] ます。|Microsoft.Office.Interop.SmartTag.dll|
|Microsoft Visio 14.0 Type Library<br /><br /> Microsoft Visio 15.0 Type Library|Microsoft.Office.Interop.Visio.dll|
|Microsoft Visio 14.0 Save As Web Type Library<br /><br /> Microsoft Visio 15.0 Save As Web Type Library|Microsoft.Office.Interop.Visio.SaveAsWeb.dll|
|Microsoft Visio 14.0 Drawing Control Type Library<br /><br /> Microsoft Visio 15.0 Drawing Control Type Library|Microsoft.Office.Interop.VisOcx.dll|
|Microsoft Word 14.0 Object Library<br /><br /> Microsoft Word 15.0 Object Library|[Microsoft.Office.Interop.Word.dll](/dotnet/api/microsoft.office.interop.word?view=word-pia&preserve-view=true)|
|Microsoft Visual Basic for Applications Extensibility 5.3|Microsoft.Vbe.Interop.dll|

### <a name="binding-redirect-assemblies"></a>バインドリダイレクトアセンブリ

グローバル アセンブリ キャッシュに (Office と共に、または PIA の再頒布可能パッケージをインストールすることにより) Office PIA をインストールし、登録すると、同時にバインディング リダイレクト アセンブリがグローバル アセンブリ キャッシュだけにインストールされます。 これらのアセンブリは、実行時にプライマリ相互運用機能アセンブリの正しいバージョンが読み込まれるようにするのに役立ちます。

たとえば、 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] アセンブリを参照するソリューションが、同じプライマリ相互運用機能アセンブリの [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] バージョンがあるコンピューターで実行されると、バインド リダイレクト アセンブリによって、そのプライマリ相互運用機能アセンブリの [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] バージョンを読み込むように [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] ランタイムに指示されます。

詳細については、「 [方法: 自動バインドリダイレクトを有効または無効](/dotnet/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection)にする」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Excel オブジェクトモデルの概要](../vsto/excel-object-model-overview.md)
- [InfoPath ソリューション](../vsto/infopath-solutions.md)
- [Outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)
- [PowerPoint ソリューション](../vsto/powerpoint-solutions.md)
- [プロジェクトソリューション](../vsto/project-solutions.md)
- [Visio オブジェクトモデルの概要](../vsto/visio-object-model-overview.md)
- [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)
- [Visual Studio での Office 開発に関する一般的なリファレンス &#40;&#41;](../vsto/general-reference-office-development-in-visual-studio.md)
