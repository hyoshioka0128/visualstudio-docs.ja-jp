---
title: '方法: SharePoint の配置コマンドを設定するMicrosoft Docs'
description: SharePoint の配置前コマンドと配置後コマンドを設定して、デプロイプロセスをカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fc1da67206e5e5c9fde1b5c595424239d1685ac7
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304379"
---
# <a name="how-to-set-sharepoint-deployment-commands"></a>方法: SharePoint の配置コマンドを設定する
  配置前コマンドと配置後コマンドを設定することによって、デプロイプロセスをカスタマイズできます。 これらのコマンドは、Visual Studio から SharePoint ソリューションをデバッグするときに、他の配置操作の前後に実行されます。

### <a name="to-add-a-pre-deployment-command"></a>配置前コマンドを追加するには

1. メニューバーで、[**プロジェクト** の  >  **\<*ProjectName*> プロパティ**] を選択します。

2. [ **SharePoint** ] タブを選択します。

3. [ **展開前のコマンドライン** ] テキストボックスに、このステップをカスタマイズするための MS-DOS または MSBuild コマンドを入力します。

     たとえば、配置が完了する前にディレクトリの内容を一覧表示するには、「 **dir**」と入力します。

### <a name="to-add-a-post-deployment-command"></a>配置後コマンドを追加するには

1. メニューバーで、[**プロジェクト** の  >  **\<*ProjectName*> プロパティ**] を選択します。

2. [ **SharePoint** ] タブを選択します。

3. [ **展開後のコマンドライン** ] テキストボックスに、このステップをカスタマイズするための MS-DOS または MSBuild コマンドを入力します。

     たとえば、配置の完了後にディレクトリの内容を一覧表示するには、「 **dir**」と入力します。 MSBuild 変数を使用してビルドディレクトリからアセンブリをコピーするには、「 **copy $ (TargetPath) C:\ deploymentdirectory**」と入力します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
