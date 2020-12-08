---
title: Office ソリューションの設計と作成
description: さまざまな種類の Office ソリューションを作成するために使用できるプロジェクトテンプレートを Visual Studio が提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], creating
- Office development in Visual Studio, creating solutions
- solutions [Office development in Visual Studio], creating
- Office project types in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 191de013c94bfede7d1ddac5f3dd0392143e08dc
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847534"
---
# <a name="design-and-create-office-solutions"></a>Office ソリューションの設計と作成

Visual Studio には、さまざまな種類の Office ソリューションの作成に使用できるプロジェクト テンプレートが用意されています。 ここでは、プロジェクト テンプレートについて説明し、Office プロジェクトを作成するためのガイダンスを示します。 プロジェクトの作成後にコードおよびユーザーインターフェイスのカスタマイズを実装する方法の詳細については、「 [Office ソリューションの開発](../vsto/developing-office-solutions.md)」を参照してください。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="create-office-projects"></a>Office プロジェクトを作成する
 開始する前に、要件を決定し、最適なソリューションの種類を探します。 たとえば、アプリケーションを使用するたびに作成した Office ソリューションを実行する必要がある場合は、VSTO アドインが最適です。 コードが 1 つのドキュメントと緊密に統合されている場合は、ドキュメント レベルのカスタマイズを作成します。 これらのプロジェクト タイプは、Visual Studio のプロジェクト テンプレートとして利用できます。 Visual Studio に含まれる Office プロジェクトテンプレートの詳細については、「 [office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。 Office プロジェクトを作成する方法の詳細については、「 [方法: Visual Studio で office プロジェクトを作成](../vsto/how-to-create-office-projects-in-visual-studio.md)する」を参照してください。

 Office プロジェクトには、Visual Studio の他の種類のプロジェクトとは異なる機能とプロジェクト項目があります。 たとえば、ドキュメント レベルのプロジェクトを作成した場合は、プロジェクト内の文書またはブックを Visual Studio 内部で開いて編集できます。 詳細については、「 [Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="choose-a-net-framework-version"></a>.NET Framework のバージョンを選択してください
 要件に最適なプロジェクトの種類を選択した後に、開発工程で使用する .NET Framework のバージョンを選択できます。 Office プロジェクトでは、次のバージョンの .NET Framework を対象にすることができます。

- [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]

- [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)]

- [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]

  ソリューションを実行するエンドユーザーのコンピューターでは、プロジェクト用に選択した .NET Framework バージョンが必要です。 たとえば、プロジェクトがを対象としている場合、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] エンドユーザーのコンピューターにはが必要です。 この例では、エンドユーザーのコンピューターに .NET Framework 3.5 のみがインストールされている場合、ソリューションは実行されません。

  .NET Framework 3.5 を対象とする VSTO アドイン プロジェクトを移行する場合、インストールした Office のバージョンに応じて、Visual Studio によってプロジェクトのターゲット フレームワークが [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更されます。

  ただし、プロジェクトで特定の機能を使用している場合は、Visual Studio によるターゲット フレームワークの変更後に、プロジェクトのコードの一部を変更することが必要になる場合があります。 ターゲットフレームワークを変更する方法の詳細については、「 [方法: .NET Framework のバージョンをターゲット](../ide/visual-studio-multi-targeting-overview.md)にする」を参照してください。 プロジェクトで行う必要がある変更の詳細については、「 [.NET Framework 4 以降への Office ソリューションの移行](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)」を参照してください。

  Visual Studio によってプロジェクトのターゲット .NET Framework が変更され、ClickOnce を使用してソリューションを配置している場合は、[ **必須コンポーネント** ] ダイアログボックスでも、対応するバージョンの .NET Framework を選択してください。 プロジェクトのターゲット フレームワークを変更しても、この選択内容は自動的には変わりません。 詳細については、「 [方法: Office ソリューションを実行するためにエンドユーザーのコンピューターに必須コンポーネントをインストールする](/previous-versions/bb608608(v=vs.110))」を参照してください。

> [!NOTE]
> .NET Framework 3.5 以前を [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] を使用して作成した Office プロジェクトの対象にすることはできません。 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] を使用して作成した Office プロジェクトには、[!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] で導入された機能が必要です。

### <a name="understand-when-the-office-pias-are-required-on-end-user-computers"></a>エンドユーザーのコンピューターで Office Pia が必要になるタイミングを理解する
 既定では、プロジェクト内の各 Office PIA 参照の [ **相互運用機能型の埋め込み** ] プロパティが既定値である [ **True**] に設定されている場合、エンドユーザーのコンピューターに office プライマリ相互運用機能アセンブリ (pia) をインストールする必要はありません。 この場合、プロジェクトをビルドすると、ソリューションが使用する PIA 型の型情報がソリューション アセンブリに埋め込まれます。 実行時に、埋め込まれた型情報が PIA の代わりに使用され、Office アプリケーションの COM ベースのオブジェクト モデルが呼び出されます。 Pia の型をソリューションに埋め込む方法の詳細については、「 [型の等価性と埋め込み相互運用機能型](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types)」を参照してください。

 プロジェクト内の各 Office PIA 参照の [ **相互運用型の埋め込み** ] プロパティが [ **False**] に設定されている場合は、ソリューションを実行する各エンドユーザーコンピューターのグローバルアセンブリキャッシュに office pia をインストールし、登録する必要があります。 ほとんどの場合、PIA は既定で Office と共にインストールされますが、ソリューションの必須コンポーネントとして再頒布可能な PIA を含めることもできます。 詳細については、「 [Office ソリューションの配置の前提条件](/previous-versions/bb608617(v=vs.110))」を参照してください。

### <a name="understand-the-client-profile"></a>クライアントプロファイルについて
 .NET Framework Client Profile は、完全な .NET Framework のサブセットです。 .NET Framework のクライアント機能のみを使用し、Office ソリューションをできる限り迅速に配置する必要がある場合は、.NET Framework Client Profile を対象にすることができます。 詳細については、「 [.NET Framework client profile](/dotnet/framework/deployment/client-profile)」を参照してください。

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] を対象とする Office プロジェクトを作成するときに、既定で [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] が対象となります。 完全な [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 用に開発する場合は、プロジェクトを作成した後でこのオプションを設定する必要があります。 詳細については、[.NET Framework のターゲット バージョンを指定する](../ide/visual-studio-multi-targeting-overview.md)」を参照してください。

## <a name="create-solutions-for-the-64-bit-edition-of-microsoft-office"></a>Microsoft Office の64ビット版のソリューションを作成する
 Microsoft Office には、64 ビットと 32 ビットのエディションがあります。 いずれかのエディションで実行できる Office ソリューションを作成するには、プロジェクトのプラットフォームターゲット設定を [ **ANY CPU**] に設定する必要があります。 これは、Office プロジェクトの既定値です。 詳細については、「 [Office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] には、64 ビットと 32 ビットの別個のバージョンがあり、それぞれ Microsoft Office の 64 ビットおよび 32 ビットのエディションによって使用されます。 詳細については、「 [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

## <a name="assemblies-in-office-solutions"></a>Office ソリューションのアセンブリ
 Visual Studio の Office 開発ツールを使用して Office プロジェクトを作成した場合、記述したコードは最終的にアセンブリにコンパイルされます。 アセンブリは、共有サーバーまたはクライアントコンピューター上のディレクトリに配置されます。

 Office ソリューションのアセンブリは Office アプリケーションによって読み込まれます。 アセンブリが読み込まれると、アセンブリ内のコードがアプリケーションで発生するイベント (ユーザーがメニュー項目をクリックした場合など) に応答できます。 アセンブリ内のコードでは、オブジェクト モデルを呼び出してアプリケーションの自動化や拡張を行うこともでき、さらに [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] のクラスも使用できます。 詳細については、「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md) 」および「 [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

 Office ソリューションでは、配置マニフェストとアプリケーション マニフェストを使用してアセンブリを特定します。 これらのマニフェストには、アセンブリの名前、バージョン、および場所に関する情報が含まれているので、アプリケーションでは正しいアセンブリの検索、リンク、および実行ができます。 詳細については、「 [Office ソリューションのアプリケーションマニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)」を参照してください。

 ドキュメント レベルのプロジェクトには、アセンブリに加え、ドキュメントも含まれています。 ドキュメントは、アプリケーションのフロント エンドとして機能し、ユーザーはすべての操作をドキュメント上で行います。 各ドキュメントは、メイン プロジェクト アセンブリを 1 つしか関連付けることができませんが、複数のドキュメントが同じアセンブリをポイントすることは可能です。

 ドキュメント レベルのプロジェクトのアセンブリは、ドキュメントに埋め込まれるわけではなく、別の場所に格納されていて、ドキュメントのアプリケーション マニフェストによって識別されます。

## <a name="security-considerations-for-assemblies"></a>アセンブリのセキュリティに関する考慮事項
 Office ソリューションをコンピューターで実行する場合、ソリューションに使用されるアセンブリは信頼して実行できる必要があります。 セキュリティの詳細については、「 [Office ソリューション](../vsto/securing-office-solutions.md)のセキュリティ保護」を参照してください。

 既定では、プロジェクトの出力フォルダーにあるソリューション アセンブリおよび参照アセンブリは、プロジェクトをビルドするときに開発用コンピューターで信頼して実行できます。 詳細については、「 [Office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

 セキュリティ上の理由により、プロジェクトは、共有の場所に配置するのではなく、ローカル コンピューター上に作成することをお勧めします。 詳細については、「 [Office ソリューションの共同開発](../vsto/collaborative-development-of-office-solutions.md)」を参照してください。

## <a name="referenced-assemblies"></a>参照アセンブリ
 アセンブリは、プロジェクトの参照にリストされている他のアセンブリを参照できます。 ただし、ドキュメント レベルのプロジェクト アセンブリが別のドキュメント レベルのプロジェクト アセンブリを参照することはできません。

## <a name="see-also"></a>関連項目
- [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)
- [Office プロジェクトのプロパティ](../vsto/properties-in-office-projects.md)
- [さまざまなバージョンの Microsoft Office でソリューションを実行する](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)
- [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Office ソリューションのアプリケーションマニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [方法: Office ソリューションの構成情報を設定する](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)
- [Visual Studio 内での Office 機能の使用](../vsto/using-office-functionality-inside-of-visual-studio.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
- [Office プログラミングにおける一般的なタスク](../vsto/common-tasks-in-office-programming.md)
- [Office ソリューションの開発](../vsto/developing-office-solutions.md)
- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)