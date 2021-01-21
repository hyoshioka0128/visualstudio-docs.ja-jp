---
title: SharePoint オブジェクトモデルの呼び出し |Microsoft Docs
description: SharePoint ツールの拡張機能で使用できる2つの異なるオブジェクトモデルを呼び出す方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint development in Visual Studio, server object model
- SharePoint commands [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 40cd7132888d8b19d8e2a2818ec9a299b465e786
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850053"
---
# <a name="call-into-the-sharepoint-object-models"></a>SharePoint オブジェクトモデルの呼び出し
  Visual Studio で SharePoint ツールの拡張機能を作成するときに、特定のタスクを実行するために SharePoint Api を呼び出すことが必要になる場合があります。 たとえば、SharePoint プロジェクトのカスタム配置手順を作成する場合、ソリューションを配置するためのタスクの一部を実行するために、SharePoint Api を呼び出す必要がある場合があります。

 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] と [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] には、SharePoint ツールの拡張機能で使用できる2つの異なるオブジェクトモデル (サーバーオブジェクトモデルとクライアントオブジェクトモデル) が用意されています。 各オブジェクトモデルには、SharePoint ツールの拡張機能のコンテキストでの利点と欠点があります。

 SharePoint オブジェクトモデルの概要については、「 [sharepoint ツールの拡張機能のプログラミングモデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)」を参照してください。

## <a name="use-the-client-object-model-in-extension-projects"></a>拡張機能プロジェクトでクライアントオブジェクトモデルを使用する
 SharePoint ツールの拡張機能を開発する場合は、他のマネージ Api のセットと同様に、プロジェクトでクライアントオブジェクトモデルを使用できます。 クライアントオブジェクトモデルのアセンブリへの参照をプロジェクトに追加できます。また、コードから直接、クライアントオブジェクトモデルの Api を呼び出すことができます。

 ただし、クライアントオブジェクトモデルには、SharePoint ツールの拡張機能のコンテキストで2つの欠点があります。

- クライアントオブジェクトモデルは、サーバーオブジェクトモデルのサブセットのみを提供します。 クライアントオブジェクトモデルで公開されていない SharePoint 機能を使用する必要がある場合は、サーバーオブジェクトモデルを使用する必要があります。

- SharePoint ツールの拡張機能でクライアントオブジェクトモデルを使用することはほとんどの場合に機能しますが、クライアントオブジェクトモデルの呼び出しが想定どおりに動作しない場合があります。 クライアントオブジェクトモデルは、リモートサーバーまたはファーム上の SharePoint サイトを呼び出すためにクライアントアプリケーションで使用されるように設計されています。 Visual Studio の SharePoint ツールは、開発用コンピューター上の SharePoint のローカルインストールでのみ動作します。 そのため、SharePoint ツールの拡張機能でクライアントオブジェクトモデルを使用する場合は、ローカルコンピューター上の SharePoint サイトを呼び出すことになります。これは、クライアントオブジェクトモデルを使用するように設計されたものではありません。

  Visual Studio の SharePoint ツールの拡張機能でクライアントオブジェクトモデルを使用する方法を示すチュートリアルについては、「 [チュートリアル: サーバーエクスプローラー拡張機能での sharepoint クライアントオブジェクトモデルの呼び出し](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)」を参照してください。

## <a name="use-the-server-object-model-in-extension-projects"></a>拡張機能プロジェクトでのサーバーオブジェクトモデルの使用
 サーバーオブジェクトモデルは、クライアントオブジェクトモデルのスーパーセットです。 サーバーオブジェクトモデルを使用すると、およびによって公開されるすべての機能をプログラムによって使用でき [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] ます。

 SharePoint ツールの拡張機能では、サーバーオブジェクトモデルの Api を使用できますが、Api を直接呼び出すことはできません。 サーバーオブジェクトモデルは、.NET Framework 3.5 を対象とする64ビットプロセスからのみ呼び出すことができます。 ただし、SharePoint ツールの拡張機能では、が必要 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] です。これらは、32ビットの Visual Studio プロセスで実行されます。 これにより、SharePoint ツールの拡張機能は、SharePoint サーバーオブジェクトモデル内のアセンブリを直接参照できなくなります。

 SharePoint ツールの拡張機能でサーバーオブジェクトモデルを使用する場合は、API を呼び出すカスタム *SharePoint コマンド* を作成する必要があります。 サーバーオブジェクトモデルを直接呼び出すことができるセカンダリアセンブリで、SharePoint コマンドを定義します。 拡張プロジェクトでは、オブジェクトの ExecuteCommand メソッドを使用して、SharePoint コマンドを間接的に呼び出し <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> ます。

 SharePoint コマンドの作成と使用の詳細については、「 [方法:](../sharepoint/how-to-create-a-sharepoint-command.md) sharepoint コマンドを作成する」および「 [方法: Sharepoint コマンドを実行](../sharepoint/how-to-execute-a-sharepoint-command.md)する」を参照してください。 SharePoint コマンドを配置する方法の詳細については、「 [Visual Studio での sharepoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

 SharePoint コマンドを作成して使用する方法を示すチュートリアルについては、「 [チュートリアル: sharepoint プロジェクトのカスタム配置手順を作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md) する」および「 [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

### <a name="understand-how-sharepoint-commands-are-executed"></a>SharePoint コマンドの実行方法について
 SharePoint コマンドを定義するアセンブリは、 *vssphost4.exe* という名前の64ビットホストプロセスに読み込まれます。 Sharepoint ツールの拡張機能で SharePoint コマンドを呼び出すと、32ビットの Visual Studio プロセス (*devenv.exe*) ではなく、 *vssphost4.exe* によってコマンドが実行されます。 レジストリで値を設定することにより、SharePoint コマンドの実行方法のいくつかの側面を制御できます。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)
- [方法: SharePoint コマンドを実行する](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
