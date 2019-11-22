---
title: Integrate UML models with other models and tools | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, references to models
ms.assetid: 9e75e7d1-93cf-4196-baa3-bd10b9af16d3
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: caecb85392170559a860a7dc334570880d6e76f1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301469"
---
# <a name="integrate-uml-models-with-other-models-and-tools"></a>UML モデルを他のモデルおよびツールと統合する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML モデルは、他のモデルやドメイン固有の言語に統合することができます。

 さまざまな機能を実行する拡張機能のコードを記述して、次の方法でモデルを統合できます。

 任意の要素からの参照を、ファイルなどの他の項目、または他のモデル内の要素にアタッチします。
UML 要素の場合、他の UML 要素、ファイル、またはその他のオブジェクトへのリンクを格納するために、それらの身元を文字列としてエンコードすることができます。

 たとえば、UML アクション (つまり、アクティビティ図の要素) を別のアクティビティ図にリンクできる拡張機能を記述することができます。 ユーザーがアクションをダブルクリックすると、別のアクティビティ図が表示されます。 これでユーザーは、アクションに関する詳細なビューを提供できます。

 文字列やその他のデータを要素に格納するには、次の 2 つの方法があります。

- **Stereotype properties.** UML プロファイルを定義し、その中で定義するステレオタイプを使って、指定する種類の UML 要素にプロパティを追加できます。 For example, you could define a profile that adds a property named **MoreDetail** to a UML action. ステレオタイプをアクションに適用してからリンク データをプロパティに格納することで、データをアクションに格納する拡張機能のコードを記述することができます。

   ステレオタイプとそのプロパティは、[プロパティ] ウィンドウでユーザーが表示することができます。

   この拡張機能を配置するには、プロファイル定義と拡張機能のコードを 1 つの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能にパッケージ化します。

   For more information, see [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md).

   For a sample project in which a profile is deployed together with menu commands and gesture handlers, see [Sample: UML Profiles](https://go.microsoft.com/fwlink/?LinkID=213811).

- **References.** 一連の文字列を任意の UML 要素にアタッチできます。 ファイル名や別の要素の GUID などの情報を格納するコードを記述することもできます。 これは、追加の定義を行わなくても行えます。 参照は、ユーザーには直接表示されません。

   For more information, see [Attach reference strings to UML model elements](../modeling/attach-reference-strings-to-uml-model-elements.md). For a sample, see [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813).

  参照をモデル要素にエンコードするには次の 2 つの方法があります。

- **GUID and Filename** of the target model element and the model that contains it, or a particular diagram that displays it.

   For an example, see [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813).

- **ModelBus References.** ModelBus は、モデル間の参照を作成および解決するためのフレームワークです。 これには、モデル内の要素をユーザーが選択できるようにする ModelBus ピッカーが含まれます。 これは、対象のモデルに変更があったために失われた参照をユーザーが解決するのにも役立ちます。

   For more information, see [Integrating Models by using Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).

  1 つのモデルから別のモデルに変更を反映します。
  たとえば、1 つの要素の名前をリンクされた図の名前と同期させると、一方がユーザーによって変更されると他方も変更されるようになります。 これを行うための次の 2 つのメカニズムがあります。

1. **VMSDK Rules** can be used to propagate changes inside the same model.

    For an example, see [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813).

2. **VMSDK Events** can be used to propagate changes outside the model – for example, to change the filename of a linked document, or to change an element in another model.

   For information about both these mechanisms, see [How to: Respond to Changes in a UML Model](../misc/how-to-respond-to-changes-in-a-uml-model.md).

   Drag elements to copy them from one model to another You can let the user create elements by dragging items onto a UML diagram. 作成した要素は、オリジナルのコピーである必要はありません。 たとえば、ソリューション エクスプローラーからアクティビティ図を別のアクティビティ図にドラッグして新しいアクションを作成する機能をユーザーに提供することができます。

   For more information see [Define a gesture handler on a modeling diagram](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md) and [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md).

## <a name="samples"></a>サンプル
 Please see the code sample [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813). このサンプルを使用すると、ユーザーは任意の UML 要素にファイルをドラッグし、後でその要素をダブルクリックしてファイルを開くことができます。 たとえば、アクティビティ図を、ユースケース要素にリンクすることができます。 リンクが設定されている要素はアイコンで示されます。

 このコード サンプルでは、以下の技法を説明します。

- [UML モデル要素に参照文字列をアタッチする](../modeling/attach-reference-strings-to-uml-model-elements.md)

   このサンプル コードは、要素に関連付けられている参照文字列にファイル パスと要素 GUID を格納します。

- UML 要素にデコレータを追加する方法。 For general information about decorators, see [Customizing Text and Image Fields](../modeling/customizing-text-and-image-fields.md).

   サンプルは、UML 図形にイメージのデコレータを追加します。

- [方法: UML モデル内で変更に応答する](../misc/how-to-respond-to-changes-in-a-uml-model.md)

   このサンプルでは、図に表示される新しい図形に応答するルールを定義する方法を示します。

- [モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)

- [モデリング図にジェスチャ ハンドラーを定義する](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)

   このサンプルでは、Windows エクスプローラー (またはエクスプローラー)、ソリューション エクスプローラー、およびその他の UML 要素からドラッグした項目を処理する方法について説明しています。

  For an example in which a UML model is be read by a DSL, see [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md).

## <a name="see-also"></a>参照
 [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md) [Define a gesture handler on a modeling diagram](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md) [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md) [How to: Respond to Changes in a UML Model](../misc/how-to-respond-to-changes-in-a-uml-model.md) [Sample: UML Profiles](https://go.microsoft.com/fwlink/?LinkID=213811) [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813)
