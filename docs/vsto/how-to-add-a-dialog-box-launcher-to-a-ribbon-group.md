---
title: '方法: リボングループにダイアログボックスランチャーを追加する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- dialog box launcher [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], dialog box launcher
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 29b260929d0478749296496db5b454326497d3ad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85541621"
---
# <a name="how-to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>方法: リボングループにダイアログボックスランチャーを追加する
  ダイアログボックスランチャーは、リボン上の任意のグループに追加できます。 ダイアログボックスランチャーは、グループに表示される小さいアイコンです。 ユーザーはこのアイコンをクリックして、関連するダイアログボックスや、グループに関連するその他のオプションを提供する作業ウィンドウを開くことができます。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-dialog-box-launcher-to-a-ribbon-group"></a>リボングループにダイアログボックスランチャーを追加するには

1. **ソリューションエクスプローラー**でリボンコードファイル (*.vb*または *.cs*ファイル) を選択します。

2. [ **表示** ] メニューの [ **デザイナー**] をクリックします。

3. リボンデザイナーで、任意のグループを右クリックし、[ **追加**] をクリックします。

     <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick>カスタムまたは組み込みダイアログボックスを開くには、グループのイベントにコードを追加します。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [リボンデザイナー](../vsto/ribbon-designer.md)
- [リボンオブジェクトモデルの概要](../vsto/ribbon-object-model-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [方法: リボンをリボンデザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)
- [方法: backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)
- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [方法: アドインのユーザーインターフェイスエラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: 実行時にリボンのコントロールを更新する](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [チュートリアル: リボン XML を使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
