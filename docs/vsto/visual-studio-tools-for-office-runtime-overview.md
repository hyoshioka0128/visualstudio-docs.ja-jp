---
title: Visual Studio Tools for Office ランタイムの概要
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio], about Office runtime
- VSTOLoader.dll
- runtime loader [Office development in Visual Studio]
- Office runtime [Office development in Visual Studio], assemblies
- Office runtime [Office development in Visual Studio]
- runtime [Office development in Visual Studio], assemblies
- vstoee.dll
- Visual Studio Tools for Office runtime
- Office solutions [Office development in Visual Studio], runtime
- solutions [Office development in Visual Studio], runtime
- versions [Office development in Visual Studio], runtime
- assemblies [Office development in Visual Studio], runtime
- runtime [Office development in Visual Studio], about VSTO runtime
- solution loader [Office development in Visual Studio]
- runtime [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 31d2244796282aaad56011d5b9963232d3438ce9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "71253983"
---
# <a name="visual-studio-tools-for-office-runtime-overview"></a>Visual Studio Tools for Office ランタイムの概要
  Visual Studio の Microsoft Office 開発者ツールを使用して作成されたソリューションを実行するには、エンドユーザーのコンピューターに Visual Studio 2010 Tools for Office runtime をインストールする必要があります。 詳細については、「 [方法: Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストール](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)する」を参照してください。 Visual Studio 2010 Tools for Office runtime は、次の2つの主要コンポーネントで構成されています。

- .NET Framework 用の Office 拡張機能。 これらのコンポーネントは、ソリューションと Microsoft Office アプリケーションの間の通信レイヤーとなるマネージド アセンブリです。 詳細については、「 [.NET Framework 用の Office 拡張機能に](#officeextensions)ついて」を参照してください。

- Office ソリューション ローダー。 このコンポーネントは、Office アプリケーションがランタイムおよびソリューションの読み込みに使用する一連のアンマネージ DLL です。 詳細については、「 [Office ソリューションローダーに](#UnmanagedLoader)ついて」を参照してください。

  ランタイムをインストールする方法はいくつかあります。 ランタイムをインストールするときには、コンピューターの構成に応じて異なるランタイム コンポーネントがインストールされます。 詳細については、「 [Visual Studio Tools for Office ランタイムのインストールシナリオ](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)」を参照してください。

## <a name="understand-the-office-extensions-for-the-net-framework"></a><a name="officeextensions"></a> .NET Framework 用の Office 拡張機能について
 Visual Studio 2010 Tools for Office runtime には、.NET Framework 3.5 (以降) 用の Office 拡張機能が含まれてい [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ます。 .NET Framework の各バージョンを対象とするソリューションでは、そのバージョンに適した拡張機能が使用されます。

 これらの拡張機能は、ソリューションが Office アプリケーションの自動化および拡張に使用するアセンブリで構成されています。 Office プロジェクトを作成すると、Visual Studio によって、そのプロジェクト タイプおよびプロジェクトの対象 .NET Framework に使用するアセンブリへの参照が自動的に追加されます。 Office 拡張機能のアセンブリの詳細については、「 [Visual Studio Tools for Office ランタイムのアセンブリ](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)」を参照してください。

### <a name="design-differences-in-the-office-extensions"></a>Office 拡張機能の設計の相違点
 .NET Framework 3.5 用の Office 拡張機能で使用する型の大部分は、クラスです。 これらのクラスは、以前のバージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]に含まれていたクラスと同じです。 これに対して、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能で使用する型の大部分は、インターフェイスです。 たとえば、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする場合、 <xref:Microsoft.Office.Tools.Excel.Worksheet> と <xref:Microsoft.Office.Tools.Word.Document> の型はクラスではなくインターフェイスです。

 ほとんどの場合、ソリューションが .NET Framework 3.5 を対象とするかまたは [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]を対象とするかに関係なく、Office ソリューションで記述するコードは同じです。 ただし、一部の機能については、対象となる .NET Framework のバージョンが異なる場合に別のコードが必要になります。 詳細については、「 [.NET Framework 4 以降への Office ソリューションの移行](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)」を参照してください。

### <a name="interfaces-in-the-office-extensions-for-the-net-framework-4-or-later"></a>.NET Framework 4 以降用の Office 拡張機能のインターフェイス
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能に含まれるインターフェイスの大部分は、ユーザー コードで実装されることを意図していません。 直接実装できるインターフェイスは、 **I**という文字で始まる名前の付いたインターフェイスです。たとえば、 <xref:Microsoft.Office.Tools.Excel.ISmartTagExtension>などです。

 文字 **I** で始まらないすべてのインターフェイスは、Visual Studio 2010 Tools for Office runtime によって内部的に実装されます。これらのインターフェイスは、今後のリリースで変更される可能性があります。 これらのインターフェイスを実装するオブジェクトを作成するには、プロジェクトで `Globals.Factory` オブジェクトによって提供されるメソッドを使用します。 たとえば、<xref:Microsoft.Office.Tools.Excel.SmartTag> インターフェイスを実装するオブジェクトを取得するには、`Globals.Factory.CreateSmartTag` メソッドを使用します。 の詳細について `Globals.Factory` は、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

### <a name="enable-type-equivalence-and-embedded-types-in-projects-that-target-the-net-framework-4-or-later"></a>.NET Framework 4 以降を対象とするプロジェクトでの型の等価性と埋め込み型の有効化
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能のオブジェクト モデルはインターフェイスに基づいているため、Visual Studio の Visual C# および Visual Basic の両方で、型の等価性の機能を使用して [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] から取得した型情報をソリューションに埋め込むことができます。 この機能によって、Office ソリューションおよび [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] が、それぞれ独立してバージョン管理できるようになります。 たとえば、ソリューションで <xref:Microsoft.Office.Tools.Word.Document> インターフェイスを埋め込み型として使用し、ランタイムの次のバージョンによって <xref:Microsoft.Office.Tools.Word.Document> インターフェイスにメンバーが追加される場合でも、そのソリューションは引き続きランタイムの次のバージョンで機能します。 ソリューションで <xref:Microsoft.Office.Tools.Word.Document> インターフェイスを埋め込み型として使用しない場合、そのソリューションはランタイムの次のバージョンで機能しません。

 既定では、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする Office プロジェクトを作成するときに、型の等価性の機能は有効になりません。 この機能を有効にするには、プロジェクト内の次のアセンブリ参照の **相互運用型の埋め込み** プロパティを **True**に設定します。

- Microsoft.Office.Tools.dll

- Microsoft.Office.Tools.Common.dll

- Microsoft.Office.Tools.Excel.dll

- Microsoft.Office.Tools.Outlook.dll

- Microsoft.Office.Tools.Word.dll

  この変更を加えると、プロジェクトをビルドするときに、プロジェクトが使用するすべてのランタイム型の型情報が、ソリューション アセンブリに埋め込まれます。 実行時には、参照されるアセンブリの型情報ではなく、この埋め込み型情報がソリューションで使用されます。

## <a name="understand-the-office-solution-loader"></a><a name="UnmanagedLoader"></a> Office ソリューションローダーについて
 Visual Studio Tools for Office Runtime には、Office アプリケーションがランタイムおよび Office ソリューションの読み込みに使用する複数のアンマネージ DLL が含まれています。 これらの DLL を直接操作する必要が生じることはありませんが、その目的を把握しておくと、Office ソリューションのアーキテクチャについて理解を深めるうえで役に立ちます。

 読み込みプロセス中のこれらのコンポーネントの使用方法の詳細については、「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md) 」および「 [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

### <a name="vstoeedll"></a>vstoee.dll
 ユーザーがドキュメントレベルのカスタマイズを開いたり VSTO アドインを起動したりすると、Office アプリケーションは *VSTOEE.dll* を呼び出して、の読み込みに必要なタスクを実行し [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。

 *VSTOEE.dll* によって、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ソリューションおよびインストールされている Office のバージョンに適したバージョンのが読み込まれます。 複数のバージョンのを [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 同じコンピューターにインストールすることはできますが、 *VSTOEE.dll* のインスタンスは一度に1つしかインストールされません。 これは、コンピューターにインストールされているランタイムの最新バージョンに含まれていた *VSTOEE.dll* です。 他のソリューションで使用できるのさまざまなバージョンの詳細については [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 、「 [異なるバージョンの Microsoft Office でのソリューションの実行](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)」を参照してください。

### <a name="vstoloaderdll"></a>VSTOLoader.dll
 *VSTOEE.dll*が適切なバージョンのを読み込んだ後 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 、 *VSTOLoader.dll*は、ソリューションアセンブリの読み込みに必要なほとんどの作業を実行します。 *VSTOLoader.dll* はいくつかのことを行います。

- ソリューション アセンブリごとにアプリケーション ドメインを作成します。

- 一連のセキュリティ チェックによって、ソリューション アセンブリに実行のアクセス許可があることを確認します。

- ソリューションに必要な .NET Framework 用のバージョンの Office 拡張機能を読み込みます。

  また、 *VSTOLoader.dll* VSTO アドインに固有のいくつかの処理も行います。

- <xref:Extensibility.IDTExtensibility2> インターフェイスを実装します。 <xref:Extensibility.IDTExtensibility2> は、Microsoft Office アプリケーションのすべての VSTO アドインが実装する必要のある COM インターフェイスです。 このインターフェイスには、アプリケーションが VSTO アドインと通信するために呼び出すメソッドが定義されています。

- IManagedAddin インターフェイスを実装します。 このインターフェイスは、VSTO アドインを読み込むために Office アプリケーションによって使用されます。詳細については、「 [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)」を参照してください。

## <a name="understand-the-32-bit-and-64-bit-versions-of-the-runtime"></a>32ビットバージョンと64ビットバージョンのランタイムについて
 Visual Studio 2010 Tools for Office runtime には、64ビット版と32ビット版の別個のバージョンがあります。 ランタイムのこれらのバージョンは、64 ビット エディションおよび 32 ビット エディションの Office でソリューションを実行するのに使用されます。 次の表は、Windows と Office のそれぞれの組み合わせで必要とされる、ランタイムのバージョンを示しています。

|Windows のエディション|Microsoft Office のエディション|Visual Studio Tools for Office Runtime のバージョン番号|
|------------------------|---------------------------------|--------------------------------------------------------------------|
|32 ビット|32 ビット|32 ビット|
|64 ビット|32 ビット|64 ビット|
|64 ビット|64 ビット|64 ビット|

 Office をインストールするときに、必要なバージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] が Office と共にインストールされます。 たとえば、64 ビット エディションの Office を 64 ビット バージョンの Windows にインストールすると、64 ビット バージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] もインストールされます。 Office を使用したのインストールの詳細につい [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ては、「 [Visual Studio Tools for Office ランタイムのインストールシナリオ](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)」を参照してください。

 64 ビット バージョンの Office は、Visual Studio 2008 で 2007 Microsoft Office system 用のプロジェクト テンプレートを使用して作成された Office ソリューションも実行できます。 ただし、Visual Studio 2008 で Microsoft Office 2003 用のプロジェクト テンプレートを使用して作成された Office ソリューションや、Visual Studio 2005 を使用して作成された Office ソリューションは実行できません。 詳細については、「 [異なるバージョンの Microsoft Office でのソリューションの実行](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)」を参照してください。

## <a name="repair-the-visual-studio-2010-tools-for-office-runtime"></a>Visual Studio 2010 Tools for Office runtime の修復
 ランタイムを修復する必要がある場合は、[コントロール パネル] の **[プログラムと機能]** または **[プログラムの追加と削除]** を開き、プログラムの一覧から **[Microsoft Visual Studio 2010 Tools for Office Runtime]** をクリックし、 **[アンインストール]** をクリックします。 実行されるセットアップ プログラムを使用して、ランタイムを修復できます。 **[変更]** をクリックした場合、ランタイムを修復するオプションは表示されません。

## <a name="see-also"></a>関連項目
- [Visual Studio Tools for Office ランタイムのインストールシナリオ](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [Visual Studio Tools for Office ランタイムのアセンブリ](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)
- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office ソリューションのアップグレードと移行](../vsto/upgrading-and-migrating-office-solutions.md)
