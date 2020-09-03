---
title: UML API を使用したプログラミング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, API
- UML model, extending
ms.assetid: c5937139-49d0-4439-8a9f-89f5e0474618
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bdf1111198c7f874d03596382372fe25851e37d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75852128"
---
# <a name="programming-with-the-uml-api"></a>UML API を使用したプログラミング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の UML API を使用すると、UML モデルおよび図の生成、読み取り、および更新を実行するためのコードを作成できます。 UML モデルをサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 API については、API リファレンス ページのほか、次のトピックで説明されています。

|トピック|説明されている型およびメソッドの例|説明されている機能|
|-----------|-----------------------------------------|------------------------|
|[UML API を使用して関係をナビゲートする](../modeling/navigate-relationships-with-the-uml-api.md)|UML 要素とそのプロパティおよび関連。 たとえば、IElement とその子孫である IClass、IActivity、IUseCase、IComponent、IInteraction、IModel、IPackage。|Visual Studio では、uml モデルは uml 仕様バージョン2.1.2 に準拠しています。これは、 [Uml リソースページ](https://www.uml.org/)で取得できます。 それぞれの型は、プレフィックスとして "I" が付けられた、UML 型と同じ名前のインターフェイスです。|
|[UML モデル内に要素および関係を生成する](../modeling/create-elements-and-relationships-in-uml-models.md)|IPackage.CreateClass()<br /><br /> IClass.CreateOperation()|それぞれの要素型は、子を生成するためのメソッドを持ちます。|
|[図に UML モデルを表示する](../modeling/display-a-uml-model-on-diagrams.md)|IShape、IDiagram<br /><br /> IShape.Move()|モデルのそれぞれの要素は、図においてシェイプとして表すことができます。 場合によっては、それぞれのオブジェクトに対して新しいシェイプを生成できます。 これらのシェイプについては、移動、サイズ変更、色の設定、および折りたたみ/展開を行うことができます。|
|[UML モデル内を移動する](../modeling/navigate-the-uml-model.md)|IModelStore<br /><br /> IDiagramContext|モデル ストアは、モデルを格納します。<br /><br /> 図コンテキストは、現在の図およびストアへのアクセスを提供します。|
|[トランザクションを使用して UML モデルの更新をリンクする](../modeling/link-uml-model-updates-by-using-transactions.md)|ILinkedUndoContext|一連の変更を 1 つのトランザクションにリンクできます。|
|[モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)|IMenuCommand<br /><br /> IGestureExtension<br /><br /> ICommandExtension|ダブルクリックと図へのドラッグによって起動されるコマンドを定義することで、図の機能を拡張できます。|
|[UML モデルの検証制約を定義する](../modeling/define-validation-constraints-for-uml-models.md)|ValidationContext|モデルが指定された制約に準拠していることを保証するための検証規則を定義できます。|
|[IDataObject から UML モデル要素を取得する](../modeling/get-uml-model-elements-from-idataobject.md)|IElement、IShape|要素を UML モデル エクスプローラーまたは UML 図から別の図またはアプリケーションにドラッグすると、要素は IDataObject としてシリアル化されます。|
|[UML API を使用して UML シーケンス図を編集する](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)|IInteraction、ILifeline、IMessage|相互作用図の生成と更新は、他の種類の図とはその操作方法が異なります。|
|[レイヤー図を拡張する](../modeling/extend-layer-diagrams.md)|ILayer、ILayerDiagram|レイヤー図を生成および編集するコードを記述できます。また、レイヤー図と照らし合わせてプログラム コードを検証することもできます。|

## <a name="about-the-implementation"></a>実装について
 UML モデリング ツールは[!INCLUDE[dsl](../includes/dsl-md.md)]上に構築されています。 それぞれのパッケージとそれぞれの図は[!INCLUDE[dsl](../includes/dsl-md.md)]モデルによって表されており、ルールとその他のメソッドのコレクションによって、パッケージと図の間の一貫性を保ちます。

 そのプラットフォームの型は、UML 拡張機能を記述するために参照するアセンブリの一部で表示されます。 [!INCLUDE[dsl](../includes/dsl-md.md)] API にアクセスすると、UML ツールへの拡張機能も作成できますが、次の事項を考慮に入れる必要があります。

- 単純と思われる変更によって一貫性が失われ、予測できない結果を引き起こすことがあります。

- 実装は将来的に変更されることがあるので、[!INCLUDE[dsl](../includes/dsl-md.md)] API を使用して行った調整が有効でなくなる場合があります。

## <a name="the-api-assemblies"></a>API アセンブリ
 この表は、UML ツールに機能拡張をもたらすアセンブリと、推奨される名前空間を示します。

|アセンブリ|名前空間|アクセス先|
|--------------|----------------|-------------------------|
|Microsoft.VisualStudio.Uml.Interfaces|(すべて)|UML の種類|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility|VisualStudio (Microsoft. アーキテクチャのアーキテクチャ)|[作成方法](../modeling/create-elements-and-relationships-in-uml-models.md)|
||Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation|[図と図形](../modeling/display-a-uml-model-on-diagrams.md)|
||Microsoft.VisualStudio.ArchitectureTools.Extensibility|[モデリング プロジェクト](../modeling/read-a-uml-model-in-program-code.md)|
|Microsoft.VisualStudio.Modeling.Sdk.[バージョン]|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement>|[メニューコマンドの拡張機能](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。<br /><br /> リンクされた[元に戻すトランザクション](../modeling/link-uml-model-updates-by-using-transactions.md)。|
||<xref:Microsoft.VisualStudio.Modeling.Validation>|[検証](../modeling/define-validation-constraints-for-uml-models.md)|
||(その他の名前空間)|高度な用途向け|
|Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[バージョン]|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement>|[ジェスチャハンドラー](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)。|
||(その他の名前空間)|高度な用途向け|
|Microsoft.VisualStudio.TeamFoundation.WorkItemTracking|Microsoft.VisualStudio.TeamFoundation.WorkItemTracking|[作業項目へのリンク](../modeling/define-a-work-item-link-handler.md)。|
|Microsoft.TeamFoundation.WorkItemTracking.Client|Microsoft.TeamFoundation.WorkItemTracking.Client|[作業項目とそのフィールド](../modeling/define-a-work-item-link-handler.md)。|
|Microsoft.TeamFoundation.Client|Microsoft.TeamFoundation.Client|[作業項目とそのフィールド](../modeling/define-a-work-item-link-handler.md)。|
|System.ComponentModel.Composition|<xref:System.ComponentModel.Composition>|[MEF コンポーネントのエクスポートとインポート](../modeling/define-and-install-a-modeling-extension.md)|
|System.Linq|<xref:System.Linq>|[コレクションの簡単な操作 (特にリレーションシップを扱う場合)](../modeling/navigate-relationships-with-the-uml-api.md)。|

## <a name="see-also"></a>参照
 Uml[モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md) [Uml モデリング機能拡張の API リファレンス](../modeling/api-reference-for-uml-modeling-extensibility.md)
