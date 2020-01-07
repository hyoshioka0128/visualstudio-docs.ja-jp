---
title: '方法: 型の間の継承を表示する (クラス デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.AssociationTypeNotFoundError
helpviewer_keywords:
- types [Visual Studio], inheritance
- types [Visual Studio], base
- types [Visual Studio], derived
ms.assetid: ea3f0ada-f53b-4fb1-9fb5-908286f5ec3e
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e1e76d45847d0887b47746c60b836c7acf19d03b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670530"
---
# <a name="how-to-view-inheritance-between-types-class-designer"></a>方法: 型の間の継承を表示する (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

基本型とその派生型の間に継承関係がある場合は、クラス デザイナーのクラス ダイアグラムでそのことがわかります。 2 つの型の間に継承関係が存在しない場合に作成する方法については、「[方法: 型の間の継承を作成する (クラス デザイナー)](../ide/how-to-create-inheritance-between-types-class-designer.md)」をご覧ください。

### <a name="to-find-the-base-type"></a>基本型を特定するには

1. クラス ダイアグラムで、基底クラスまたは基本インターフェイスを表示する型をクリックします。

2. **[クラス ダイアグラム]** メニューで、 **[基底クラスの表示]** または **[基底インターフェイスの表示]** を選択します。

    該当する型の基底クラスまたは基本インターフェイスがダイアグラムに表示され、選択されます。 2 つの図形間に非表示の継承線がある場合、それも表示されます。

   また、基本型を表示する型を右クリックして、 **[基底クラスの表示]** または **[基底インターフェイスの表示]** を選択することもできます。

### <a name="to-find-the-derived-types"></a>派生型を特定するには

1. クラス ダイアグラムで、派生クラスまたは派生インターフェイスを表示する型をクリックします。

2. **[クラス ダイアグラム]** メニューで、 **[派生クラスの表示]** または **[派生インターフェイスの表示]** を選択します。

    該当する型の派生クラスまたは派生インターフェイスがダイアグラムに表示されます。 図形間に非表示の継承線がある場合、それも表示されます。

   また、派生型を表示する型を右クリックして、 **[派生クラスの表示]** または **[派生インターフェイスの表示]** を選択することもできます。

## <a name="see-also"></a>参照
 [方法: 型の間の関連付けを作成する (クラスデザイナー)](../ide/how-to-create-associations-between-types-class-designer.md) [型とリレーションシップを表示する (クラスデザイナー)](../ide/viewing-types-and-relationships-class-designer.md)
