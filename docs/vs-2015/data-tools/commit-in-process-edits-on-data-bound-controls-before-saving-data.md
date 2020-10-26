---
title: データを保存する前にデータバインドコントロールのインプロセス編集をコミットする |Microsoft Docs
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
- committing edited records
- data-bound controls, in-process edits
- DataBinding class, committing edited records
- hierarchical update, committing edited records
- BindingSource class, committing edited records
- EndEdit method
ms.assetid: 61af4798-eef7-468c-b229-5e1497febb2f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3867b91a8b417b5670514b66aaf93fdab4e9618c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662449"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>データの保存前にデータ バインド コントロールで実行中の編集をコミットする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データバインドコントロールの値を編集する場合、ユーザーは現在のレコードから移動して、更新された値をコントロールがバインドされている基になるデータソースにコミットする必要があります。 [ [データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) からフォームに項目をドラッグすると、ドロップした最初の項目によって、の [ **保存** ] ボタンクリックイベントにコードが生成され <xref:System.Windows.Forms.BindingNavigator> ます。 このコード <xref:System.Windows.Forms.BindingSource.EndEdit%2A> は、のメソッドを呼び出し <xref:System.Windows.Forms.BindingSource> ます。 したがって、メソッドの呼び出し <xref:System.Windows.Forms.BindingSource.EndEdit%2A> は、フォームに追加された最初のに対してのみ生成され <xref:System.Windows.Forms.BindingSource> ます。

 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは、現在編集中のデータ バインド コントロールで実行されている変更をコミットします。 したがって、あるデータ バインド コントロールにフォーカスがある状態で **[保存]** ボタンをクリックすると、実際の保存 (`TableAdapterManager.UpdateAll` メソッド) が実行される前に、そのコントロール内のすべての保留中の編集がコミットされます。

 保存プロセスの一環として、変更をコミットせずにユーザーがデータを保存しようとした場合でも、変更を自動的にコミットするようにアプリケーションを構成できます。

> [!NOTE]
> デザイナーは、 `BindingSource.EndEdit` フォームにドロップされた最初の項目に対してのみコードを追加します。 したがって、 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> フォーム上の各に対してメソッドを呼び出すコード行を追加する必要があり <xref:System.Windows.Forms.BindingSource> ます。 コード行を手動で追加 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> して、それぞれに対してメソッドを呼び出すことができ <xref:System.Windows.Forms.BindingSource> ます。 または、 `EndEditOnAllBindingSources` メソッドをフォームに追加して、保存を実行する前に呼び出すこともできます。

 次のコードでは、 [LINQ (統合言語クエリ)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) クエリを使用し <xref:System.Windows.Forms.BindingSource> てすべてのコンポーネントを反復処理し、 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> フォーム上の各に対してメソッドを呼び出し <xref:System.Windows.Forms.BindingSource> ます。

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>フォーム上のすべての BindingSource コンポーネントに対して EndEdit を呼び出すには

1. コンポーネントを含むフォームに次のコードを追加し <xref:System.Windows.Forms.BindingSource> ます。

     [!code-csharp[VSProDataOrcasEndEditOnAll#1](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs#1)]
     [!code-vb[VSProDataOrcasEndEditOnAll#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb#1)]

2. フォームのデータを保存するための呼び出しの直前に、次のコード行を追加し `TableAdapterManager.UpdateAll()` ます (メソッド)。

     [!code-csharp[VSProDataOrcasEndEditOnAll#2](../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs#2)]
     [!code-vb[VSProDataOrcasEndEditOnAll#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb#2)]

## <a name="see-also"></a>参照
 Visual Studio[階層更新](../data-tools/hierarchical-update.md)[で Windows フォームコントロールをデータにバインドする](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
