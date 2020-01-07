---
title: '方法: クラス ダイアグラムをカスタマイズする (クラス デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- class diagrams, customizing
- shapes, removing type from class diagrams
- type shapes, removing from class diagrams
- class diagrams, removing type shapes
ms.assetid: e9030aea-c77d-4cc1-b8f6-b6ca469b692d
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ff78bea6759359d3703f5fed6157f051c89befb0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668008"
---
# <a name="how-to-customize-class-diagrams-class-designer"></a>方法: クラス ダイアグラムをカスタマイズする (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

クラス ダイアグラムで情報を表示する方法を変更できます。 ダイアグラム全体をカスタマイズすることも、デザイン サーフェイス上の個々の型をカスタマイズすることもできます。

 たとえば、クラス ダイアグラム全体のズーム レベルの調整、個々の型のメンバーのグループ化および並べ替え方法の変更、リレーションシップの表示または非表示、ダイアグラム上での個々の型または型のセットの移動などを実行できます。

> [!NOTE]
> ダイアグラムで図形が表示される方法をカスタマイズしても、ダイアグラムが表す型の基になるコードが変更されるわけではありません。

 クラスのプロパティ セクションのように型のメンバーが含まれるセクションは、コンパートメントと呼ばれます。 個々のコンパートメントや型のメンバーは、表示または非表示にできます。

 **このトピックの内容**

- [クラス ダイアグラムを拡大または縮小する](../ide/how-to-customize-class-diagrams-class-designer.md#ZoomInOut)

- [型のメンバーのグループ化および並べ替えをカスタマイズする](../ide/how-to-customize-class-diagrams-class-designer.md#CustomizeGroupingSorting)

- [型のコンパートメントを非表示にする](../ide/how-to-customize-class-diagrams-class-designer.md#HideCompartments)

- [型の個々のメンバーを非表示にする](../ide/how-to-customize-class-diagrams-class-designer.md#HideMembers)

- [型で非表示になっているコンパートメントおよびメンバーを表示する](../ide/how-to-customize-class-diagrams-class-designer.md#DisplayHiddenCompartmentsAndMemberrs)

- [リレーションシップを非表示にする](../ide/how-to-customize-class-diagrams-class-designer.md#HideAssociationAndInheritance)

- [非表示のリレーションシップを表示する](../ide/how-to-customize-class-diagrams-class-designer.md#DisplayAssociationAndInheritance)

- [クラス ダイアグラムから図形を削除する](../ide/how-to-customize-class-diagrams-class-designer.md#RemoveCodeAndShape)

- [型シェイプとその基になるコードを削除する](../ide/how-to-customize-class-diagrams-class-designer.md#DeleteTypeShapeAndCode)

## <a name="ZoomInOut"></a> クラス ダイアグラムを拡大または縮小する

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. クラス デザイナーのツール バーの **[拡大表示]** または **[縮小表示]** をクリックして、デザイナー画面のズーム レベルを変更します。

     、または

     特定のズームの値を指定します。 **[ズーム]** ドロップダウン リストから指定するか、有効なズーム レベルを入力します。有効な値の範囲は 10 ～ 400% です。

    > [!NOTE]
    > ズーム レベルを変更しても、クラス ダイアグラムの出力のスケールには影響ありません。

## <a name="CustomizeGroupingSorting"></a> 型のメンバーのグループ化および並べ替えをカスタマイズする

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. デザイン サーフェイスの空の領域を右クリックし、 **[グループ メンバー]** をポイントします。

3. 使用可能なオプションのうち 1 つを選択します。

    1. **[種類でグループ化]** をクリックすると、個々の型のメンバーが、プロパティ、メソッド、イベント、およびフィールドの、グループ化された一覧に分けられます。 個々のグループは、エンティティ定義によって変わります。たとえば、イベントが定義されていないクラスの場合、そのクラスではイベント グループが表示されません。

    2. **[アクセスでグループ化]** をクリックすると、個々の型のメンバーが、メンバーのアクセス修飾子に基づいて、グループ化された一覧に分けられます。 たとえば、パブリックとプライベートに分けられます。

    3. **[アルファベット順に並べ替え]** をクリックすると、1 つのエンティティを構成する項目が、単一のアルファベット順の一覧として表示されます。 この一覧は昇順に並べ替えられます。

## <a name="HideCompartments"></a> 型のコンパートメントを非表示にする

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. カスタマイズする型のメンバー カテゴリを右クリックします。たとえば、クラスの **[メソッド]** ノードを選択します。

3. **[コンパートメントの非表示]** をクリックします。

     選択したコンパートメントが型のコンテナーに表示されなくなります。

## <a name="HideMembers"></a> 型の個々のメンバーを非表示にする

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. 非表示にする型のメンバーを右クリックします。

3. **[非表示]** をクリックします。

     選択したメンバーが型のコンテナーに表示されなくなります。

## <a name="DisplayHiddenCompartmentsAndMemberrs"></a> 型で非表示になっているコンパートメントおよびメンバーを表示する

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. 非表示になっているコンパートメントを持つ型の名前を右クリックします。

3. **[すべてのメンバーの表示]** をクリックします。

     非表示になっていたすべてのコンパートメントおよびメンバーが、型のコンテナーに表示されます。

## <a name="HideAssociationAndInheritance"></a> リレーションシップを非表示にする

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. 非表示にする関連行または継承線を右クリックします。

3. 関連行の場合は **[非表示]** 、継承線の場合は **[継承線を隠す]** をクリックします。

4. **[すべてのメンバーの表示]** をクリックします。

     非表示になっていたすべてのコンパートメントおよびメンバーが、型のコンテナーに表示されます。

## <a name="DisplayAssociationAndInheritance"></a> 非表示のリレーションシップを表示する

1. クラス デザイナーでクラス ダイアグラム ファイルを開いて選択します。

2. 非表示になっている関連行または継承線を持つ型を右クリックします。

   関連行の場合は **[すべてのメンバーの表示]** 、継承線の場合は **[基本クラスの表示]** または **[派生クラスの表示]** をクリックします。

## <a name="RemoveCodeAndShape"></a> クラス ダイアグラムから図形を削除する
 型の基になるコードに影響を与えずに型シェイプをクラス ダイアグラムから削除できます。 クラス ダイアグラムからの型シェイプの削除は、そのダイアグラムだけに影響します。型を定義する基礎のコードと、型を表示する他のダイアグラムには影響しません。

1. クラス ダイアグラムで、ダイアグラムから削除する型シェイプを選択します。

2. **[編集]** メニューの **[ダイアグラムから削除]** をクリックします。

     型シェイプと、図形に接続されている関連付けまたは継承の線が、ダイアログに表示されなくなります。

## <a name="DeleteTypeShapeAndCode"></a> 型シェイプとその基になるコードを削除する

1. デザイン サーフェイスで図形を右クリックします。

2. コンテキスト メニューの **[コードの削除]** をクリックします。

     シェイプがダイアグラムから削除され、基礎となるコードはプロジェクトから削除されます。

## <a name="see-also"></a>参照
 [クラスダイアグラムの使用 (クラスデザイナー)](../ide/working-with-class-diagrams-class-designer.md) [方法: メンバー表記と関連付け表記の間で変更する (クラスデザイナー)](../ide/how-to-change-between-member-notation-and-association-notation-class-designer.md) [方法: 既存の型を表示する (クラスデザイナー)](../ide/how-to-view-existing-types-class-designer.md) [型とリレーションシップを表示する (クラスデザイナー)](../ide/viewing-types-and-relationships-class-designer.md)
