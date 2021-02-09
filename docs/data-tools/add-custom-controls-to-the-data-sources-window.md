---
title: '[データ ソース] ウィンドウにカスタム コントロールを追加する'
description: Visual Studio の [データソース] ウィンドウにカスタムコントロールを追加します。 バインド可能なコントロールの一覧をカスタマイズします。 関連付けられたコントロールを追加します。
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
author: ghogen
ms.author: ghogen
manager: jmartens
ms.openlocfilehash: 5591dc9c3422918fa8f9c605105ea10c8fbc447d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867426"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>[データ ソース] ウィンドウにカスタム コントロールを追加する

[データソース] ウィンドウからデザインサーフェイスに項目をドラッグしてデータバインドコントロールを作成する場合、作成するコントロールの種類を選択できます。 ウィンドウの各項目には、選択できるコントロールを表示するドロップダウンリストがあります。 各項目に関連付けられているコントロールのセットは、項目のデータ型によって決まります。 作成するコントロールが一覧に表示されない場合は、このトピックの手順に従って、コントロールをリストに追加できます。

[データソース] ウィンドウでアイテムに対して作成するデータバインドコントロールの選択の詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)する」を参照してください。

## <a name="customize-the-bindable-controls-list"></a>バインド可能なコントロールの一覧をカスタマイズする

特定のデータ型の [データソース] ウィンドウの項目に対して使用可能なコントロールの一覧からコントロールを追加または削除するには、次の手順を実行します。

### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>データ型について一覧表示するコントロールを選択するには

1. WPF デザイナーまたは Windows フォーム デザイナーが開いていることを確認します。

2. [ **データソース** ] ウィンドウで、ウィンドウに追加したデータソースの一部であるアイテムをクリックし、アイテムのドロップダウンメニューをクリックします。

   > [!TIP]
   > [データソース] ウィンドウが開いていない場合は、[  >  **他の Windows**  >  **データソース** を表示] を選択して開きます。

3. ドロップダウンメニューで、[ **カスタマイズ**] をクリックします。 次のいずれかのダイアログボックスが表示されます。

    - **Windows フォームデザイナー** が開いている場合は、[**オプション**] ダイアログボックスの [**データ UI のカスタマイズ**] ページが表示されます。 詳細については、「[ [データ UI のカスタマイズオプション] ダイアログボックス](../ide/reference/options-windows-forms-designer-data-ui-customization.md)」を参照してください。

    - **WPF デザイナー** が開いている場合は、[**コントロールのバインドのカスタマイズ**] ダイアログボックスが表示されます。

4. ダイアログボックスで、[ **データ型** ] ドロップダウンリストからデータ型を選択します。

    - テーブルまたはオブジェクトのコントロールの一覧をカスタマイズするには、 **[一覧]** を選択します。

    - テーブルの列またはオブジェクトのプロパティのコントロールの一覧をカスタマイズするには、基になるデータストアの列またはプロパティのデータ型を選択します。

    - ユーザー定義の図形を持つデータオブジェクトを表示するようにコントロールの一覧をカスタマイズするには、 **[その他]** を選択します。 たとえば、アプリケーションに、特定のオブジェクトの複数のプロパティのデータを表示するカスタムコントロールがある場合は、 **[Other]** を選択します。

5. [ **関連付けられたコントロール** ] ボックスで、選択したデータ型で使用できるようにする各コントロールを選択するか、一覧から削除するコントロールの選択を解除します。

    > [!NOTE]
    > 選択するコントロールが [ **関連付けられたコントロール** ] ボックスに表示されない場合は、そのコントロールをリストに追加する必要があります。 詳細については、「 [関連付けられたコントロールの追加](#add-associated-controls)」を参照してください。

6. **[OK]** をクリックします。

7. [ **データソース** ] ウィンドウで、1つまたは複数のコントロールに関連付けたデータ型の項目をクリックし、その項目のドロップダウンメニューをクリックします。

     [ **関連付けられたコントロール** ] ボックスで選択したコントロールが、その項目のドロップダウンメニューに表示されるようになります。

## <a name="add-associated-controls"></a>関連付けられたコントロールの追加

コントロールをデータ型に関連付けようとしていても、コントロールが [ **関連付けられたコントロール** ] ボックスに表示されない場合は、コントロールをリストに追加する必要があります。 コントロールは、現在のソリューションまたは参照アセンブリに配置されている必要があります。 また、 **ツールボックス** で使用可能であり、コントロールのデータバインディング動作を指定する属性を持っている必要があります。

関連付けられたコントロールの一覧にコントロールを追加するには、次のようにします。

1. ツール **ボックスを右クリックし、** [項目の **選択]** を選択して、目的のコントロールを **ツールボックス** に追加します。

     コントロールには、次のいずれかの属性が必要です。

    |属性|説明|
    |---------------|-----------------|
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|などのデータの単一の列またはプロパティを表示する単純なコントロールに対して、この属性を実装 <xref:System.Windows.Forms.TextBox> します。|
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|などのデータのリスト (またはテーブル) を表示するコントロールに対して、この属性を実装 <xref:System.Windows.Forms.DataGridView> します。|
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|この属性は、データのリスト (またはテーブル) を表示するコントロールに実装しますが、1つの列またはプロパティ (など) を提示する必要もあり <xref:System.Windows.Forms.ComboBox> ます。|

2. Windows フォームの場合は、[ **オプション** ] ダイアログボックスで [ **データ UI のカスタマイズ** ] ページを開きます。 または、WPF の場合は、[ **コントロールのバインドのカスタマイズ** ] ダイアログボックスを開きます。 詳細については、「 [データ型のバインド可能なコントロールの一覧をカスタマイズ](#customize-the-bindable-controls-list)する」を参照してください。

3. [ **関連付けられたコントロール** ] ボックスに、 **ツールボックス** に追加したコントロールが表示されます。

    > [!NOTE]
    > 関連付けられたコントロールの一覧に追加できるのは、現在のソリューション内または参照されたアセンブリ内にあるコントロールだけです。 (コントロールは、前の表のいずれかのデータバインディング属性も実装する必要があります)。[データソース] ウィンドウで使用できないカスタムコントロールにデータをバインドするには、[ **ツールボックス** ] からデザインサーフェイスにコントロールをドラッグし、[バインド先] 項目を [ **データソース** ] ウィンドウからコントロールにドラッグします。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [[データ UI カスタマイズオプション] ダイアログボックス](../ide/reference/options-windows-forms-designer-data-ui-customization.md)
