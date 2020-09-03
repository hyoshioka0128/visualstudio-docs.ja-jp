---
title: '方法: リボンのカスタマイズを開始する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, adding Ribbon to project
- Ribbon [Office development in Visual Studio], adding
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, adding Ribbon to project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: be311f87862f4447d903294508927735d3507b08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85520069"
---
# <a name="how-to-get-started-customizing-the-ribbon"></a>方法: リボンのカスタマイズを開始する
  Microsoft Office アプリケーションのリボンをカスタマイズするには、Office プロジェクトに **リボン (ビジュアルデザイナー)** または **リボン (XML)** 項目を追加します。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-ribbon-to-a-project"></a>プロジェクトにリボンを追加するには

1. [ **プロジェクト** ] メニューの [ **新しい項目の追加**] をクリックします。

2. [ **新しい項目の追加** ] ダイアログボックスで、 **リボン (ビジュアルデザイナー)** または **リボン (XML)** を選択します。 これらのテンプレートの詳細については、「 [リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

3. [ **名前** ] ボックスに、リボン項目の名前を入力します。

    次の文字は名前に使用できません。

   - シャープ記号 (#)

   - パーセント (%)

   - アンパサンド (&)

   - アスタリスク (*)

   - 縦棒 (|)

   - 円記号 (\\)

   - コロン (:)

   - 二重引用符 (")

   - より小さい (\<)

   - より大きい (>)

   - 疑問符 (?)

   - スラッシュ (/)

   - 先頭または末尾の空白 (' ')

   - Windows または DOS 用に予約されている名前 ("nul"、"aux"、"con"、"com1"、"lpt1" など)

4. **[OK]** をクリックします。

   リボン項目が **ソリューションエクスプローラー**に表示されます。 次の手順の詳細については、「 [リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンデザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: リボン XML を使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
