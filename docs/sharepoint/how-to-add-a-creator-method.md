---
title: '方法: Creator メソッドを追加する |Microsoft Docs'
description: SharePoint の Business Data Connectivity (BDC) サービスのエンティティのデータソースに新しいデータを追加する Creator メソッドを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], Creator
- BDC [SharePoint development in Visual Studio], adding entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entity instances
- BDC [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Creator
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4079fb5be612421bfa4a0b6dc53c3003a1c65e61
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934885"
---
# <a name="how-to-add-a-creator-method"></a>方法: Creator メソッドを追加する
  Creator メソッドは、エンティティのデータソースに新しいデータを追加します。 ユーザーがモデルに基づくリストの **リボン** で [**新しい項目**] ボタンを選択すると、BUSINESS Data Connectivity (BDC) サービスはこのメソッドを呼び出します。 詳細については、「[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-add-a-creator-method"></a>Creator メソッドを追加するには

1. **BDC デザイナー** で、エンティティを選択します。

2. メニューバーで、[   >  **その他の Windows**  > **BDC メソッドの詳細** を表示] を選択します。

    [ **BDC メソッドの詳細** ] ウィンドウが開きます。 このウィンドウの詳細については、「 [BDC モデルデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. [ **メソッドの追加** ] の一覧で、[ **Create Creator method**] を選択します。

    Visual Studio は、次の要素をモデルに追加します。これらの要素は、[ **BDC メソッドの詳細** ] ウィンドウに表示されます。

   - **Create** という名前のメソッド。

   - メソッドの入力パラメーター。

   - メソッドの戻りパラメーター。

   - パラメーターの型記述子。

   - メソッドのメソッドインスタンス。

     詳細については、「[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

4. **ソリューションエクスプローラー** で、エンティティに対して生成されたサービスコードファイルのショートカットメニューを開き、[**コードの表示**] を選択します。

    コードエディターで entity service コードファイルが開きます。 Entity service コードファイルの詳細については、「 [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

5. データソースにデータを追加するコードを Creator メソッドに追加します。 次の例では、SQL Server の AdventureWorks サンプルデータベースに連絡先を追加します。

   > [!NOTE]
   > フィールドの値を `ServerName` サーバーの名前に置き換えます。

    [!code-csharp[SP_BDC#4](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#4)]
    [!code-vb[SP_BDC#4](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#4)]

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
