---
title: SharePoint ツール拡張機能のプログラミングモデルの概要
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio, extending tools
- SharePoint development in Visual Studio, extensibility object models
- SharePoint development in Visual Studio, extending tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d2f7b56b372f1f083b441a5d3e6045ffc7aff7ed
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585733"
---
# <a name="overview-of-the-programming-model-of-sharepoint-tools-extensions"></a>SharePoint ツール拡張機能のプログラミング モデルの概要
  Visual Studio で SharePoint ツールの拡張機能を作成する場合、SharePoint ツールによって公開される 1 つ以上の機能拡張インターフェイスを実装することから始めます。 ほとんどの場合、SharePoint ツールによって提供される他の型も使用して、拡張機能で機能を実装します。 一部のシナリオでは、Visual Studio および SharePoint によって提供される他のオブジェクト モデルに含まれる型も使用します。 これらの各オブジェクト モデルの用途と、これらを組み合わせて使用して SharePoint ツールの拡張機能を作成する方法を理解する必要があります。

## <a name="extend-the-sharepoint-tools-by-implementing-extensibility-interfaces"></a>機能拡張インターフェイスを実装して SharePoint ツールを拡張する
 Visual Studio は、.NET Framework 4 の Managed Extensibility Framework (MEF) を使用して SharePoint ツールの機能拡張モデルを提供します。 MEF は、アプリケーションが機能拡張ポイントを公開したり、実行時に拡張機能を検出し、読み込んだりできるようにする (System.ComponentModel.Composition アセンブリで実装される) API です。 MEF の詳細については、「 [Managed Extensibility Framework &#40;mef&#41;](/dotnet/framework/mef/index)」を参照してください。

 SharePoint ツールを拡張するには、Visual Studio によって公開される 1 つ以上の機能拡張インターフェイスを実装します。 <xref:System.ComponentModel.Composition.ExportAttribute>、および必要に応じて SharePoint ツール固有のその他の属性をインターフェイスの実装に適用する必要もあります。 次の表に、SharePoint ツールを拡張するために実装できるインターフェイスを示します。

|インターフェイス|説明|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>|このインターフェイスは、新しい種類の SharePoint プロジェクト項目を定義する際に実装します。 例については、「 [方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>|このインターフェイスは、Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類を拡張する場合に実装します。 例については、「 [方法: SharePoint プロジェクト項目の拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)する」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>|このインターフェイスは、SharePoint プロジェクトを拡張する場合に実装します。 例については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep>|SharePoint プロジェクト項目を配置または取り消すときに実行できる新しい配置手順を定義するには、このインターフェイスを実装します。 例については、「 [チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成する](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>|このインターフェイスを実装して、[**サーバーエクスプローラー** ] ウィンドウの [ **SharePoint 接続**] ノードの下にある既存のノードを拡張します。 例については、「 [方法: サーバーエクスプローラーで SharePoint ノードを拡張](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)する」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider>|このインターフェイスを実装して、[**サーバーエクスプローラー** ] ウィンドウの [ **SharePoint 接続**] ノードの下に新しい種類のノードを定義します。 例については、「 [方法: サーバーエクスプローラーで SharePoint ノードを拡張](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)する」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule>|カスタムのフィーチャー検証規則を定義するには、このインターフェイスを実装します。 例については、「 [方法: SharePoint ソリューションのカスタム機能およびパッケージ検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule>|カスタムのパッケージ検証規則を定義するには、このインターフェイスを実装します。 例については、「 [方法: SharePoint ソリューションのカスタム機能およびパッケージ検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。|

 SharePoint ツールの拡張機能を実装したら、拡張機能アセンブリを Visual Studio 拡張機能 (VSIX) のパッケージに配置し、Visual Studio が拡張機能を検出し、読み込むことができるようにする必要があります。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="understand-the-object-models-that-you-use-in-sharepoint-tools-extensions"></a>SharePoint ツールの拡張機能で使用するオブジェクトモデルについて
 SharePoint ツールの拡張機能を作成するときに使用できるいくつかのオブジェクト モデルを次に示します。

- *SharePoint ツールオブジェクトモデル*。 このオブジェクト モデルには、SharePoint ツールの拡張機能を作成するために実装する機能拡張インターフェイスと、その他の関連する型が用意されています。

- *Visual Studio のオートメーションと統合オブジェクトモデル*。 これらのオブジェクト モデルを使用して、SharePoint ツールのオブジェクト モデルの範囲を超える Visual Studio の機能にアクセスします。

    > [!NOTE]
    > SharePoint ツールのオブジェクト モデルに存在するいくつかのオブジェクトは、SharePoint プロジェクト サービスを使用して、Visual Studio のオートメーション オブジェクト モデルおよび Visual Studio の統合オブジェクト モデルのオブジェクトに変換できます。それとは逆方向の変換も可能です。 詳細については、「 [SharePoint プロジェクトシステムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)」を参照してください。

- *SharePoint サーバーとクライアントオブジェクトモデル*。 これらのオブジェクト モデルを使用して、SharePoint サイトに変更を加えたり、SharePoint ツールの拡張機能のコンテキストから SharePoint サイトのデータを取得したりします。

### <a name="sharepoint-tools-object-model"></a>SharePoint ツールオブジェクトモデル
 SharePoint ツールの各拡張機能では、SharePoint ツールのオブジェクト モデルの型を使用して、拡張機能の主要な動作と機能が定義されます。 次の表は、このオブジェクトモデルに含まれる名前空間を含むアセンブリを示しています。

#### <a name="microsoftvisualstudiosharepointdll"></a>Microsoft.VisualStudio.SharePoint.dll

|名前空間|説明|
|-|-|
|<xref:Microsoft.VisualStudio.SharePoint>|SharePoint プロジェクト システムを拡張および自動化するために使用する型があります。 たとえば、組み込みの SharePoint プロジェクトやプロジェクト項目を拡張できるほか、独自のプロジェクト項目を作成することもできます。 詳細については、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Deployment>|独自の配置手順や配置構成の作成など、SharePoint プロジェクトの配置プロセスを拡張するために使用する型があります。 詳細については、「 [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Explorer>|[**サーバーエクスプローラー** ] ウィンドウの [ **SharePoint 接続**] ノードの下のノードを拡張したり、新しい種類のノードを定義したりするために使用する型が含まれています。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.Features>|SharePoint プロジェクトのフィーチャーの定義にアクセスするために使用する型があります。|
|<xref:Microsoft.VisualStudio.SharePoint.Packages>|SharePoint ソリューションのパッケージ定義にアクセスするために使用する型があります。|
|<xref:Microsoft.VisualStudio.SharePoint.Validation>|SharePoint プロジェクトの機能およびパッケージ検証動作をカスタマイズするために使用する型があります。 詳細については、「[方法:SharePoint ソリューションのフィーチャーとパッケージのカスタム検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。|

#### <a name="microsoftvisualstudiosharepointcommandsdll"></a>Microsoft.VisualStudio.SharePoint.Commands.dll

|名前空間|説明|
|-|-|
|<xref:Microsoft.VisualStudio.SharePoint.Commands>|カスタム *SharePoint コマンド*の作成に使用できる型が含まれています。 SharePoint コマンドは、SharePoint のサーバー オブジェクト モデルに対する呼び出しを SharePoint ツールの拡張機能から行うメソッドです。 詳細については、「 [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。|

#### <a name="microsoftvisualstudiosharepointexplorerextensionsdll"></a>Microsoft.VisualStudio.SharePoint.Explorer.Extensions.dll

|名前空間|説明|
|-|-|
|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions>|リスト、フィールド、コンテンツタイプを表すノードなど、SharePoint サイト上の個々のコンポーネントを表す組み込み **サーバーエクスプローラー** ノードに関する情報を取得するために使用できる型が含まれています。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。|

### <a name="visual-studio-automation-object-model"></a>Visual Studio オートメーションオブジェクトモデル
 Visual Studio のオートメーション オブジェクト モデルには、Visual Studio のプロジェクトおよび IDE を自動化するために使用できる API が用意されています。 SharePoint プロジェクトに限定されないプロジェクト関連のタスクや、Visual Studio の全般的なオートメーション タスクを実行するには、Visual Studio のオブジェクト モデルを使用します。 このオブジェクト モデルは、以前から Visual Studio のアドインやマクロで使用されていましたが、SharePoint ツールの拡張機能で使用することもできます。

 Visual Studio オートメーションオブジェクトモデルの主要な部分は、 *EnvDTE.dll* アセンブリで定義されています。 *EnvDTE \\ \<version> *アセンブリは、Visual Studio の特定のバージョンで導入された追加機能を提供します。 これらのアセンブリは、Visual Studio に属しています。

 オートメーションオブジェクトモデルの詳細については、「 [Visual STUDIO SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)」を参照してください。

### <a name="visual-studio-integration-object-model"></a>Visual Studio の統合オブジェクトモデル
 統合オブジェクトモデルには、 *VSPackage*を作成することによって Visual Studio に機能を追加するために使用できる api が用意されています。 VSPackage は、カスタム機能 (ツール ウィンドウ、エディター、デザイナー、サービス、プロジェクトなど) を提供することによって Visual Studio IDE を拡張するモジュールです。

 組み込みの SharePoint ツールと組み合わせて使用する新しい Visual Studio 機能を追加するには、統合オブジェクト モデルを使用します。 たとえば、SharePoint サイトのカスタム動作を表すカスタム SharePoint プロジェクト項目を作成する場合、そのカスタム動作のデザイナーを実装する VSPackage を作成することもできます。 **ソリューションエクスプローラー**のカスタム動作を表すプロジェクト項目にショートカットメニュー項目を追加することにより、デザイナーをカスタム動作に関連付けることができます。 デザイナーを開くには、ショートカットメニューを開きます (カスタム動作プロジェクト項目を右クリックするか、[カスタム動作] プロジェクト項目を選択して選択し、 **Shift** + **F10**キーを押します)。次に、[**開く**] を選択します。

 このオブジェクト モデルは、Visual Studio SDK に付属の一連のアセンブリで定義されています。 このオブジェクトモデルの主なアセンブリには、 *Microsoft.VisualStudio.Shell.11.0.dll*、 *Microsoft.VisualStudio.Shell.Interop.dll*、 *Microsoft.VisualStudio.OLE.Interop.dll*があります。

 統合オブジェクトモデルの詳細については、「 [オートメーションモデルの概要](../extensibility/internals/automation-model-overview.md) 」および「 [Visual Studio SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)」を参照してください。

### <a name="sharepoint-object-models"></a>SharePoint オブジェクトモデル
 SharePoint ツールの拡張機能から SharePoint の API を使用して、SharePoint サイトに変更を加えたり、SharePoint サイトからデータを取得したりできます。 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] および [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] には、オブジェクト モデルが 2 種類あります。サーバー オブジェクト モデルとクライアント オブジェクト モデルです。

 どちらのオブジェクト モデルの API も SharePoint ツールの拡張機能から使用できます。ただし、SharePoint ツールの拡張機能からこれらのオブジェクト モデルを使用する場合、それぞれ長所と短所があります。 詳細については、「 [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

|オブジェクト モデル|説明|
|------------------|-----------------|
|サーバー オブジェクト モデル|サーバー オブジェクト モデルを使用すると、[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] および [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] が公開しているすべての機能をプログラムから使用することができます。 このオブジェクト モデルは、SharePoint サーバー上で動作する SharePoint ソリューションから使用することを前提に設計されています。 このオブジェクトモデルの大部分は *Microsoft.SharePoint.dll* アセンブリで定義されています。 サーバーオブジェクトモデルの詳細については、「 [SharePoint Foundation Server 側のオブジェクトモデルの使用](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))」を参照してください。|
|クライアント オブジェクト モデル|クライアント オブジェクト モデルは、リモート クライアントまたはリモート サーバーの SharePoint データとの相互運用に使用できるサーバー オブジェクト モデルのサブセットです。 一般的なタスクに必要なラウンド トリップの回数を最小限に抑えるようにデザインされています。 クライアントオブジェクトモデルの大部分は、 *Microsoft.SharePoint.Client.dll* アセンブリおよび *Microsoft.SharePoint.Client.Runtime.dll* アセンブリで定義されています。 クライアントオブジェクトモデルの詳細については、「管理された [クライアントオブジェクトモデル](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14))」を参照してください。|

## <a name="see-also"></a>関連項目
- [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
