---
title: '方法: Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする'
titleSuffix: ''
ms.custom: seodec18
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio]
- installing Office development tools in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ef71de75be5977ab80cbdd85448daa5de381c077
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547226"
---
# <a name="how-to-install-the-visual-studio-tools-for-office-runtime-redistributable"></a>方法: Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする
  Visual Studio 2010 Tools for Office runtime は、の Microsoft Office 開発者ツールを使用して作成されたソリューションを実行する各コンピューターにインストールする必要があり [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 ランタイムは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]、および Microsoft Office をインストールすると自動的にインストールされます。 詳細については、「 [Visual Studio Tools for Office ランタイムのインストールシナリオ](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)」を参照してください。

[!include[Add-ins note](includes/addinsnote.md)]

 次の場合は、手動による以下のインストール手順を実行する必要があります。

- [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] をサーバーにインストールする必要がある場合。 たとえば、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用してサーバー上のドキュメント レベルのソリューションを管理する場合があります。

- Office ソリューションのその他の必須コンポーネントが既にインストールされているコンピューターにランタイムをインストールする必要がある場合。

    > [!NOTE]
    > .NET Framework および [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] をインストールするには、開発コンピューターの管理者である必要があります。

## <a name="to-install-the-visual-studio-tools-for-office-runtime"></a>Visual Studio Tools for Office ランタイムをインストールするには

1. [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降をインストールします。

    - をダウンロードするには [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 、「 [Microsoft .NET Framework 4 (Web インストーラー)](https://www.microsoft.com/download/details.aspx?id=17851)」を参照してください。

    - をダウンロードするには [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] 、「 [Microsoft .NET Framework 4 Client Profile (Web インストーラー)](https://www.microsoft.com/download/details.aspx?id=17113)」を参照してください。

    - をダウンロードするには [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 、「 [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)」を参照してください。

2. *vstor_redist.exe*を実行して、をインストールし [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。

     これらのセットアップファイルは、 [Visual Studio 2010 Tools For Office runtime](https://www.microsoft.com/download/details.aspx?id=56961)からダウンロードできます。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] の必須コンポーネントは .NET Framework の場合と同じです。

     [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] には、言語パックが用意されています。 Windows のインストールが英語以外の言語に設定されている場合、Windows と同じ言語でランタイム メッセージを表示できます。 同様に、エンド ユーザーが [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] をインストールし、英語以外の言語に設定されている Windows のインストールでソリューションを実行すると、Windows と同じ言語でランタイム メッセージが表示されます。 場合によっては、追加の言語パックが必要になる場合があります。 たとえば、Windows のコピーで複数の言語設定が使用されている場合、またはを既にインストールした後に別の言語に切り替える場合は、追加の言語パックが必要になることがあり [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 言語パックは[、Microsoft Visual Studio 2010 Tools for the Microsoft Office system (version 4.0 runtime) language pack](https://www.microsoft.com/download/details.aspx?id=54246)で見つけることができます。

## <a name="see-also"></a>関連項目
- [Visual Studio で &#40;Office 開発を開始する&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office ソリューションを開発するようにコンピューターを構成する](../vsto/configuring-a-computer-to-develop-office-solutions.md)
- [方法: Office ソリューションを開発するようにコンピューターを構成する](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [方法: Office プライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
