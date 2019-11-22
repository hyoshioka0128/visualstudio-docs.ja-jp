---
title: ツールボックスの使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.chooseitems
- vs.toolboxpages.activexcontrols
- VS.CHOOSEITEMS.windowsuixamlcomponents
- VS.chooseitems.silverlightcomponents
- VC.EDITORS.RIBBON
- vs.customizetoolbox
- VS.chooseitems.System.Workflow_Components
- vs.chooseitems.frameworkcomponents
- VS.ToolboxPages..NET_Framework_Components
- VS.chooseitems.Microsoft.VisualStudio.Toolbox.VsToolboxPage
- vs.chooseitems.comcomponents
- vs.toolboxpages.NGWS_components
helpviewer_keywords:
- toolbox, adding items
- Visual Studio, toolbox
- toolbox, tabs
- toolbox
ms.assetid: 82e7cb43-4d0b-4e17-b7b0-43f96c22c3c2
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba8a37ac9e049455ffe19314dee0e228c3c14c97
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295606"
---
# <a name="using-the-toolbox"></a>ツールボックスの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ツールボックスを使用すると、コントロールなどの項目をプロジェクトに追加できます。 使用しているデザイナー画面にさまざまなコントロールをドラッグ アンド ドロップし、コントロールのサイズや位置を変更できます。

 ツールボックスは、XAML ファイルのデザイナー ビューなど、デザイナー ビューと組み合わせて表示されます。 ツールボックスには、現在のデザイナーで使用できるコントロールのみが表示されます。

 プロジェクトが対象とする .NET Framework バージョンも、ツールボックスに表示されるコントロール セットに影響します。 既定では、[!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] プロジェクトは .NET Framework 4.5.1 を対象とします。 プロジェクトが別のバージョンの .NET Framework を対象とするように設定するには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロパティ]、[アプリケーション]、[対象のフレームワーク]** の順にクリックします。

## <a name="managing-the-toolbox-and-its-controls"></a>ツールボックスと含まれるコントロールの管理
 既定では、ツールボックスは、Visual Studio IDE の左側に沿って折りたたまれており、カーソルをそこに移動すると開きます。 カーソルを移動したときに開いたままになるように、ツールボックスを固定することもできます (ツールボックス ツール バーの **[ピン]** アイコンをクリックします)。 また、ツールボックス ウィンドウをドッキング解除して、画面上の任意の場所にドラッグすることもできます。 ツールボックス ツール バーを右クリックし、いずれかのオプションを選択することで、ツールボックスのドッキング、ドッキング解除、および非表示を設定できます。

 コンテキスト メニューの次のコマンドを使用すると、ツールボックス タブの項目を再配置することも、カスタム タブやカスタム項目を追加することもできます。

- **[項目名の変更]** - 選択された項目の名前を変更します。

- **[すべて表示]** - 使用可能なコントロールをすべて (現在のデザイナーに適用されるコントロール以外も) 表示します。

- **[一覧の表示]** - コントロールを垂直方向に一覧表示します。 オフの場合は、コントロールが水平方向に表示されます。

- **[アイテムの選択]** - **[ツールボックス アイテムの選択]** ダイアログ ボックスが開き、 **[ツールボックス]** に表示する項目を指定できます。 チェック ボックスをオンまたはオフにすることで、項目の表示と非表示を切り替えることができます。

- **[アイテムをアルファベット順に並べ替え]** - 項目を名前順に並べ替えます。

- **[ツール バーのリセット]** - 既定のツールボックス設定および項目を復元します。

- **[タブの追加]** - 新しいツールボックス タブを追加します。

- **[上へ移動]** - 選択した項目を上へ移動します。

- **[下へ移動]** - 選択した項目を下へ移動します。

## <a name="creating-and-distributing-custom-toolbox-controls"></a>カスタム ツールボックス コントロールの作成と配布
 カスタム ツールボックス コントロールを Visual Basic または Visual C# で作成して、[Windows Presentation Foundation](../extensibility/creating-a-wpf-toolbox-control.md) または [Windows フォーム](../misc/how-to-create-a-toolbox-control-that-uses-windows-forms.md)に基づくプロジェクト テンプレートで開始できます。 これで、[ツールボックス コントロール インストーラー](http://www.unicode.org/versions/Unicode5.2.0/ch04.pdf)を使用してコントロールをチームメイトに配信したり、Web 上に公開したりできるようになります。
