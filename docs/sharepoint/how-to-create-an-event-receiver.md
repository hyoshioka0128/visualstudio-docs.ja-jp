---
title: '方法: イベントレシーバーを作成する |Microsoft Docs'
description: ユーザーがリストやリストアイテムなどの SharePoint アイテムを操作するときに応答できるように、イベントレシーバーを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.EventReceiver
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, event receivers
- event receivers [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d0eebee6e37fbd6696923da0e470f05688fa0387
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216580"
---
# <a name="how-to-create-an-event-receiver"></a>方法: イベント レシーバーを作成する
  *イベントレシーバー* を作成することにより、ユーザーがリストやリストアイテムなどの SharePoint アイテムを操作するときに応答できます。 たとえば、ユーザーがカレンダーを変更したり、連絡先リストから名前を削除したりすると、イベントレシーバーのコードがトリガーされます。 このトピックでは、イベントレシーバーをリストインスタンスに追加する方法について説明します。

 これらの手順を完了するには、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Windows および SharePoint のエディションがインストールされ、サポートされている必要があります。 この例では SharePoint プロジェクトが必要であるため、「 [チュートリアル: サイト列、コンテンツタイプ、および sharepoint の一覧の作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)」の手順を完了している必要もあります。

## <a name="adding-an-event-receiver"></a>イベントレシーバーの追加
 「 [チュートリアル: サイト列、コンテンツタイプ、および SharePoint の一覧の作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) 」で作成したプロジェクトには、カスタムサイト列、カスタムリスト、およびコンテンツタイプが含まれています。 次の手順では、単純なイベントハンドラー (イベントレシーバー) をリストインスタンスに追加して、このプロジェクトを拡張します。これにより、リストなどの SharePoint アイテムで発生するイベントの処理方法が示されます。

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>イベントレシーバーをリストインスタンスに追加するには

1. 「 [チュートリアル: SharePoint のサイト列、コンテンツタイプ、およびリストを作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)する」で作成したプロジェクトを開きます。

2. **ソリューションエクスプローラー** で、[**クリニック**] という名前の SharePoint プロジェクトノードを選択します。

3. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

4. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開し、[ **2010** ] 項目を選択します。

5. [ **テンプレート** ] ウィンドウで [ **イベントレシーバー**] を選択し、「 **TestEventReceiver1**」という名前を指定して、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード** が表示されます。

6. [ **どの種類のイベントレシーバーを使用しますか?** ] ボックスの一覧で、[ **リスト項目イベント**] を選択します。

7. [ **イベントソースを指定してください]** の一覧で、[ **患者 (Clinic\Patients)**] を選択します。

8. [ **次のイベントを処理** する] ボックスの一覧で、 **項目** の横にあるチェックボックスをオンにし、[ **完了** ] をクリックします。

     新しいイベントレシーバーのコードファイルには、という名前の1つのメソッドが含まれてい `ItemAdded` ます。 次の手順では、このメソッドにコードを追加して、すべての連絡先が既定で Scott Brown という名前になるようにします。

9. 既存の `ItemAdded` メソッドを次のコードに置き換え、 **F5** キーを押します。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb" id="Snippet1":::

     コードが実行され、SharePoint サイトが web ブラウザーに表示されます。

10. クイック起動バーで、[ **患者** ] リンクを選択し、[ **新しいアイテムの追加** ] リンクを選択します。

     新しい項目の入力フォームが開きます。

11. フィールドにデータを入力し、[ **保存** ] をクリックします。

     [ **保存** ] ボタンを選択すると、[ **患者の名前** ] 列が Scott Brown という名前に自動的に更新されます。

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)