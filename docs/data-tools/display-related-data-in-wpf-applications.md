---
title: WPF アプリケーションで関連データを表示する
description: WPF アプリケーションで関連データを表示します。 親子のリレーションシップで相互に関連付けられている複数のテーブルまたはエンティティのデータを操作します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: a9604ac7c0083bc40edb17b19d4de608eb7366b1
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436499"
---
# <a name="display-related-data-in-wpf-applications"></a>WPF アプリケーションで関連データを表示する

アプリケーションによっては、親子関係で相互に関連付けられている複数のテーブルまたはエンティティからのデータを処理することが必要になる場合があります。 たとえば、テーブルの顧客を表示するグリッドを表示する場合があり `Customers` ます。 ユーザーが特定の顧客を選択すると、その顧客の注文が関連テーブルから表示され `Orders` ます。

[ **データソース** ] ウィンドウから WPF デザイナーに項目をドラッグすることによって、関連データを表示するデータバインドコントロールを作成できます。

## <a name="to-create-controls-that-display-related-records"></a>関連するレコードを表示するコントロールを作成するには

1. **[データ]** メニューの **[データ ソースの表示]** をクリックして **[データ ソース]** ウィンドウを開きます。

2. **[新しいデータ ソースの追加]** をクリックして、 **データ ソース構成ウィザード** の操作を完了します。

3. WPF デザイナーを開き、[ **データソース** ] ウィンドウ内の項目の有効なドロップ先であるコンテナーがデザイナーに含まれていることを確認します。

     有効なドロップターゲットの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

4. [ **データソース** ] ウィンドウで、リレーションシップの親テーブルまたはオブジェクトを表すノードを展開します。 親テーブルまたは親オブジェクトは、一対多のリレーションシップの "一" 側にあります。

5. デザイナーの [ **データソース** ] ウィンドウから、親ノード (または親ノード内の個々のアイテム) をドラッグします。

     Visual Studio では、ドラッグする項目ごとに新しいデータバインドコントロールを作成する XAML が生成されます。 また、XAML は、 <xref:System.Windows.Data.CollectionViewSource> 親テーブルまたはオブジェクトの新しいをドロップ先のリソースに追加します。 一部のデータソースでは、Visual Studio によって、親テーブルまたはオブジェクトにデータを読み込むためのコードも生成されます。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

6. [ **データソース** ] ウィンドウで、関連する子テーブルまたはオブジェクトを見つけます。 関連する子テーブルおよびオブジェクトは、親ノードのデータリストの下部に展開可能なノードとして表示されます。

7. [ **データソース** ] ウィンドウから、子ノード (または子ノードの個々の項目) をデザイナーの有効なドロップ先にドラッグします。

     Visual Studio では、ドラッグする各項目に対して新しいデータバインドコントロールを作成する XAML が生成されます。 また、XAML は、 <xref:System.Windows.Data.CollectionViewSource> 子テーブルまたはオブジェクトの新しいをドロップ先のリソースに追加します。 この新しい <xref:System.Windows.Data.CollectionViewSource> は、デザイナーにドラッグした親テーブルまたはオブジェクトのプロパティにバインドされています。 一部のデータソースでは、Visual Studio によって、子テーブルまたはオブジェクトにデータを読み込むためのコードも生成されます。

     次の図は、[ **データソース** ] ウィンドウのデータセットにある **Customers** テーブルの関連する **Orders** テーブルを示しています。

     ![関係を示すデータ ソース ウィンドウ](../data-tools/media/datasources2.gif)

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [WPF アプリケーションでルックアップ テーブルを作成する](../data-tools/create-lookup-tables-in-wpf-applications.md)
