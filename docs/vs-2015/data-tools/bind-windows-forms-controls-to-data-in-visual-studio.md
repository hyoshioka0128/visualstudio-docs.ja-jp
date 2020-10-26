---
title: Windows フォーム コントロールをデータにバインドする
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
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
caps.latest.revision: 40
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8a03f4df57b216fa68e5ac24df80b67917aa3e3f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672986"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>Visual Studio でのデータへの Windows フォーム コントロールのバインド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データを Windows フォームにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインドコントロールを作成するには、[ **データソース** ] ウィンドウから Visual Studio の Windows フォームデザイナーに項目をドラッグします。 このトピックでは、データ バインド Windows フォーム アプリケーションの作成に使用できる最も一般的なタスク、ツール、およびクラスについて説明します。

 ![データソースのドラッグ操作](../data-tools/media/raddata-data-source-drag-operation.png "レーダーデータデータソースのドラッグ操作")

 Visual Studio でデータバインドコントロールを作成する方法に関する一般的な情報については、「 [Visual studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。 Windows フォームでのデータバインディングの詳細については、「 [データバインディングの Windows フォーム](https://msdn.microsoft.com/library/c3826d8e-ea25-4ad4-a669-45bfb19192aa)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

- [Windows フォーム コントロールをデータにバインドする](../data-tools/bind-windows-forms-controls-to-data.md)

- [データの保存前にデータ バインド コントロールで実行中の編集をコミットする](../data-tools/commit-in-process-edits-on-data-bound-controls-before-saving-data.md)

- [Windows フォーム アプリケーションでルックアップ テーブルを作成する](../data-tools/create-lookup-tables-in-windows-forms-applications.md)

- [データを検索する Windows フォームを作成する](../data-tools/create-a-windows-form-to-search-data.md)

- [単純なデータ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)

- [複合データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)

- [ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)

- [フォーム間でデータを渡す](../data-tools/pass-data-between-forms.md)

## <a name="bindingsource-component"></a>BindingSource コンポーネント
 <xref:System.Windows.Forms.BindingSource> コンポーネントは 2 つの目的で利用できます。 まず、フォームのコントロールをデータにバインドするときに、抽象化レイヤーの役割を果たします。 フォーム上のコントロールは、<xref:System.Windows.Forms.BindingSource> コンポーネントにバインドされます (データ ソースに直接バインドされるわけではありません)。

 また、オブジェクトのコレクションを管理できます。 <xref:System.Windows.Forms.BindingSource> に型を追加すると、その型の一覧が作成されます。

 <xref:System.Windows.Forms.BindingSource> コンポーネントの詳細については、次のトピックを参照してください。

- [BindingSource コンポーネント](https://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9)

- [BindingSource コンポーネントの概要](https://msdn.microsoft.com/library/be838caf-fcb0-4b68-827f-58b2c04b747f)

- [BindingSource コンポーネント アーキテクチャ](https://msdn.microsoft.com/library/7bc69c90-8a11-48b1-9336-3adab5b41591)

## <a name="bindingnavigator-control"></a>BindingNavigator コントロール
 このコンポーネントには、Windows アプリケーションによって表示されるデータを移動するためのユーザー インターフェイスが用意されています。 詳細については、「[BindingNavigator コントロール](https://msdn.microsoft.com/library/18c1e2a5-9834-40d3-9b2e-2b545e4e769e)」を参照してください。

## <a name="datagridview-control"></a>DataGridView コントロール
 さまざまな種類のデータソースの表形式データを表示および編集するには、コントロールを使用し <xref:System.Windows.Forms.DataGridView> ます。 <xref:System.Windows.Forms.DataGridView> にデータをバインドするには、<xref:System.Windows.Forms.DataGridView.DataSource%2A> プロパティを使用します。 詳細については、「 [DataGridView コントロールの概要](https://msdn.microsoft.com/library/0a45c661-89dc-4390-9cc6-c47eee501488)」を参照してください。

## <a name="see-also"></a>参照
 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
