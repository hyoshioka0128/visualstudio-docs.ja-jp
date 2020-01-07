---
title: ツールボックス、[データ] タブ
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Toolbox, Data tab
- Data tab, Toolbox
- data [Visual Studio], Toolbox
ms.assetid: 2ae38b2a-29d2-461c-a67d-29dad274bf45
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34707c39a14650023c9caa701813de65999010ef
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72644610"
---
# <a name="toolbox-data-tab"></a>ツールボックス、[データ] タブ

フォームとコンポーネントに追加できるデータ オブジェクトを表示します。 作成しているプロジェクトに関連するデザイナーがあると、**ツールボックス**の **[データ]** タブが表示されます。 **ツールボックス**は、Visual Studio の統合開発環境 (IDE: Integrated Development Environment) に既定で表示されます。**ツールボックス**を表示する必要がある場合は、 **[表示]** メニューの **[ツールボックス]** をクリックします。

> [!TIP]
> データ ソース構成ウィザードを実行すると、ほとんどのデータ項目が自動的に作成され、構成されます。 詳細については、「[新しいデータ ソースの追加](../../data-tools/add-new-data-sources.md)」を参照してください。

## <a name="ui-element-list"></a>UI 要素の一覧

コンポーネントに対する .NET の参照ページを直接表示するには、**ツールボックス**の項目で、またはデザイナーのトレイにあるコンポーネントの項目で、**F1** キーを押します。

|name|説明|
|----------|-----------------|
|<xref:System.Data.DataSet>|型付きまたは型なしのデータセットのインスタンスをフォームまたはコンポーネントに追加します。 このオブジェクトをデザイナーにドラッグすると、ダイアログ ボックスが表示されて、既存の型指定されたデータセット クラスを選択、または新しいブランクの型指定されていないデータセットの作成を指定できます。 **注:** 新しい型指定されたデータセット スキーマおよびクラスを作成する場合、**ツールボックス**の <xref:System.Data.DataSet> オブジェクトは使用しません。 詳細については、[データセットの作成と構成](../../data-tools/create-and-configure-datasets-in-visual-studio.md)に関するページを参照してください。|
|<xref:System.Windows.Forms.DataGridView>|データを表形式で表示するための強力で柔軟な機能が用意されています。|
|<xref:System.Windows.Forms.BindingSource>|基になるデータ ソースにコントロールをバインドするプロセスを簡略化します。|
|<xref:System.Windows.Forms.BindingNavigator>|データにバインドされている、フォーム上のコントロールを移動および操作するためのユーザー インターフェイス (UI) を表します。|

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../../data-tools/accessing-data-in-visual-studio.md)
- [.NET 用の Visual Studio データ ツール](../../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Visual Studio のデータセット ツール](../../data-tools/dataset-tools-in-visual-studio.md)
- [Visual Studio でのデータへのコントロールのバインド](../../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [データセットのデータの編集](../../data-tools/edit-data-in-datasets.md)
- [データセットのデータの検証](../../data-tools/validate-data-in-datasets.md)
