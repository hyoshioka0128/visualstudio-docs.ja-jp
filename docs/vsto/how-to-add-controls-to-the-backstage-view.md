---
title: '方法: Backstage ビューにコントロールを追加する '
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, menus
- controls, Ribbon
- menus, customizing
- Microsoft Office Button
- custom Ribbon, menus
- Ribbon, customizing
- Office button
- Ribbon, menus
- Microsoft Office Menu
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5b4ea5cdcd869f16f987e9431359511831af9573
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538347"
---
# <a name="how-to-add-controls-to-the-backstage-view"></a>方法: Backstage ビューにコントロールを追加する
  リボンデザイナーを使用すると、[ **ファイル** ] タブをクリックしたときに表示されるメニューにコントロールを追加できます。アプリケーションを実行すると、[ **ファイル** ] タブに追加したコントロールに、 **アドイン**という名前のグループが表示されます。

 Visual Studio のリボンデザイナーを使用して、組み込みコントロールの前または後にコントロールを配置することはできません。 ビルトイン コントロールは、Backstage ビューで既に表示されているコントロールです。 組み込みコントロールの前または後にコントロールを配置する場合は、リボン XML を使用する必要があります。 **リボン (xml)** の詳細については、「[リボン xml](../vsto/ribbon-xml.md)」を参照してください。 Backstage ビューのカスタマイズの詳細については、「 [開発者向け office 2010 backstage ビューの概要](/previous-versions/office/developer/office-2010/ee691833(v=office.14)) 」および「 [開発者向けの office 2010 Backstage ビューのカスタマイズ](/previous-versions/office/developer/office-2010/ee815851(v=office.14))」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-controls-to-backstage-view"></a>Backstage ビューにコントロールを追加するには

1. デザインビューでリボン項目を開きます。

     **リボン (ビジュアルデザイナー)** 項目をプロジェクトに追加する方法については、「[方法: リボンのカスタマイズを開始](../vsto/how-to-get-started-customizing-the-ribbon.md)する」を参照してください。

2. リボンデザイナーで、[ **ファイル** ] タブをクリックします。

     メニューデザイナーが表示されます。 このデザインサーフェイスには、コントロールは含まれていません。

3. **ツールボックス**の [ **Office リボンコントロール**] タブから、次のコントロールのいずれかをメニューデザイナーにドラッグします。

    - Button

    - CheckBox

    - [ギャラリー]

    - メニュー

    - 区切り記号

    - SplitButton

    - ToggleButton

4. コントロールをドラッグして、メニューの新しい位置に移動します。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボンデザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
