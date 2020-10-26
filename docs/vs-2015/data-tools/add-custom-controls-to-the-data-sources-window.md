---
title: '[データソース] ウィンドウにカスタムコントロールを追加する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 402e62602d99492730d3094965e76964cd5f8218
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673095"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>[データ ソース] ウィンドウにカスタム コントロールを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **データソース** ] ウィンドウからデザインサーフェイスに項目をドラッグしてデータバインドコントロールを作成する場合、作成するコントロールの種類を選択できます。 ウィンドウの各項目には、選択できるコントロールを表示するドロップダウンリストがあります。 各項目に関連付けられているコントロールのセットは、項目のデータ型によって決まります。 作成するコントロールが一覧に表示されない場合は、このトピックの手順に従って、コントロールをリストに追加できます。

 [データ **ソース** ] ウィンドウでアイテムに対して作成するデータバインドコントロールの選択の詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)する」を参照してください。

> [!NOTE]
> 使用している設定またはエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。 設定を変更するには、[ **ツール** ] メニューの [ **設定のインポートとエクスポート**] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="customize-the-list-of-bindable-controls-for-a-data-type"></a><a name="customizinglist"></a> データ型のバインド可能なコントロールの一覧をカスタマイズする
 特定のデータ型の [ **データソース** ] ウィンドウの項目に対して使用可能なコントロールの一覧からコントロールを追加または削除するには、次の手順を実行します。

#### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>データ型について一覧表示するコントロールを選択するには

1. WPF デザイナーまたは Windows フォーム デザイナーが開いていることを確認します。

2. [ **データソース** ] ウィンドウで、ウィンドウに追加したデータソースの一部であるアイテムをクリックし、アイテムのドロップダウンメニューをクリックします。

3. ドロップダウンメニューで、[ **カスタマイズ**] をクリックします。 次のいずれかのダイアログボックスが表示されます。

    - Windows フォームデザイナーが開いている場合は、[**オプション**] ダイアログボックスの [**データ UI のカスタマイズ**] ページが表示されます。

    - WPF デザイナーが開いている場合は、[ **コントロールのバインドのカスタマイズ** ] ダイアログボックスが表示されます。

4. ダイアログボックスで、[ **データ型** ] ドロップダウンリストからデータ型を選択します。

    - テーブルまたはオブジェクトのコントロールの一覧をカスタマイズするには、 **[一覧]** を選択します。

    - テーブルの列またはオブジェクトのプロパティのコントロールの一覧をカスタマイズするには、基になるデータストアの列またはプロパティのデータ型を選択します。

    - ユーザー定義の図形を持つデータオブジェクトを表示するようにコントロールの一覧をカスタマイズするには、 **[その他]** を選択します。 たとえば、アプリケーションに、特定のオブジェクトの複数のプロパティのデータを表示するカスタムコントロールがある場合は、 **[Other]** を選択します。

5. [ **関連付けられたコントロール** ] ボックスで、選択したデータ型で使用できるようにする各コントロールを選択するか、一覧から削除するコントロールの選択を解除します。

    > [!NOTE]
    > 選択するコントロールが [ **関連付けられたコントロール** ] ボックスに表示されない場合は、そのコントロールをリストに追加する必要があります。 詳細については、「 [データ型に関連付けられているコントロールのリストへのコントロールの追加](#addingcontrols)」を参照してください。

6. **[OK]** をクリックします。

7. [ **データソース** ] ウィンドウで、1つまたは複数のコントロールに関連付けたデータ型の項目をクリックし、その項目のドロップダウンメニューをクリックします。

     [ **関連付けられたコントロール** ] ボックスで選択したコントロールが、その項目のドロップダウンメニューに表示されるようになります。

## <a name="addcontrols-to-the-list-of-associated-controls-for-a-data-type"></a><a name="addingcontrols"></a> データ型に関連付けられているコントロールの一覧に対する addcontrols
 コントロールをデータ型に関連付けようとしていても、コントロールが [ **関連付けられたコントロール** ] ボックスに表示されない場合は、コントロールをリストに追加する必要があります。 コントロールは、現在のソリューションまたは参照アセンブリに配置されている必要があります。 また、 **ツールボックス**でも使用可能であり、コントロールのデータバインディング動作を指定する属性を持っている必要があります。

#### <a name="to-add-controls-to-the-list-of-associated-controls"></a>関連付けられたコントロールの一覧にコントロールを追加するには

1. ツール**ボックスを右クリックし、** [項目の**選択]** を選択して、目的のコントロールを**ツールボックス**に追加します。

     コントロールには、次のいずれかの属性が必要です。

    |属性|説明|
    |---------------|-----------------|
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|などのデータの単一の列またはプロパティを表示する単純なコントロールに対して、この属性を実装 <xref:System.Windows.Forms.TextBox> します。|
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|などのデータのリスト (またはテーブル) を表示するコントロールに対して、この属性を実装 <xref:System.Windows.Forms.DataGridView> します。|
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|この属性は、データのリスト (またはテーブル) を表示するコントロールに実装しますが、1つの列またはプロパティ (など) を提示する必要もあり <xref:System.Windows.Forms.ComboBox> ます。|

2. Windows フォームの場合は、[      **オプション** ] ダイアログボックスで [ **データ UI のカスタマイズ** ] ページを開きます。 または、WPF の場合は、[ **コントロールのバインドのカスタマイズ** ] ダイアログボックスを開きます。 詳細については、「 [データ型のバインド可能なコントロールのリストのカスタマイズ](#customizinglist)」を参照してください。

3. [ **関連付けられたコントロール** ] ボックスに、 **ツールボックス** に追加したコントロールが表示されます。

    > [!NOTE]
    > 関連付けられたコントロールの一覧に追加できるのは、現在のソリューション内または参照されたアセンブリ内にあるコントロールだけです。 (コントロールは、前の表のいずれかのデータバインディング属性も実装する必要があります)。[ **データソース** ] ウィンドウで使用できないカスタムコントロールにデータをバインドするには、[ **ツールボックス** ] からデザインサーフェイスにコントロールをドラッグし、[バインド先] 項目を [ **データソース** ] ウィンドウからコントロールにドラッグします。

## <a name="see-also"></a>参照
 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
