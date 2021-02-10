---
title: エンティティ間の関連付けの作成 |Microsoft Docs
description: Business Data Connectivity (BDC) モデル内のエンティティ間の関連付けを作成します。 アソシエーションのメソッドと型の関連付けについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Association_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7efd3d622e40c21574c0aa9e39263d53979706ec
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949195"
---
# <a name="create-an-association-between-entities"></a>エンティティ間の関連付けを作成する
  関連付けを作成することによって、Business Data Connectivity (BDC) モデルのエンティティ間のリレーションシップを定義できます。 Visual Studio では、モデルのコンシューマーに各アソシエーションに関する情報を提供するメソッドが生成されます。 これらのメソッドは、SharePoint web パーツ、リスト、またはカスタムアプリケーションで、ユーザーインターフェイス (UI) にデータリレーションシップを表示するために使用できます。

## <a name="create-an-association"></a>関連付けを作成する
 関連付けを作成するには、Visual Studio の [**ツールボックス**] で [**関連付け**] コントロールを選択し、最初のエンティティ (ソースエンティティと呼ばれます) を選択して、2番目のエンティティ (送信先エンティティと呼ばれます) を選択します。 アソシエーション **エディター** でアソシエーションの詳細を定義できます。 詳細については、「 [方法: エンティティ間の関連付けを作成する](../sharepoint/how-to-create-an-association-between-entities.md)」を参照してください。

## <a name="association-methods"></a>アソシエーションメソッド
 SharePoint ビジネスデータ web パーツなどのアプリケーションは、エンティティのサービスクラスのメソッドを呼び出すことによって、アソシエーションを使用します。 エンティティのサービスクラスにメソッドを追加するには、 **アソシエーションエディター** で選択します。

 既定では、 **関連付けエディター** は、ソースエンティティとターゲットエンティティにアソシエーションナビゲーションメソッドを追加します。 ソースエンティティのアソシエーションナビゲーションメソッドを使用すると、コンシューマーはターゲットエンティティの一覧を取得できます。 ターゲットエンティティのアソシエーションナビゲーションメソッドを使用すると、コンシューマーは、送信先エンティティに関連付けられているソースエンティティを取得できます。

 これらの各メソッドにコードを追加して、適切な情報を返す必要があります。 さらに高度なシナリオをサポートするために、他の種類のメソッドを追加することもできます。 これらの各方法の詳細については、「 [サポートされる操作](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14))」を参照してください。

## <a name="types-of-associations"></a>関連付けの種類
 BDC デザイナーでは、外部キーベースの関連付けと外部キーなしの関連付けの2種類の関連付けを作成できます。

### <a name="foreign-key-based-association"></a>外部キーベースの関連付け
 ソースエンティティの識別子を、送信先エンティティで定義されている型記述子に関連付けることによって、外部キーベースの関連付けを作成できます。 このリレーションシップを使用すると、モデルのコンシューマーはユーザーに対して高度な UI を提供できます。 たとえば、ユーザーがドロップダウンリストに顧客を表示できる販売注文を作成できるようにする、Outlook のフォームなどです。または、ユーザーが顧客のプロファイルページを開くことができるようにする、SharePoint の販売注文の一覧。

 外部キーベースの関連付けを作成するには、同じ名前と型を共有する識別子と型記述子を関連付けます。 たとえば、エンティティとエンティティの間に外部キーベースの関連付けを作成することができ `Contact` `SalesOrder` ます。 エンティティは、 `SalesOrder` `ContactID` finder または特定の finder メソッドの戻りパラメーターの一部として型記述子を返します。 両方の型記述子が **関連付けエディター** に表示されます。 エンティティとエンティティの間に外部キーベースのリレーションシップを作成するには `Contact` `SalesOrder` 、 `ContactID` これらの各フィールドの横にある識別子を選択します。

 変換先エンティティのコレクションを返すソースエンティティの Association Navigator メソッドにコードを追加します。 次の例では、連絡先の販売注文を返します。

 [!code-csharp[SP_BDC#7](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#7)]
 [!code-vb[SP_BDC#7](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#7)]

 ソースエンティティを返す宛先エンティティの Association Navigator メソッドにコードを追加します。 次の例では、販売注文に関連付けられている連絡先を返します。

 [!code-csharp[SP_BDC#8](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs#8)]
 [!code-vb[SP_BDC#8](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb#8)]

### <a name="foreign-keyless-association"></a>外部キーなしの関連付け
 識別子をフィールド型記述子にマップせずにアソシエーションを作成できます。 ソースエンティティに宛先エンティティとの直接的な関係がない場合は、この種類の関連付けを作成します。 たとえば、テーブルには、 `SalesOrderDetail` テーブル内の主キーにマップされる外部キーがありません `Contact` 。

 に関連する情報をテーブルに表示する場合は、 `SalesOrderDetail` `Contact` エンティティとエンティティの間に外部キーなし関連付けを作成でき `Contact` `SalesOrderDetail` ます。

 エンティティのアソシエーションナビゲーションメソッドで `Contact` 、 `SalesOrderDetail` テーブルを結合するか、ストアドプロシージャを呼び出すことによって、エンティティを返します。

 次の例では、テーブルを結合して、すべての販売注文の詳細を返します。

 [!code-csharp[SP_BDC#9](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#9)]
 [!code-vb[SP_BDC#9](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#9)]

 エンティティのアソシエーションナビゲーションメソッドで、 `SalesOrderDetail` 関連するを返し `Contact` ます。 次に例を示します。

 [!code-csharp[SP_BDC#10](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs#10)]
 [!code-vb[SP_BDC#10](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb#10)]

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: エンティティ間の関連付けを作成する](../sharepoint/how-to-create-an-association-between-entities.md)
