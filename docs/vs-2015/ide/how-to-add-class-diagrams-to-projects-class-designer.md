---
title: '方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- class diagrams, creating
- Class Designer [Visual Studio], opening
ms.assetid: 0eac1b54-2711-4e4b-9654-a0c429c08c8f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f1a0d10dabdace7ef7ab3805a59b892548cf6556
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645516"
---
# <a name="how-to-add-class-diagrams-to-projects-class-designer"></a>方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

クラスおよび他の型の設計、編集およびリファクタリングを行うには、クラス ダイアグラムを Visual C# .NET、Visual Basic .NET、または C++ プロジェクトに追加します。 プロジェクト内のコードの異なる部分を視覚化するには、複数のクラス ダイアグラムをプロジェクトに追加します。

 複数のアプリでコードを共有しているプロジェクトからは、クラス ダイアグラムを作成できません。 UML クラス ダイアグラムを作成するには、「[UML モデリング プロジェクトおよびダイアグラムを作成する](../modeling/create-uml-modeling-projects-and-diagrams.md)」を参照してください。

### <a name="to-add-a-blank-class-diagram-to-a-project"></a>プロジェクトに空のクラス ダイアグラムを追加するには

1. ソリューション エクスプローラーで、プロジェクト名を右クリックします。 次に、 **[新しい項目の追加]** または **[追加]** 、 **[新しい項目]** をクリックします。

2. テンプレートの一覧から、 **[クラス ダイアグラム]** を選択します。 Visual C++ のプロジェクトの場合、このテンプレートを見つけるには、 **[テンプレート]** の下にある **[ユーティリティ]** を探します。

     クラス デザイナーでクラス ダイアグラムが開き、ソリューション エクスプローラーのプロジェクト階層に .cd 拡張子付きのファイルとして表示されます。 図形や線をダイアグラムにドラッグするには、クラス デザイナーのツールボックスを使用します。

3. 複数のクラス ダイアグラムを追加するには、この手順を繰り返します。

### <a name="to-add-a-class-diagram-based-on-existing-types"></a>既存の型に基づいてクラス ダイアグラムを追加するには

1. ソリューション エクスプローラーで、クラス ファイル コンテキスト メニューを開き、 **[クラス ダイアグラムの表示]** をクリックします。

     -または-

     **[クラス ビュー]** で、名前空間または型のコンテキスト メニューを開き、 **[クラス ダイアグラムで表示]** を選択します。

### <a name="to-display-the-contents-of-a-complete-project-in-a-class-diagram"></a>クラス ダイアグラムに完全なプロジェクトの内容を表示するには

1. ソリューション エクスプローラーまたはクラス ビューで、プロジェクトを右クリックし、 **[表示]** を選択してから **[クラス ダイアグラムの表示]** を選択します。

     自動設定されたクラス ダイアグラムが作成されます。

## <a name="see-also"></a>参照
 [方法: クラスデザイナーを使用して型を作成](../ide/how-to-create-types-by-using-class-designer.md)する[方法: 既存の型を表示する (クラスデザイナー)](../ide/how-to-view-existing-types-class-designer.md) [クラスと型のデザイン (クラスデザイナー) クラスと型のデザイン](../ide/designing-classes-and-types-class-designer.md)(クラスデザイナー) クラスダイアグラムの操作 ( [)](../ide/viewing-types-and-relationships-class-designer.md) [クラスデザイナー)](../ide/working-with-class-diagrams-class-designer.md)
