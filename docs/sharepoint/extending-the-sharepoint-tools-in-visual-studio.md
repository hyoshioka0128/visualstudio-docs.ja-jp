---
title: Visual Studio での SharePoint ツールの拡張 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio, extending tools
- extensibility [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extending tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7dc0cc0d0af73d032d870629877b62c94e6b347b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016037"
---
# <a name="extend-the-sharepoint-tools-in-visual-studio"></a>Visual Studio での SharePoint ツールの拡張
  Visual Studio の SharePoint ツールは、多くのアプリケーション開発シナリオの要件を満たしています。 ただし、自分や他の開発者が必要とする機能が提供されていない場合もあります。 このような場合は、SharePoint ツールを拡張して、必要な機能を作成できます。

## <a name="how-to-extend-the-sharepoint-tools"></a>SharePoint ツールを拡張する方法
 SharePoint プロジェクトシステムと [ **Sharepoint 接続**] ノードは、[**サーバーエクスプローラー** ] ウィンドウで拡張できます。

### <a name="extend-the-sharepoint-project-system"></a>SharePoint プロジェクトシステムの拡張
 Visual Studio には、SharePoint ソリューションの作成に使用できる一連のプロジェクトテンプレートと項目テンプレートが含まれています。 たとえば、イベントレシーバー、リスト定義、ワークフロー、および Web パーツのテンプレートがあります。 ただし、フィールドやカスタムアクションなどの SharePoint コンポーネントを作成するために、独自の種類の SharePoint プロジェクトアイテムを定義することもできます。 また、Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類の拡張機能を作成したり、SharePoint プロジェクトの拡張機能を作成したりすることもできます。

 詳細については、「 [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

### <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>サーバーエクスプローラーで SharePoint 接続ノードを拡張する
 Visual Studio では、[**サーバーエクスプローラー** ] ウィンドウの [ **SharePoint 接続**] ノードを使用して、1つまたは複数のローカル SharePoint サイトの多くのコンポーネントを階層ツリービューで表示できます。 **SharePoint Connections**ノードは、次の方法で拡張することもできます。

- 独自のノードを追加します。 これは、既定では表示されない SharePoint サイトのコンポーネントを表示する場合に便利です。

- 既存のノードを拡張する。 たとえば、既存のノードに新しい子ノードを追加したり、ショートカットメニュー項目をノードに追加して、開発者がメニュー項目をクリックしたときにタスクを実行したりすることができます。

  詳細については、[サーバーエクスプローラーの「SharePoint 接続ノードの拡張](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

## <a name="development-computer-requirements"></a>開発用コンピューターの要件
 SharePoint ツールの拡張機能を作成するには、開発用コンピューターが Visual Studio で SharePoint ソリューションを作成する場合と同じ要件を満たしている必要があります。

 また、をインストールすることもお勧めし [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] ます。 SDK には、Visual Studio を拡張するために使用できるプロジェクトテンプレートとツールが含まれています。 特に、SDK には、Visual Studio 拡張機能 (VSIX) パッケージを簡単に作成するために使用できるプロジェクトテンプレートが含まれています。 Visual studio 拡張機能を Visual Studio に配置するには、VSIX パッケージを使用することをお勧めします。 すべての SharePoint ツールの拡張機能は、VSIX パッケージを使用して配置する必要があります。 このドキュメントのすべてのチュートリアルでは、がインストールされていることを前提とし [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] ています。

 Visual Studio SDK をインストールするには、「 [Visual STUDIO sdk のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。 Visual Studio 拡張機能の詳細については、「 [Visual Studio 拡張機能の開発の開始](../extensibility/starting-to-develop-visual-studio-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [SharePoint ツール拡張機能のプログラミングモデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)
- [サーバーエクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint ツールの拡張機能のプログラミングの概念と機能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [SharePoint ツールの機能拡張&#41;のリファレンス &#40;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [Visual Studio の SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)