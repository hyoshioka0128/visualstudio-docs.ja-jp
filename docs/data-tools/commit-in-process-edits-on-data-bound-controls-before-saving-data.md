---
title: 保存前にデータバインドコントロールのインプロセス編集をコミットする
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 4a708128f827568e072c617effff17129e41e558
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586940"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>データの保存前にデータ バインド コントロールで実行中の編集をコミットする

データバインドコントロールの値を編集する場合、ユーザーは現在のレコードから移動して、更新された値をコントロールがバインドされている基になるデータソースにコミットする必要があります。 [[データソース] ウィンドウ](add-new-data-sources.md)からフォームに項目をドラッグすると、ドロップした最初の項目によって、<xref:System.Windows.Forms.BindingNavigator>の **[保存]** ボタンクリックイベントにコードが生成されます。 このコードは、<xref:System.Windows.Forms.BindingSource>の <xref:System.Windows.Forms.BindingSource.EndEdit%2A> メソッドを呼び出します。 したがって、<xref:System.Windows.Forms.BindingSource.EndEdit%2A> メソッドへの呼び出しは、フォームに追加された最初の <xref:System.Windows.Forms.BindingSource> に対してのみ生成されます。

<xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは、現在編集中のデータ バインド コントロールで実行されている変更をコミットします。 したがって、あるデータ バインド コントロールにフォーカスがある状態で **[保存]** ボタンをクリックすると、実際の保存 (`TableAdapterManager.UpdateAll` メソッド) が実行される前に、そのコントロール内のすべての保留中の編集がコミットされます。

保存プロセスの一環として、変更をコミットせずにユーザーがデータを保存しようとした場合でも、変更を自動的にコミットするようにアプリケーションを構成できます。

> [!NOTE]
> デザイナーは、フォームにドロップされた最初の項目に対してのみ `BindingSource.EndEdit` コードを追加します。 そのため、フォームの各 <xref:System.Windows.Forms.BindingSource> に対して <xref:System.Windows.Forms.BindingSource.EndEdit%2A> メソッドを呼び出すコード行を追加する必要があります。 コード行を手動で追加して、<xref:System.Windows.Forms.BindingSource>ごとに <xref:System.Windows.Forms.BindingSource.EndEdit%2A> メソッドを呼び出すことができます。 または、`EndEditOnAllBindingSources` メソッドをフォームに追加して、保存を実行する前に呼び出すこともできます。

次のコードでは、 [LINQ (統合言語クエリ)](/dotnet/csharp/linq/)クエリを使用してすべての <xref:System.Windows.Forms.BindingSource> コンポーネントを反復処理し、フォーム上の各 <xref:System.Windows.Forms.BindingSource> の <xref:System.Windows.Forms.BindingSource.EndEdit%2A> メソッドを呼び出します。

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>フォーム上のすべての BindingSource コンポーネントに対して EndEdit を呼び出すには

1. <xref:System.Windows.Forms.BindingSource> コンポーネントを含むフォームに次のコードを追加します。

     [!code-csharp[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#1](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_1.vb)]

2. フォームのデータを保存するための呼び出しの直前に、次のコード行 (`TableAdapterManager.UpdateAll()` メソッド) を追加します。

     [!code-csharp[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/CSharp/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.cs)]
     [!code-vb[VSProDataOrcasEndEditOnAll#2](../data-tools/codesnippet/VisualBasic/commit-in-process-edits-on-data-bound-controls-before-saving-data_2.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [階層更新](../data-tools/hierarchical-update.md)
