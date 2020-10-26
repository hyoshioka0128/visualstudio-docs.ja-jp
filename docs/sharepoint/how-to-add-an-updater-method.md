---
title: '方法: Updater メソッドを追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], updating data
- BDC [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating data
- Business Data Connectivity service [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating entity instances
- BDC [SharePoint development in Visual Studio], updating entity instances
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c76373c710908a8ae7edc49c4e26ff7e94336a6d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86014985"
---
# <a name="how-to-add-an-updater-method"></a>方法: Updater メソッドを追加する
  ユーザーが *Updater* メソッドを作成することによって、SharePoint 外部リストのビジネスデータを更新できるようにすることができます。 詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-create-an-updater-method"></a>Updater メソッドを作成するには

1. BDC デザイナーで、エンティティを選択します。

2. メニューバーで、[ **View**  >  **その他の Windows**  >  **BDC メソッドの詳細**を表示] を選択します。

    [BDC メソッドの詳細] ウィンドウが開きます。 このウィンドウの詳細については、「 [BDC モデルデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. [ **メソッドの追加** ] の一覧で、[ **アップデーター方法の作成**] を選択します。

    Visual Studio によって、モデルに次の要素が追加されます。 これらの要素は、[BDC メソッドの詳細] ウィンドウに表示されます。

   - **Update**という名前のメソッド。

   - メソッドの入力パラメーター。

   - パラメーターの型記述子。 既定では、Visual Studio は Finder メソッドに対して定義したエンティティ型記述子 (Contact など) を使用します。

   - メソッドのメソッドインスタンス。

     詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

   > [!NOTE]
   > エンティティ型の識別子が、自動的に生成されないデータベーステーブル内のフィールドを表している場合は、[ **更新前のフィールド]** プロパティを [ **True**] に設定します。

4. **ソリューションエクスプローラー**で、エンティティに対して生成されたサービスコードファイルのショートカットメニューを開き、[**コードの表示**] を選択します。

    **コードエディター**で entity service コードファイルが開きます。 そのファイルの詳細については、「 [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

5. Update メソッドにデータを更新するコードを追加します。 次の例では、AdventureWorks サンプルデータベースの連絡先に関する情報を SQL Server に更新します。

   > [!NOTE]
   > フィールドの値を `ServerName` サーバーの名前に置き換えます。

    [!code-csharp[SP_BDC#5](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#5)]
    [!code-vb[SP_BDC#5](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#5)]

## <a name="see-also"></a>関連項目
- [ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
