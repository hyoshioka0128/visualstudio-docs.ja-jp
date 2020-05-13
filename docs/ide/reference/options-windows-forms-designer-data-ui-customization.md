---
title: '[オプション]、[Windows フォームデザイナー]、[データ UI カスタマイズ]'
ms.date: 08/09/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.WindowsFormsDesigner.Data_UI_Customization
helpviewer_keywords:
- Data UI customization options
- Options dialog box, Windows Forms Designer, Data UI Customization
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: e48777a50ddf66a8e5493698fb401ff7201de03e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114693"
---
# <a name="options-dialog-box-windows-forms-designer--data-ui-customization"></a>[オプション] ダイアログ ボックス:[Windows フォーム デザイナー] > [データ UI カスタマイズ]

このダイアログ ボックスでは、[データ ソース] ウィンドウの項目に対して使用できるコントロールの一覧に表示されるコントロールを定義します。 それを開くには、 **[ツール]**  >  **[オプション]** の順に選択し、 **[Windows フォーム デザイナー]**  >  **[データ UI カスタマイズ]** を選択します。

Windows フォーム アプリのフォームにドラッグする前に、[データ ソース] ウィンドウの項目からコントロールを選択することができます。 使用できるコントロールは、項目のデータ型によって決まります。 各データ型には、このダイアログ ボックスで定義されている、既定のコントロールを含む有効なコントロールの一覧が、関連付けられています。 コントロールを選択せずに [データ ソース] ウィンドウからフォームに項目をドラッグすると、選択した項目のデータ型に対する既定のコントロールがフォームに追加されます。

関連付けられているコントロールの一覧をカスタマイズするには、各データ型で使用可能なコントロールのチェック ボックスをオンまたはオフにします。 一覧にコントロールを追加するには、<xref:System.ComponentModel.DefaultBindingPropertyAttribute> または <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> データ バインディング属性が実装されているコントロールを、ツールボックスに追加します。 その後、コントロールはデータ型に対するコントロールの一覧に表示されます。 詳細については、[[データ ソース] ウィンドウにカスタム コントロールを追加する](../..//data-tools/add-custom-controls-to-the-data-sources-window.md)」をご覧ください。

## <a name="data-type"></a>データの種類

コントロールを関連付ける型の一覧が表示されます。 テーブルは `[List]` データ型として表されます。 列は、基になっているデータ ストア内の列の実際のデータ型として表されます。

## <a name="associated-controls"></a>関連付けられたコントロール

選択したデータ型に関連付けられているコントロールの一覧が表示されます。 関連付けたり、関連付けを解除したりするには、コントロールの横にあるチェック ボックスをオンまたはオフにします。 選択したコントロールは、関連付けられたデータ型にバインドされているデータベース列の [データ ソース] ウィンドウに表示されます。

## <a name="set-default"></a>既定値の設定

選択したコントロールの種類を、選択したデータ型の既定値として割り当てます。 既定のコントロールは、[データ ソース] ウィンドウのデータベース列のショートカット メニューで、最初の選択肢として表示されます。 コントロールを選択せずに [データ ソース] ウィンドウからフォームに項目をドラッグすると、選択した項目のデータ型に対する既定のコントロールがフォームに追加されます。

データ型の既定値として割り当てることができるコントロールの種類は 1 つだけです。

## <a name="clear-default"></a>既定値のクリア

選択したデータ型の既定値としてのコントロールの指定を削除します。 選択したデータ型に既定値がない場合は、その型のデータベース列に対するショートカット メニューの最初の選択肢として、`[None]` が表示されます。
