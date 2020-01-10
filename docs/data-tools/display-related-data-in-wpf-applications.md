---
title: WPF アプリケーションで関連データを表示する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 3aa80194-0191-474d-9d28-5ec05654b426
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 6ab1301e421f8326cf4cdda97556ecb19e394c29
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586680"
---
# <a name="display-related-data-in-wpf-applications"></a>WPF アプリケーションで関連データを表示する

アプリケーションによっては、親子関係で相互に関連付けられている複数のテーブルまたはエンティティからのデータを処理することが必要になる場合があります。 たとえば、`Customers` テーブルの顧客を表示するグリッドを表示する場合があります。 ユーザーが特定の顧客を選択すると、関連する `Orders` テーブルから、その顧客の注文が別のグリッドに表示されます。

**[データソース]** ウィンドウから WPF デザイナーに項目をドラッグすることによって、関連データを表示するデータバインドコントロールを作成できます。

## <a name="to-create-controls-that-display-related-records"></a>関連するレコードを表示するコントロールを作成するには

1. **[データ]** メニューの **[データ ソースの表示]** をクリックして **[データ ソース]** ウィンドウを開きます。

2. **[新しいデータ ソースの追加]** をクリックして、**データ ソース構成ウィザード**の操作を完了します。

3. WPF デザイナーを開き、 **[データソース]** ウィンドウ内の項目の有効なドロップ先であるコンテナーがデザイナーに含まれていることを確認します。

     有効なドロップターゲットの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

4. **[データソース]** ウィンドウで、リレーションシップの親テーブルまたはオブジェクトを表すノードを展開します。 親テーブルまたは親オブジェクトは、一対多のリレーションシップの "一" 側にあります。

5. デザイナーの **[データソース]** ウィンドウから、親ノード (または親ノード内の個々のアイテム) をドラッグします。

     Visual Studio では、ドラッグする項目ごとに新しいデータバインドコントロールを作成する XAML が生成されます。 また、XAML は、親テーブルまたはオブジェクトの新しい <xref:System.Windows.Data.CollectionViewSource> をドロップ先のリソースに追加します。 一部のデータソースでは、Visual Studio によって、親テーブルまたはオブジェクトにデータを読み込むためのコードも生成されます。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

6. **[データソース]** ウィンドウで、関連する子テーブルまたはオブジェクトを見つけます。 関連する子テーブルおよびオブジェクトは、親ノードのデータリストの下部に展開可能なノードとして表示されます。

7. **[データソース]** ウィンドウから、子ノード (または子ノードの個々の項目) をデザイナーの有効なドロップ先にドラッグします。

     Visual Studio では、ドラッグする各項目に対して新しいデータバインドコントロールを作成する XAML が生成されます。 また、XAML は、子テーブルまたはオブジェクトの新しい <xref:System.Windows.Data.CollectionViewSource> をドロップ先のリソースに追加します。 この新しい <xref:System.Windows.Data.CollectionViewSource> は、デザイナーにドラッグした親テーブルまたはオブジェクトのプロパティにバインドされます。 一部のデータソースでは、Visual Studio によって、子テーブルまたはオブジェクトにデータを読み込むためのコードも生成されます。

     次の図は、 **[データソース]** ウィンドウのデータセットにある**Customers**テーブルの関連する**Orders**テーブルを示しています。

     ![関係を示すデータ ソース ウィンドウ](../data-tools/media/datasources2.gif)

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [WPF アプリケーションでルックアップ テーブルを作成する](../data-tools/create-lookup-tables-in-wpf-applications.md)
