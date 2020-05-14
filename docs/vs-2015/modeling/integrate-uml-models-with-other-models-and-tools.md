---
title: UML モデルを他のモデルおよびツールと統合する |Microsoft Docs
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
ms.openlocfilehash: 72ea0c562bb9c2a8050fc1365fac19df20232f80
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918353"
---
# <a name="integrate-uml-models-with-other-models-and-tools"></a>UML モデルを他のモデルおよびツールと統合する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML モデルは、他のモデルやドメイン固有の言語に統合することができます。

 さまざまな機能を実行する拡張機能のコードを記述して、次の方法でモデルを統合できます。

 任意の要素からの参照を、ファイルなどの他の項目、または他のモデル内の要素にアタッチします。
UML 要素の場合、他の UML 要素、ファイル、またはその他のオブジェクトへのリンクを格納するために、それらの身元を文字列としてエンコードすることができます。

 たとえば、UML アクション (つまり、アクティビティ図の要素) を別のアクティビティ図にリンクできる拡張機能を記述することができます。 ユーザーがアクションをダブルクリックすると、別のアクティビティ図が表示されます。 これでユーザーは、アクションに関する詳細なビューを提供できます。

 文字列やその他のデータを要素に格納するには、次の 2 つの方法があります。

- **ステレオタイプのプロパティ。** UML プロファイルを定義し、その中で定義するステレオタイプを使って、指定する種類の UML 要素にプロパティを追加できます。 たとえば、**詳細**という名前のプロパティを UML アクションに追加するプロファイルを定義できます。 ステレオタイプをアクションに適用してからリンク データをプロパティに格納することで、データをアクションに格納する拡張機能のコードを記述することができます。

   ステレオタイプとそのプロパティは、[プロパティ] ウィンドウでユーザーが表示することができます。

   この拡張機能を配置するには、プロファイル定義と拡張機能のコードを 1 つの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能にパッケージ化します。

   詳細については、「プロファイルを定義して[UML を拡張する](../modeling/define-a-profile-to-extend-uml.md)」を参照してください。

- **形式.** 一連の文字列を任意の UML 要素にアタッチできます。 ファイル名や別の要素の GUID などの情報を格納するコードを記述することもできます。 これは、追加の定義を行わなくても行えます。 参照は、ユーザーには直接表示されません。

参照をモデル要素にエンコードするには次の 2 つの方法があります。

- ターゲットモデル要素の**GUID とファイル名**、およびターゲットモデル要素を含むモデル、またはそれを表示する特定の図。

- **ModelBus 参照。** ModelBus は、モデル間の参照を作成および解決するためのフレームワークです。 これには、モデル内の要素をユーザーが選択できるようにする ModelBus ピッカーが含まれます。 これは、対象のモデルに変更があったために失われた参照をユーザーが解決するのにも役立ちます。

   詳細については、「 [Visual Studio Modelbus を使用](../modeling/integrating-models-by-using-visual-studio-modelbus.md)したモデルの統合」を参照してください。

  1 つのモデルから別のモデルに変更を反映します。
  たとえば、1 つの要素の名前をリンクされた図の名前と同期させると、一方がユーザーによって変更されると他方も変更されるようになります。 これを行うための次の 2 つのメカニズムがあります。

1. **Vmsdk ルール**を使用して、同じモデル内の変更を反映することができます。

2. **Vmsdk イベント**を使用して、モデルの外部の変更を反映することができます。たとえば、リンクドキュメントのファイル名を変更したり、別のモデルの要素を変更したりできます。

   これらのメカニズムの詳細については、「[方法: UML モデルの変更に対応する](../misc/how-to-respond-to-changes-in-a-uml-model.md)」を参照してください。

   要素をドラッグして1つのモデルから別のモデルにコピーするには、ユーザーが UML 図に項目をドラッグして要素を作成できるようにします。 作成した要素は、オリジナルのコピーである必要はありません。 たとえば、ソリューション エクスプローラーからアクティビティ図を別のアクティビティ図にドラッグして新しいアクションを作成する機能をユーザーに提供することができます。

   詳細については、「[モデリング図でのジェスチャハンドラーの定義](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)」および「[方法: ドラッグアンドドロップハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)」を参照してください。

## <a name="see-also"></a>参照
 [モデリング図にメニューコマンドを定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)する[モデリング図にジェスチャハンドラーを定義](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)する[方法: ドラッグアンドドロップハンドラーを追加](../modeling/how-to-add-a-drag-and-drop-handler.md)する方法[: UML モデルの変更に応答](../misc/how-to-respond-to-changes-in-a-uml-model.md)する
