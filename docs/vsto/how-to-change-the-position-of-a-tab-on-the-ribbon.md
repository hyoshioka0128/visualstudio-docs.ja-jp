---
title: '方法: リボンのタブの位置を変更する'
description: リボンのカスタムタブの順序を変更したり、タブコレクションエディターを使用して、リボン上の組み込みタブの前または後にカスタムタブを配置したりすることができます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dc0b4548ffa4e5efa75734b5528a7021cf122bfa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921914"
---
# <a name="how-to-change-the-position-of-a-tab-on-the-ribbon"></a>方法: リボンのタブの位置を変更する
  リボンのカスタムタブの順序は、 **タブコレクションエディター** を使用して変更できます。 リボンの組み込みタブの前または後にカスタムタブを配置できます。 組み込みタブは、Microsoft Office アプリケーションのリボンに用意されているタブです。 たとえば、[ **データ** ] タブは Excel の組み込みタブです。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-change-the-order-of-tabs-on-the-ribbon"></a>リボンのタブの順序を変更するには

1. **ソリューションエクスプローラー** でリボンコードファイル (*.vb* または *.cs* ファイル) を選択します。

2. [ **表示** ] メニューの [ **デザイナー**] をクリックします。

3. リボンデザイナーを右クリックし、[ **プロパティ**] をクリックします。

4. [ **プロパティ** ] ウィンドウで、[ **タブ** ] プロパティを選択し、省略記号ボタン (![ASP.NET mobile designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

     **タブコレクションエディター** が表示されます。

5. **タブコレクションエディター** の [**メンバー** ] ボックスの一覧で、移動するタブを選択し、上矢印または下矢印をクリックしてタブオーダーを変更します。

### <a name="to-position-a-tab-before-or-after-a-built-in-tab-on-the-ribbon"></a>リボン上の組み込みタブの前または後にタブを配置するには

1. リボンデザイナーで、[カスタム] タブを選択します。

2. [ **プロパティ** ] ウィンドウで、[ **ControlId** ] プロパティを展開し、[制御 **lidtype** ] プロパティの値が " **カスタム**" に設定されていることを確認します。

3. [ **プロパティ** ] ウィンドウで、[ **位置** ] プロパティを展開します。

4. **Positiontype** プロパティを適切な値に設定します。

    - **Beforeofficeid** は、指定された組み込みタブの前にグループを配置します。

    - **Afterofficeid** は、指定された組み込みタブの後にグループを配置します。

5. **Officeid** プロパティを組み込みタブのコントロール ID に設定します。

     コントロール Id の一覧については、「 [office 2010 のヘルプファイル: office fluent ユーザーインターフェイスコントロールの識別子](https://www.microsoft.com/download/details.aspx?id=6627)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: リボン XML を使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
