---
title: '[.NET 型の参照と選択] ダイアログボックス |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- TypeBrowser.UI
- ActivityTypeResolver.UI
ms.assetid: 864b60b6-a070-4e5c-aa5b-a25341b57ea6
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d8e25ad181202a2c7994c116e2220426ca3d8509
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297616"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>[.NET 型の参照と選択] ダイアログ ボックス
**[プロパティ]** ウィンドウ、ダイアログボックス、または変数デザイナーなどのデザイナーで、 **[型の参照]** を選択します。 データ型の一覧からは、 **[.Net 型の参照と選択]** ダイアログボックスが表示されます ("型ブラウザー" として省略形で参照されています)。 このダイアログ ボックスでは、アセンブリとプロジェクトのツリー表示から型を選択できます。

 このダイアログ ボックスは、次のようなさまざなユーザー シナリオで使用されます。

- 変数または引数の型を設定する。

- 一般的なアクティビティの型を選択する。

- <xref:System.Activities.Statements.TryCatch> アクティビティに catch を追加する。

> [!NOTE]
> 型ブラウザーは、多次元配列型ではなく Visual Basic ジャグ配列型を表示できます。 詳細については、「[ジャグ配列](https://go.microsoft.com/fwlink/?LinkId=195226)と[多次元配列](https://go.microsoft.com/fwlink/?LinkId=195227)」を参照してください。

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>型ブラウザーでの値型または参照型の選択

#### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>型ブラウザーで値型または参照型を選択するには

1. **[型名]** ボックスに、使用する型の名前を入力します。

2. 以下のいずれかを実行します。

    - 使用する型の名前が **[型名]** ボックスのツリーに表示されたら、その型をダブルクリックして選択します。

    - **[型名]** ボックスに、使用する型を一意に識別するために十分な文字を入力し、enter キーを押して型を選択します。

#### <a name="to-select-a-generic-type-from-the-type-browser"></a>型ブラウザーでジェネリック型を選択するには

1. **[型名]** ボックスに、使用する型の名前を入力します。

2. 使用する型の名前が **[型名]** ボックスのツリーに表示されたら、その種類をクリックして選択し、ドロップダウンボックスが表示されるようにします。

     ジェネリックを閉じるために使用する種類をドロップダウンボックスから選択し、[ **OK]** をクリックします。

## <a name="types-displayed-in-the-type-browser"></a>型ブラウザーに表示される型
 型ブラウザーに表示される型は、型ブラウザーを起動した方法に応じて変わる場合があります。 **Vs2010**内のワークフロープロジェクトから型ブラウザーを起動した場合、既定では、参照されたアセンブリと参照されるプロジェクトのすべての型が表示されます。 **Vs2010**プロジェクトシステム (再ホストされたワークフローアプリケーションやスタンドアロンワークフローファイルなど) の外部から型ブラウザーを起動した場合、既定では、AppDomain に読み込まれたすべてのアセンブリの型が表示されます。

 アクティビティ デザイナーの開発者は、型ブラウザーの型をフィルター処理できます。 どのアクティビティでも、表示されるのは型のサブセットのみです。 たとえば、<xref:System.Activities.Statements.TryCatch> アクティビティでは、<xref:System.Exception> から派生した型のみが型ブラウザーに表示されます。

## <a name="filtering-search-results-in-the-type-browser"></a>型ブラウザーでの検索結果のフィルター処理
 **[型名]** ボックスの型の一覧は、一致を検索するためにさらに文字を入力すると短くなります。 フィルター処理された一覧には、入力した文字列で完全修飾名が始まる型、または、入力した文字列で始まる短い名前を持つ型のみが表示されます。

 例 :

1. 入力**操作**は <xref:System.OperationCanceledException> と一致しますが、<xref:System.InvalidOperationException>は一致しません。 <xref:System.InvalidOperationException> と一致するためには、「System.I」または「Invalid」と入力します。

2. 型指定**ジェネリック**は <xref:System.GenericUriParser> に一致しますが、<xref:System.Collections.Generic> 名前空間の型には一致しません。 <xref:System.Collections.Generic> 名前空間の型を検索するには、その名前空間の完全修飾名を入力します。

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>型ブラウザー ダイアログを使用したサービス コントラクトの選択
 サービス コントラクト型を選択すると、型ブラウザーは <xref:System.ServiceModel.ServiceContractAttribute> 属性を持つ型だけを表示します。

## <a name="see-also"></a>関連項目
 [アクティビティ デザイナーの使用](../workflow-designer/using-the-activity-designers.md)