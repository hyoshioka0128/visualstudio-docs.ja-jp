---
title: データベースの画像にコントロールをバインドする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- images [Visual Basic], displaying on Windows Forms
- data binding [Windows Forms], pictures
- images [Visual Basic], data binding
- pictures, data binding
- pictures, dragging from Data Sources window
- Data Sources Window, setting controls to display images
- PictureBox control [Windows Forms], data binding
- images [Visual Basic], dragging from Data Sources window
ms.assetid: 9748815e-3556-49e8-86b1-c6aa593c6163
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0b8f6ee192399c8af8a508b2f9c2817db954bb36
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673011"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>データベースの画像にコントロールをバインドする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[データ ソース]** ウィンドウを使用して、データベースのイメージをアプリケーションのコントロールにバインドできます。 たとえば、WPF アプリケーションの <xref:System.Windows.Controls.Image> コントロールまたは Windows フォーム アプリケーションの <xref:System.Windows.Forms.PictureBox> コントロールにイメージをバインドできます。

 データベースの画像は、通常はバイト配列として格納されます。 **[データ ソース]** ウィンドウ内のバイト配列として格納されている項目は、既定ではコントロール型が **[なし]** に設定されています。これは、バイト配列には、シンプルなバイトの配列から大規模なアプリケーションの実行可能ファイルまで、どのようなものでも含めることができるためです。 **[データ ソース]** ウィンドウ内のイメージを表すバイト配列項目のデータ バインド コントロールを作成するには、作成するコントロールを選択する必要があります。

 次の手順では、イメージにバインドされている項目が既に **[データ ソース]** ウィンドウに作成されていると仮定します。

## <a name="bind-a-picture-in-a-database-to-a-control"></a>データベース内の画像をコントロールにバインドする

1. コントロールを追加するデザイン サーフェイスが WPF デザイナーまたは Windows フォーム デザイナーで開いていることを確認します。

2. **[データ ソース]** ウィンドウで、目的のテーブルまたはオブジェクトを展開して、その列またはプロパティを表示します。

3. イメージ データを含む列またはプロパティを選択し、ドロップダウン コントロール リストから次のいずれかのコントロールを選択します。

    - WPF デザイナーが開いている場合は、**[Image]** を選択します。

    - Windows フォーム デザイナーが開いている場合は、**[PictureBox]** を選択します。

    - または、データ バインディングをサポートし、かつイメージを表示できる、別のコントロールを選択することもできます。 使用するコントロールが利用できるコントロールのリストに含まれていない場合は、そのコントロールをリストに追加してから選択できます。 詳細については、「 [[データソース] ウィンドウにカスタムコントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

## <a name="see-also"></a>参照
 [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)
