---
title: '方法: パラメーターの型記述子を定義する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], type descriptor
- BDC [SharePoint development in Visual Studio], parameter types
- BDC [SharePoint development in Visual Studio], type descriptor
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0b3ae803576c98a86a45d175af45aa28b3852134
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016847"
---
# <a name="how-to-define-the-type-descriptor-of-a-parameter"></a>方法: パラメーターの型記述子を定義する
  型記述子には、パラメーターのデータ型を表すプロパティが含まれています。 型記述子では、フィールド、エンティティ、またはエンティティのコレクションを定義できます。 詳細については、「 [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\))」を参照してください。

### <a name="to-define-the-type-descriptor-of-a-parameter"></a>パラメーターの型記述子を定義するには

1. [ **BDC メソッドの詳細**] ウィンドウで、パラメーターの型記述子を選択します。

2. メニューバーで、[**表示**]、[**プロパティウィンドウ**] の順に選択します。

3. [**プロパティ**] ウィンドウで、型記述子のプロパティを設定します。

     以降の手順では、型記述子をフィールド、エンティティ、またはエンティティのコレクションとして定義する方法を説明します。

### <a name="to-define-a-field"></a>フィールドを定義するには

1. [**プロパティ**] ウィンドウで、型記述子の**name**プロパティを、エンティティを表す型のフィールドの名前 (例: **FirstName**) に設定します。

2. [ **TypeName** ] プロパティの横にある一覧で、適切なデータ型 (たとえば、 **Int32**) を選択します。

     その他のオプションパラメーターの詳細については、「 [TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\))」を参照してください。

### <a name="to-define-an-entity"></a>エンティティを定義するには

1. [**プロパティ**] ウィンドウで、[**名前**] プロパティを、エンティティを表す名前に設定します ( **Contact**など)。

2. " **TypeName** " プロパティを、エンティティを表す型の完全修飾名に設定します。 この型は、プロジェクト内のクラスにすることも、ソリューションで参照されているアセンブリで定義されている型にすることも、BDC オブジェクト モデルで定義されている型にすることもできます。

    - プロジェクトのクラスの場合は、[ **TypeName** ] プロパティの横にある下向き矢印をクリックし、表示されるダイアログボックスで [**現在のプロジェクト**] タブを選択して、プロジェクトでクラスを選択します。

         完全修飾名には、クラスの名前空間および名前と、LOB システムの名前が含まれます。 次の例では、 **TypeName**プロパティの値をプロジェクトのクラスに設定します。

         `MyBDCNamespace.BdcModel1.Contact, BdcModel1`

    - ソリューション内のアセンブリに配置されている型にする場合は、完全修飾名に型の名前、アセンブリの名前、バージョン番号、カルチャ、および公開キー トークンが含まれます。

         次の例では、 **TypeName**プロパティの値を、ソリューション内で参照するアセンブリで定義されている型に設定しています。

         `MyNamespace.Contact, myAssemblyName, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`

    - BDC オブジェクト モデルで定義されている型にする場合は、完全修飾名に型の名前空間と名前が含まれます。

         次の例では、 **TypeName**プロパティの値を、BDC オブジェクトモデルの型に設定しています。

         `Microsoft.BusinessData.Runtime.DynamicType`

3. [ **BDC メソッドの詳細**] ウィンドウで、型記述子に対して表示される一覧を開き、[**編集**] を選択します。

     [ **BDC エクスプローラー** ] ウィンドウが開きます。

4. **BDC エクスプローラー**で、型記述子のショートカットメニューを開き、[**型記述子の追加**] を選択します。

     そのエンティティ型記述子の子として新しい型記述子が追加されます。 その型記述子をフィールドとして構成します。

5. 手順 4. を繰り返して、エンティティの各フィールドに対応する子の型記述子を追加します。

### <a name="to-define-a-collection-of-entities"></a>エンティティのコレクションを定義するには

1. [ **BDC メソッドの詳細**] ウィンドウで、目的のパラメーターの型記述子を選択します。

2. メニューバーで、[**表示**]、[**プロパティウィンドウ**] の順に選択します。

3. [**プロパティ**] ウィンドウで、[**名前**] プロパティを、エンティティを表す名前に設定します (例: **Contacts**)。

4. **IsCollection**プロパティを**True**に設定します。 これは、この型記述子がエンティティのコレクションであることを表します。

5. [ **TypeName** ] プロパティを、インターフェイスへの参照 <xref:System.Collections.Generic.IEnumerable%601> と、エンティティを表す型の完全修飾名を含む文字列に設定します。 この型は、プロジェクト内のクラスにすることも、ソリューションで参照されているアセンブリで定義されている型にすることも、BDC オブジェクト モデルで定義されている型にすることもできます。

   - プロジェクトのクラスの場合は、[ **TypeName** ] プロパティの横にある下向き矢印をクリックし、表示されるダイアログボックスで [**現在のプロジェクト**] タブを選択して、プロジェクトでクラスを選択します。

      完全修飾名には、クラスの名前空間および名前と、LOB システムの名前が含まれます。

      次の例では、 **TypeName**プロパティの値を、プロジェクト内のクラスのコレクションに設定します。

      `System.Collections.Generic.IEnumerable`1 [MyBDCNamespace、BdcModel1] '

   - ソリューション内のアセンブリに配置されている型にする場合は、完全修飾名に型の名前、アセンブリの名前、バージョン番号、カルチャ、および公開キー トークンが含まれます。

      次の例では、 **TypeName**プロパティの値を、ソリューション内で参照するアセンブリ内の型のコレクションに設定します。

      `System.Collections.Generic.IEnumerable`1 [MyNamespace、myAssemblyName、Version = 4.0.0.0、Culture = ニュートラル、PublicKeyToken = b77a5c561934e089] '

   - BDC オブジェクト モデルで定義されている型にする場合は、完全修飾名に型の名前空間と名前のみが含まれます。

      次の例では、 **TypeName**プロパティの値を、BDC オブジェクトモデルで定義されている型のコレクションに設定します。

      `System.Collections.Generic.IEnumerable`1 [BusinessData. DynamicType] '

6. [ **BDC メソッドの詳細**] ウィンドウで、型記述子に対して表示される一覧を開き、[**編集**] を選択します。

    [ **BDC エクスプローラー** ] ウィンドウが開きます。

7. **BDC エクスプローラー**で、型記述子のショートカットメニューを開き、[**型記述子の追加**] を選択します。

    そのコレクション型記述子の子として新しい型記述子が追加されます。 その型記述子をエンティティとして構成します。

## <a name="see-also"></a>関連項目
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
- [ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
