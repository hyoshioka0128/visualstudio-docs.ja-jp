---
title: '方法: SharePoint の配置構成を編集する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.DeploymentConfig
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
ms.openlocfilehash: 74f6377bad0f62aa2c470e72afe64b85b3017ee6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016778"
---
# <a name="how-to-edit-a-sharepoint-deployment-configuration"></a>方法: SharePoint の配置構成を編集する
  展開構成を作成するか、既存の展開構成を変更することができます。 たとえば、1つの手順を実行したり、配置プロセスのステップの順序を変更したりできます。 組み込みの構成およびプログラムによって追加された構成は変更できないため、配置構成を作成または変更することができます。

## <a name="create-a-sharepoint-deployment-configuration"></a>SharePoint 配置構成を作成する

#### <a name="to-create-a-sharepoint-deployment-configuration"></a>SharePoint の配置構成を作成するには

1. **ソリューションエクスプローラー**で、SharePoint プロジェクトを選択し、メニューバーで [**プロジェクト**]、[ProjectName の_ProjectName_**プロパティ**] の順に選択します。

2. [ **SharePoint** ] タブで、[ **新規作成** ] をクリックします。

     [ **新しい展開構成の追加** ] ダイアログボックスが表示されます。

3. [ **名前** ] テキストボックスに、展開構成の名前を入力します。

4. [ **利用可能な展開手順** ] ウィンドウで、展開構成に追加する手順を選択し、() ボタンを選択して、[ **>** **OK** ] をクリックします。

    > [!NOTE]
    > 配置前コマンドまたは配置後コマンドを構成した場合、これらの手順は、カスタマイズされた展開構成に追加した場合にのみ実行されます。

## <a name="change-the-active-deployment-configuration"></a>アクティブな配置構成の変更

#### <a name="to-change-the-active-deployment-configuration"></a>アクティブな配置構成を変更するには

1. **ソリューションエクスプローラー**で、SharePoint プロジェクトを選択し、メニューバーで [**プロジェクト**の  >  ** \<*ProjectName*> プロパティ**] を選択します。

2. [ **SharePoint** ] タブを選択します。

3. [ **アクティブな展開構成** ] ボックスの一覧で、使用する展開構成の名前を選択します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
