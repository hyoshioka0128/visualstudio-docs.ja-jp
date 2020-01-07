---
title: ツールボックス、[データ] タブ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Toolbox, Data tab
- Data tab, Toolbox
- data [Visual Studio], Toolbox
ms.assetid: 2ae38b2a-29d2-461c-a67d-29dad274bf45
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9349745eeee24f2f8b1e62eb2b01bd75273c86d8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658598"
---
# <a name="toolbox-data-tab"></a>ツールボックス、[データ] タブ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

フォームとコンポーネントに追加できるデータ オブジェクトを表示します。 作成しているプロジェクトに関連するデザイナーがあると、**ツールボックス**の **[データ]** タブが表示されます。 **ツールボックス**は、Visual Studio の統合開発環境 (IDE: Integrated Development Environment) に既定で表示されます。**ツールボックス**を表示する必要がある場合は、 **[表示]** メニューの **[ツールボックス]** をクリックします。

> [!TIP]
> データ ソース構成ウィザードを実行すると、ほとんどのデータ項目が自動的に作成され、構成されます。 詳細については、[Visual Studio を使ったデータ アプリケーションの作成](https://msdn.microsoft.com/28edce21-220a-484c-b461-a75b0232d293)に関するページをご覧ください。

## <a name="ui-element-list"></a>UI 要素の一覧
 コンポーネントに対する .NET Framework の参照ページを直接表示するには、**ツールボックス**の項目で、またはデザイナーのトレイにあるコンポーネントの項目で、**F1** キーを押します。

|name|説明|
|----------|-----------------|
|<xref:System.Data.DataSet>|型付きまたは型なしのデータセットのインスタンスをフォームまたはコンポーネントに追加します。 このオブジェクトをデザイナーにドラッグすると、ダイアログ ボックスが表示されて、既存の型指定されたデータセット クラスを選択、または新しいブランクの型指定されていないデータセットの作成を指定できます。 **注:** 新しい型指定されたデータセット スキーマおよびクラスを作成する場合、**ツールボックス**の <xref:System.Data.DataSet> オブジェクトは使用しません。 詳細については、[データセットの作成と構成](../../data-tools/create-and-configure-datasets-in-visual-studio.md)に関するページを参照してください。|
|<xref:System.Windows.Forms.DataGridView>|データを表形式で表示するための強力で柔軟な機能が用意されています。|
|<xref:System.Windows.Forms.BindingSource>|基になるデータ ソースにコントロールをバインドするプロセスを簡略化します。|
|<xref:System.Windows.Forms.BindingNavigator>|データにバインドされている、フォーム上のコントロールを移動および操作するためのユーザー インターフェイス (UI) を表します。|

## <a name="see-also"></a>関連項目
 [データチュートリアル](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4) [visual studio でデータに Windows フォームコントロールをバインド](../../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)する[Visual studio でデータを](../../data-tools/bind-controls-to-data-in-visual-studio.md)[受信するため](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)のデータバインドコントロールの準備[データの検証](https://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)
