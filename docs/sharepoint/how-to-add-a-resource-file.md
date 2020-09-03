---
title: '方法: リソースファイルを追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- resource files [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, resource files
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 657eb473adcff40a62d2fc9b09518ebe8135eeb4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015180"
---
# <a name="how-to-add-a-resource-file"></a>方法: リソースファイルを追加する
  リソースファイルを追加するためのコマンドは、[ソリューション] ノードのショートカットメニューとソリューションエクスプローラーの機能ノードにあります。 詳細については、「 [SharePoint ソリューションのローカライズ](../sharepoint/localizing-sharepoint-solutions.md)」を参照してください。

### <a name="to-add-a-global-resource-file-to-a-sharepoint-solution"></a>SharePoint ソリューションにグローバルリソースファイルを追加するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、SharePoint ソリューションを開きます。

2. **ソリューションエクスプローラー**で、SharePoint プロジェクトノードを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

3. [ **新しい項目の追加** ] ダイアログボックスで、[ **グローバルリソースファイル** ] テンプレートを選択し、[ **追加** ] をクリックします。

   > [!NOTE]
   > [グローバルリソースファイル] プロジェクト項目テンプレートは、SharePoint プロジェクト項目が選択されている場合にのみ表示されます。

4. [ **リソースの追加** ] ダイアログボックスで、リソースファイルのカルチャ (英語 (米国) など) を選択します。

    この手順では、Resource_x_ の形式でソリューションにグローバルリソースファイルを追加し**ます。**<em>カルチャ</em><strong>。</strong>.resx (など)、 *resource1.resx*です。

5. で **リソースエディター** が開いたら [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、リソースファイルにリソースを追加します。

### <a name="to-add-a-feature-resource-file-to-a-sharepoint-feature"></a>フィーチャーリソースファイルを SharePoint 機能に追加するには

1. SharePoint ソリューションがでまだ開いていない場合は [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、ソリューションを開きます。

2. **ソリューションエクスプローラー**で、[**機能**] ノードの下にある機能の名前のショートカットメニューを開き、[**機能リソースの追加**] を選択します。

     この手順では、リソースファイルを_Resourcefilename_形式で機能に追加し**ます。***feature1.feature*のような、.resx などの **.resx**_です。_

3. で **リソースエディター** が開いたら [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、リソースファイルにリソースを追加します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
