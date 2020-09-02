---
title: '方法: Finder メソッドを追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1fa8f8eb34943cc17bc6cabca8e93ea7569a7ba6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016722"
---
# <a name="how-to-add-a-finder-method"></a>方法: Finder メソッドを追加する
  Business Data Connectivity (BDC) サービスで、web パーツまたはリスト内のエンティティの一覧を表示できるようにするには、 *Finder* メソッドを作成する必要があります。 Finder メソッドは、エンティティインスタンスのコレクションを返す特殊なメソッドです。 詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-create-a-finder-method"></a>Finder メソッドを作成するには

1. **BDC デザイナー**で、エンティティを選択します。

    詳細については、「 [方法: モデルにエンティティを追加](../sharepoint/how-to-add-an-entity-to-a-model.md)する」を参照してください。

2. メニューバーで、[ **View**  >  **その他の Windows**  >  **BDC メソッドの詳細**を表示] を選択します。

    [ **BDC メソッドの詳細** ] ウィンドウが開きます。 [ **Bdc メソッドの詳細** ] ウィンドウの詳細については、「 [bdc モデルデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. [ **メソッドの追加** ] の一覧で、[ **Finder メソッドの作成**] を選択します。

    Visual Studio によって、メソッド、戻りパラメーター、および型記述子が追加されます。

4. 型記述子をエンティティコレクション型記述子として構成します。 エンティティコレクション型記述子を作成する方法の詳細については、「 [方法: パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)する」を参照してください。

   > [!NOTE]
   > 特定の Finder メソッドをエンティティに追加した場合、この手順を実行する必要はありません。 Visual Studio では、特定の Finder メソッドで定義した型記述子が使用されます。

5. **ソリューションエクスプローラー**で、エンティティに対して生成されたサービスコードファイルのショートカットメニューを開き、[**コードの表示**] を選択します。 サービスコードファイルの詳細については、「 [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

6. Finder メソッドにコードを追加します。 このコードは、以下のタスクを実行します。

   - データソースからデータを取得します。

   - BDC サービスへのエンティティの一覧を返します。

     次の例では、 `Contact` SQL Server の AdventureWorks サンプルデータベースのデータを使用して、エンティティのコレクションを返します。

   > [!NOTE]
   > フィールドの値を `ServerName` サーバーの名前に置き換えます。

    [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
    [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="see-also"></a>関連項目
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
