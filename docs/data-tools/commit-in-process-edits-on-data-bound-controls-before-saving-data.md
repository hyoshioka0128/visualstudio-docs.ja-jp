---
title: コミットされていない編集
description: データを保存する前に、データバインド Windows フォームコントロールのインプロセス編集をコミットします。 フォーム上のすべての BindingSource コンポーネントに対して EndEdit を呼び出します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- committing edited records
- data-bound controls, in-process edits
- DataBinding class, committing edited records
- hierarchical update, committing edited records
- BindingSource class, committing edited records
- EndEdit method
ms.assetid: 61af4798-eef7-468c-b229-5e1497febb2f
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: cd50ad6c0e81f337ad922f6fa994f0d900edb8b6
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382391"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>データの保存前にデータ バインド コントロールで実行中の編集をコミットする

データバインドコントロールの値を編集する場合、ユーザーは現在のレコードから移動して、更新された値をコントロールがバインドされている基になるデータソースにコミットする必要があります。 [ [データソース] ウィンドウ](add-new-data-sources.md) からフォームに項目をドラッグすると、ドロップした最初の項目によって、の [ **保存** ] ボタンクリックイベントにコードが生成され <xref:System.Windows.Forms.BindingNavigator> ます。 このコード <xref:System.Windows.Forms.BindingSource.EndEdit%2A> は、のメソッドを呼び出し <xref:System.Windows.Forms.BindingSource> ます。 したがって、メソッドの呼び出し <xref:System.Windows.Forms.BindingSource.EndEdit%2A> は、フォームに追加された最初のに対してのみ生成され <xref:System.Windows.Forms.BindingSource> ます。

<xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは、現在編集中のデータ バインド コントロールで実行されている変更をコミットします。 したがって、あるデータ バインド コントロールにフォーカスがある状態で **[保存]** ボタンをクリックすると、実際の保存 (`TableAdapterManager.UpdateAll` メソッド) が実行される前に、そのコントロール内のすべての保留中の編集がコミットされます。

保存プロセスの一環として、変更をコミットせずにユーザーがデータを保存しようとした場合でも、変更を自動的にコミットするようにアプリケーションを構成できます。

> [!NOTE]
> デザイナーは、 `BindingSource.EndEdit` フォームにドロップされた最初の項目に対してのみコードを追加します。 したがって、 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> フォーム上の各に対してメソッドを呼び出すコード行を追加する必要があり <xref:System.Windows.Forms.BindingSource> ます。 コード行を手動で追加 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> して、それぞれに対してメソッドを呼び出すことができ <xref:System.Windows.Forms.BindingSource> ます。 または、 `EndEditOnAllBindingSources` メソッドをフォームに追加して、保存を実行する前に呼び出すこともできます。

次のコードでは、 [LINQ (統合言語クエリ)](/dotnet/csharp/linq/) クエリを使用し <xref:System.Windows.Forms.BindingSource> てすべてのコンポーネントを反復処理し、 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> フォーム上の各に対してメソッドを呼び出し <xref:System.Windows.Forms.BindingSource> ます。

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>フォーム上のすべての BindingSource コンポーネントに対して EndEdit を呼び出すには

1. コンポーネントを含むフォームに次のコードを追加し <xref:System.Windows.Forms.BindingSource> ます。

     [!code-csharp[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.vb)]

2. フォームのデータを保存するための呼び出しの直前に、次のコード行を追加し `TableAdapterManager.UpdateAll()` ます (メソッド)。

     [!code-csharp[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [階層更新](../data-tools/hierarchical-update.md)
