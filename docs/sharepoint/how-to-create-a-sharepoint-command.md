---
title: '方法: SharePoint コマンドを作成する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 15ea7ff86e90bf7a474f9d64c30a9803e3e20bf5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016224"
---
# <a name="how-to-create-a-sharepoint-command"></a>方法: SharePoint コマンドを作成する
  SharePoint ツールの拡張機能でサーバーオブジェクトモデルを使用する場合は、API を呼び出すカスタム *SharePoint コマンド* を作成する必要があります。 サーバーオブジェクトモデルを直接呼び出すことができるアセンブリで、SharePoint コマンドを定義します。

 SharePoint コマンドの目的の詳細については、「 [sharepoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

### <a name="to-create-a-sharepoint-command"></a>SharePoint コマンドを作成するには

1. 次のように構成されたクラスライブラリプロジェクトを作成します。

    - .NET Framework 3.5 を対象とします。 ターゲットフレームワークの選択の詳細については、「 [方法: .NET Framework のバージョンをターゲット](../ide/visual-studio-multi-targeting-overview.md)にする」を参照してください。

    - は、AnyCPU または x64 プラットフォームを対象としています。 既定では、クラスライブラリプロジェクトのターゲットプラットフォームは AnyCPU です。 ターゲットプラットフォームの選択の詳細については、「 [方法: プロジェクトを構成してターゲットプラットフォームを設定](../ide/how-to-configure-projects-to-target-platforms.md)する」を参照してください。

    > [!NOTE]
    > Sharepoint コマンドは、sharepoint ツールの拡張機能を定義するのと同じプロジェクトに実装することはできません。これは、sharepoint コマンドが .NET Framework 3.5 と SharePoint ツールの拡張機能を対象としているため [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] です。 拡張機能によって使用される SharePoint コマンドは、別のプロジェクトで定義する必要があります。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint.Commands

    - Microsoft.SharePoint

3. プロジェクトのクラスで、SharePoint コマンドを定義するメソッドを作成します。 メソッドは、次のガイドラインに従う必要があります。

    - 1つまたは2つのパラメーターを持つことができます。

         最初のパラメーターはオブジェクトである必要があり <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> ます。 このオブジェクトは、コマンドが実行される、Microsoft SharePoint の SPSite または Microsoft. SharePoint. を提供します。 また、 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger> Visual Studio の [ **出力** ] ウィンドウまたは [ **エラー一覧** ] ウィンドウにメッセージを書き込むために使用できるオブジェクトも用意されています。

         2番目のパラメーターは任意の型にすることができますが、このパラメーターは省略可能です。 SharePoint ツールの拡張機能からのデータをコマンドに渡す必要がある場合は、このパラメーターを SharePoint コマンドに追加できます。

    - 戻り値を持つことはできますが、これは省略可能です。

    - 2番目のパラメーターと戻り値は、Windows Communication Foundation (WCF) によってシリアル化できる型である必要があります。 詳細については、「 [データコントラクトシリアライザーでサポートされる型](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer) 」と「 [XmlSerializer クラスの使用](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class)」を参照してください。

    - メソッドは、任意の可視性 (**パブリック**、 **内部**、または **プライベート**) を持つことができ、静的または非静的にすることができます。

4. <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute>をメソッドに適用します。 この属性は、コマンドの一意の識別子を指定します。この識別子は、メソッド名と一致する必要はありません。

     SharePoint ツールの拡張機能からコマンドを呼び出すときは、同じ一意の識別子を指定する必要があります。 詳細については、「 [方法: SharePoint コマンドを実行](../sharepoint/how-to-execute-a-sharepoint-command.md)する」を参照してください。

## <a name="example"></a>例
 次のコード例は、識別子を持つ SharePoint コマンドを示して `Contoso.Commands.UpgradeSolution` います。 このコマンドは、サーバーオブジェクトモデルの Api を使用して、配置されたソリューションにアップグレードします。

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#5)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#5)]

 暗黙的な最初のパラメーターに加えて <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 、このコマンドには、SharePoint サイトにアップグレードする .wsp ファイルの完全なパスを含むカスタム文字列パラメーターもあります。 このコードをより大きな例のコンテキストで表示するには、「 [チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)する」を参照してください。

## <a name="compiling-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint.Commands

- Microsoft.SharePoint

## <a name="deploying-the-command"></a>コマンドの展開
 コマンドを配置するには、コマンドを [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用する拡張機能アセンブリと同じ拡張機能 (*vsix*) パッケージにコマンドアセンブリを含めます。 また、source.extension.vsixmanifest ファイルにコマンドアセンブリのエントリを追加する必要があります。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [方法: SharePoint コマンドを実行する](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
