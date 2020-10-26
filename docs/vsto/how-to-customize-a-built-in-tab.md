---
title: '方法: 組み込みタブをカスタマイズする'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- built-in tabs [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5f73ec7a8555a5e5d569d4316ca619747550bf11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547187"
---
# <a name="how-to-customize-a-built-in-tab"></a>方法: 組み込みタブをカスタマイズする
  組み込みタブにグループとコントロールを追加できます。組み込みタブは、既に Microsoft Office アプリケーションのリボンにあるタブです。 たとえば、[ **データ** ] タブは Excel の組み込みタブです。 カスタム グループを作成すると、そのグループはタブの最後に表示されますが、タブ上のどこにでも移動できます。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

> [!NOTE]
> 組み込みタブにグループを追加することはできますが、組み込みタブから組み込みグループを削除することはできません。

### <a name="to-add-groups-to-a-built-in-tab"></a>組み込みタブにグループを追加するには

1. **ソリューションエクスプローラー**でリボンコードファイルを右クリックし、[デザイナーの**表示**] をクリックします。

    > [!NOTE]
    > リボンコードファイルが **ソリューションエクスプローラー**に表示されない場合は、プロジェクトに **リボン項目** を追加する必要があります。 「 [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)」を参照してください。

2. リボンデザイナーの任意のタブを右クリックし、[ **プロパティ**] をクリックします。

3. [ **プロパティ** ] ウィンドウで、[ **ControlId** ] プロパティを展開し、[制御 **Lidtype** ] プロパティを「 **Office**」に設定します。

4. **Officeid**プロパティを、カスタマイズする組み込みタブの*コントロール ID*に設定します。

     コントロール ID は、Microsoft Office アプリケーションに組み込まれているタブ、グループ、コントロールを一意に識別する名前です。

     コントロール Id の一覧については、「 [office 2010 のヘルプファイル: office fluent ユーザーインターフェイスコントロールの識別子](https://www.microsoft.com/download/details.aspx?id=6627)」を参照してください。

5. [**ツールボックス**] の [ **Office リボンコントロール**] タブから、グループをタブにドラッグします。

    > [!NOTE]
    > 組み込みグループは、デザイナーには表示されません。 したがって、組み込みタブを使用して作業しているかどうかを判断する唯一の方法は、タブの **ControlId** プロパティを調べることです。

### <a name="to-position-groups-on-a-built-in-tab"></a>組み込みタブ上でグループを配置するには

1. リボン デザイナーで、カスタム グループを選択します。

2. [ **プロパティ** ] ウィンドウで、[ **位置** ] プロパティを展開します。

3. **Positiontype**プロパティを適切な値に設定します。

    - **Beforeofficeid** は、指定された組み込みグループの前にグループを配置します。

    - **Afterofficeid** は、指定された組み込みグループの後にグループを配置します。

4. **Officeid**プロパティを組み込みグループのコントロール ID に設定します。

     コントロール Id の一覧については、「 [office 2010 のヘルプファイル: office fluent ユーザーインターフェイスコントロールの識別子](https://www.microsoft.com/download/details.aspx?id=6627)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボンデザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: リボン XML を使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [方法: アドインのユーザーインターフェイスエラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)
