---
title: '方法: 特定の Finder メソッドを追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], Specific Finder
- BDC [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], get an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], return an entity
- BDC [SharePoint development in Visual Studio], Specific Finder
- Business Data Connectivity service [SharePoint development in Visual Studio], get an entity
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 403213b6dcd87251df0b24333c759c8de8720afd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86014814"
---
# <a name="how-to-add-a-specific-finder-method"></a>方法: 特定の Finder メソッドを追加する
  *特定の Finder*メソッドを作成することによって、1つのエンティティインスタンスを返すことができます。 Business data Connectivity (BDC) サービスは、ユーザーがビジネスデータ web パーツまたは外部リストでエンティティを選択したときに、特定の Finder メソッドを実行します。 詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-create-a-specific-finder-method"></a>特定の Finder メソッドを作成するには

1. **BDC デザイナー**で、エンティティを選択します。

    Visual Studio で **BDC デザイナー** にエンティティを追加する方法の詳細については、「 [方法: モデルにエンティティを追加](../sharepoint/how-to-add-an-entity-to-a-model.md)する」を参照してください。

2. メニューバーで、[ **View**  >  **他のウィンドウ**を表示]、[ **BDC メソッドの詳細**] の順に選択します。

    [ **BDC メソッドの詳細** ] ウィンドウが開きます。 このウィンドウの詳細については、「 [BDC モデルデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. [ **メソッドの追加** ] の一覧で、[ **特定の Finder メソッドの作成**] を選択します。

    Visual Studio によって、モデルに次の要素が追加されます。 これらの要素は、[ **BDC メソッドの詳細** ] ウィンドウに表示されます。

   - メソッド。

   - メソッドの入力パラメーター。

   - メソッドの戻りパラメーター。

   - 各パラメーターの型記述子。

   - メソッドのメソッドインスタンス。

     詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

4. Visual Studio の [ **プロパティ** ] ウィンドウを開きます。

5. 戻りパラメーターの型記述子をエンティティ型記述子として構成します。 エンティティ型記述子を作成する方法の詳細については、「 [方法: パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)する」を参照してください。

   > [!NOTE]
   > Finder メソッドをエンティティに追加した場合、この手順を実行する必要はありません。 Visual Studio では、Finder メソッドで定義した型記述子が使用されます。

   > [!NOTE]
   > エンティティ型の識別子フィールドが、自動的に生成されたデータベーステーブル内のフィールドを表している場合は、[識別子] フィールドの **読み取り** 専用プロパティを **True**に設定します。

6. [ **メソッドの詳細** ] ウィンドウで、メソッドのメソッドインスタンスを選択します。

7. [ **プロパティ] ウィンドウ**で、[ **パラメーター名の戻り** ] プロパティをメソッドの戻りパラメーターの名前に設定します。 メソッドインスタンスのプロパティの詳細については、「 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))」を参照してください。

8. **ソリューションエクスプローラー**で、エンティティに対して生成されたサービスコードファイルのショートカットメニューを開き、[**コードの表示**] を選択します。

    コードエディターで entity service コードファイルが開きます。 Entity service コードファイルの詳細については、「 [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

9. 特定の Finder メソッドにコードを追加します。 このコードは、以下のタスクを実行します。

   - データソースからレコードを取得します。

   - BDC サービスにエンティティを返します。

     次の例では、SQL Server の AdventureWorks サンプルデータベースから連絡先を返します。

     > [!NOTE]
     > フィールドの値を `ServerName` サーバーの名前に置き換えます。

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="see-also"></a>関連項目
- [ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
