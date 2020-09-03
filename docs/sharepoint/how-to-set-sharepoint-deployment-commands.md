---
title: '方法: SharePoint の配置コマンドを設定するMicrosoft Docs'
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
ms.openlocfilehash: c2329efef64e7d8605f8483ff7dce3107cd702fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015504"
---
# <a name="how-to-set-sharepoint-deployment-commands"></a>方法: SharePoint の配置コマンドを設定する
  配置前コマンドと配置後コマンドを設定することによって、デプロイプロセスをカスタマイズできます。 これらのコマンドは、Visual Studio から SharePoint ソリューションをデバッグするときに、他の配置操作の前後に実行されます。

### <a name="to-add-a-pre-deployment-command"></a>配置前コマンドを追加するには

1. メニューバーで、[**プロジェクト**の  >  ** \<*ProjectName*> プロパティ**] を選択します。

2. [ **SharePoint** ] タブを選択します。

3. [ **展開前のコマンドライン** ] テキストボックスに、このステップをカスタマイズするための MS-DOS または MSBuild コマンドを入力します。

     たとえば、配置が完了する前にディレクトリの内容を一覧表示するには、「 **dir**」と入力します。

### <a name="to-add-a-post-deployment-command"></a>配置後コマンドを追加するには

1. メニューバーで、[**プロジェクト**の  >  ** \<*ProjectName*> プロパティ**] を選択します。

2. [ **SharePoint** ] タブを選択します。

3. [ **展開後のコマンドライン** ] テキストボックスに、このステップをカスタマイズするための MS-DOS または MSBuild コマンドを入力します。

     たとえば、配置の完了後にディレクトリの内容を一覧表示するには、「 **dir**」と入力します。 MSBuild 変数を使用してビルドディレクトリからアセンブリをコピーするには、「 **copy $ (TargetPath) C:\ deploymentdirectory**」と入力します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
