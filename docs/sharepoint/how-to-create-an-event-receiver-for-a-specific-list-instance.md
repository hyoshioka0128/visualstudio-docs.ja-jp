---
title: '方法: 特定のリストインスタンスのイベントレシーバーを作成する |Microsoft Docs'
titleSuffix: ''
description: 特定のリストインスタンスのイベントレシーバーを作成します。 リストインスタンスイベントレシーバーは、リスト定義の任意のインスタンスで発生するイベントに応答します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
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
ms.openlocfilehash: 664a7ac4e763b2378cf30603c417aacde27c2e47
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925494"
---
# <a name="how-to-create-an-event-receiver-for-a-specific-list-instance"></a>方法: 特定のリストインスタンスのイベントレシーバーを作成する
  リストインスタンスイベントレシーバーは、リスト定義の任意のインスタンスで発生するイベントに応答します。 イベントレシーバーテンプレートでは、特定のリストインスタンスのターゲット設定が有効になっていませんが、特定のリストインスタンスのイベントに応答するように、リスト定義にスコープ設定されているイベントレシーバーを変更することができます。

 特定のリストインスタンスを対象にするには、イベントレシーバーの *Elements.xml* で、をに置き換え、 `ListTemplateId` `ListUrl` リストインスタンスの URL を追加します。

## <a name="create-a-list-instance-event-receiver"></a>リストインスタンスイベントレシーバーの作成
 次の手順では、カスタムのアナウンスリストインスタンスで発生したイベントにのみ応答するようにリスト項目イベントレシーバーを変更する方法を示します。

#### <a name="to-modify-an-event-receiver-to-respond-to-a-specific-list-instance"></a>特定のリストインスタンスに応答するようにイベントレシーバーを変更するには

1. ブラウザーで SharePoint サイトを開きます。

2. ナビゲーションウィンドウに [リスト] リンクが **表示** されます。

3. [ **すべてのサイトコンテンツ** ] ページで、[ **作成** ] リンクを選択します。

4. [ **作成** ] ダイアログボックスで、[ **お知らせ** の種類] を選択し、アナウンスの **testannouncements** に名前を指定して、[ **作成** ] ボタンを選択します。

5. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、イベントレシーバープロジェクトを作成します。

6. [ **どの種類のイベントレシーバーを使用しますか?** ] ボックスの一覧で、[ **リスト項目イベント**] を選択します。

    > [!NOTE]
    > リスト定義にスコープを持つ他の種類のイベントレシーバーを選択することもできます。たとえば、 **電子メールイベントの一覧表示** や **ワークフローイベントの一覧** 表示を行うことができます。

7. [ **イベントソースの項目** を選択してください] ボックスの一覧で、[ **アナウンス**] を選択します。

8. [ **次のイベントを処理** する] の一覧で、[ **追加中の項目** ] チェックボックスをオンにし、[ **完了** ] をクリックします。

9. **ソリューションエクスプローラー** の [EventReceiver1] で、[ *Elements.xml* を開きます。

     イベントレシーバーは、現在、次の行を使用してお知らせリストの定義を参照しています。

    ```xml
    <Receivers ListTemplateId="104">
    ```

     この行を次のテキストに変更します。

    ```xml
    <Receivers ListUrl="Lists/TestAnnouncements">
    ```

     これにより、イベントレシーバーは、先ほど作成した新しい **testannouncements** アナウンスリストで発生したイベントにのみ応答します。 属性を変更して、 `ListURL` SharePoint サーバー上の任意のリストインスタンスを参照することができます。

10. イベントレシーバーのコードファイルを開き、ItemAdding メソッドにブレークポイントを設定します。

11. F5 キーを **押し** て、ソリューションをビルドして実行します。

12. SharePoint で、ナビゲーションウィンドウの [ **Testannouncements** ] リンクを選択します。

13. [ **新しいアナウンスの追加** ] リンクを選択します。

14. お知らせのタイトルを入力し、[ **保存** ] をクリックします。

     新しい項目がカスタムのアナウンスリストに追加されると、ブレークポイントにヒットします。

15. F5 キーを **押し** て再開します。

16. ナビゲーションウィンドウで、[ **リスト** ] リンクを選択し、[ **お知らせ** ] リンクを選択します。

17. 新しいお知らせを追加します。

     レシーバーはカスタムアナウンスリストインスタンス **Testannouncements** のイベントにのみ応答するように構成されているため、新しいアナウンスでイベントレシーバーがトリガーされないことに注意してください。

## <a name="see-also"></a>関連項目
- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
