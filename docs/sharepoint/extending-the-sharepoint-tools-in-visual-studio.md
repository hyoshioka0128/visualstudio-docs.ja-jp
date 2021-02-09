---
title: Visual Studio での SharePoint ツールの拡張 | Microsoft Docs
description: Visual Studio の SharePoint ツールを拡張します。 SharePoint プロジェクト システムを拡張します。 サーバー エクスプローラーで [SharePoint 接続] ノードを拡張します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c074e62b47b926351948e94d78621a8a41c9c3e5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876850"
---
# <a name="extend-the-sharepoint-tools-in-visual-studio"></a>Visual Studio での SharePoint ツールの拡張
  Visual Studio の SharePoint ツールは、多くのアプリケーション開発シナリオの要件を満たしています。 しかし、自分や他の開発者が必要とする機能が提供されていない場合もあります。 このような場合は、SharePoint ツールを拡張して、必要な機能を作成できます。

## <a name="how-to-extend-the-sharepoint-tools"></a>SharePoint ツールを拡張する方法
 SharePoint プロジェクト システムと **[SharePoint 接続]** ノードは、 **[サーバー エクスプローラー]** ウィンドウで拡張できます。

### <a name="extend-the-sharepoint-project-system"></a>SharePoint プロジェクト システムを拡張する
 Visual Studio には、SharePoint ソリューションの作成に使用できる一連のプロジェクト テンプレートと項目テンプレートが含まれています。 たとえば、イベント レシーバー、リスト定義、ワークフロー、Web パーツのテンプレートがあります。 ただし、フィールドやカスタム アクションなどの SharePoint コンポーネントを作成する場合は、独自の種類の SharePoint プロジェクト項目を定義することもできます。 また、Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類の拡張機能を作成したり、SharePoint プロジェクトの拡張機能を作成したりできます。

 詳細については、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

### <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する
 Visual Studio では、 **[サーバー エクスプローラー]** ウィンドウの **[SharePoint 接続]** ノードを使用して、1 つまたは複数のローカル SharePoint サイトのコンポーネントの多くを階層ツリー ビューで表示できます。 また、次の方法で **[SharePoint 接続]** ノードを拡張することもできます。

- 独自のノードを追加する。 これは、既定では表示されない SharePoint サイトのコンポーネントを表示する場合に便利です。

- 既存のノードを拡張する。 たとえば、既存のノードに新しい子ノードを追加したり、ショートカット メニュー項目をノードに追加して、開発者がメニュー項目をクリックしたときにタスクを実行したりできます。

  詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

## <a name="development-computer-requirements"></a>開発コンピューターの要件
 SharePoint ツールの拡張機能を作成するには、開発用コンピューターが Visual Studio で SharePoint ソリューションを作成する場合と同じ要件を満たしている必要があります。

 [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] もインストールすることをお勧めします。 SDK には、Visual Studio を拡張するために使用できるプロジェクト テンプレートとツールが含まれています。 特に、SDK には、Visual Studio 拡張機能 (VSIX) パッケージを簡単に作成するために使用できるプロジェクト テンプレートが含まれています。 Visual Studio で Visual Studio 拡張機能を配置するには、VSIX パッケージを使用することをお勧めします。 すべての SharePoint ツールの拡張機能は、VSIX パッケージを使用して配置する必要があります。 このドキュメントのすべてのチュートリアルで、[!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] がインストールされていることを前提としています。

 Visual Studio SDK をインストールするには、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。 Visual Studio 拡張機能の詳細については、「[Visual Studio 拡張機能の開発を始める](../extensibility/starting-to-develop-visual-studio-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint ツール拡張機能におけるプログラミングに関する概念および特徴](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [リファレンス (SharePoint ツールの拡張性)](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [Visual Studio での SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)