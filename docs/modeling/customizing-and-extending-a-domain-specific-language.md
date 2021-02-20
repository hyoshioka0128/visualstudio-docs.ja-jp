---
title: ドメイン固有言語のカスタマイズおよび拡張
description: Visual Studio モデリングと視覚化 SDK (VMSDK) が、モデリングツールを定義できるいくつかのレベルを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, creating solutions
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9cfa8a3cda3f6bb2f564efe745a11863cf4d0e8a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945306"
---
# <a name="customize-and-extend-a-domain-specific-language"></a>ドメイン固有言語のカスタマイズと拡張

Visual Studio モデリングと視覚化 SDK (VMSDK) には、モデリングツールを定義できるいくつかのレベルが用意されています。

1. DSL 定義図を使用して、ドメイン固有言語 (DSL) を定義します。 図式記法、読み取り可能な XML フォーム、およびコードやその他の成果物を生成するために必要な基本ツールを使用して、DSL をすばやく作成できます。 詳細については、「 [Domain-Specific 言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。

2. DSL 定義のより高度な機能を使用して DSL を微調整します。 たとえば、ユーザーが要素を作成するときに、追加のリンクを表示できます。 これらの手法は DSL 定義でほとんど実現されていますが、いくつかのプログラムコードが必要です。

3. プログラムコードを使用してモデリングツールを拡張します。 VMSDK は特に、DSL 定義から生成されるコードにより、拡張機能を容易に統合できるようにすることを目的としています。 詳細については、「 [Domain-Specific 言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)」を参照してください。

> [!NOTE]
> DSL 定義ファイルを更新したら、ソリューションを再構築する前に、**ソリューションエクスプローラー** のツールバーにある [**すべてのテンプレートの変換**] を必ずクリックしてください。

## <a name="article-reference"></a>記事リファレンス

|この効果を実現するには|このトピックを参照してください|
|-|-|
|図形の色とスタイルのプロパティをユーザーが設定できるようにします。|図形またはコネクタクラスを右クリックし、[ **公開の追加**] をポイントして、項目をクリックします。|
|モデル要素のさまざまなクラスは、図に似ています。初期の高さ、幅、色、ツールヒントなどのプロパティを共有します。|図形またはコネクタクラス間の継承を使用します。 派生図形と派生ドメインクラス間のマッピングは、親のマッピングの詳細を継承します。<br /><br /> または、異なるドメインクラスを同じ shape クラスにマップします。|
|モデル要素のクラスは、さまざまな図形コンテキストによって表示されます。|複数のシェイプクラスを同じドメインクラスにマップします。 ソリューションをビルドするときに、エラー報告に従って、使用する図形を決定するために要求されたコードを指定します。|
|図形の色またはフォントなどのその他の機能は、現在の状態を示します。|「 [モデルを反映するための図形とコネクタの更新」を](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)参照してください。<br /><br /> 公開されたプロパティを更新するルールを作成します。 「 [ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。<br /><br /> または、OnAssociatedPropertyChanged () を使用して、リンク矢印やフォントなどの公開されていない機能を更新します。|
|状態を示すために変更された図形のアイコン。|DSL の詳細ウィンドウで、デコレータマッピングの表示を設定します。 同じ位置で複数のイメージのデコレーターを検索します。 「  [モデルを反映するための図形とコネクタの更新」を](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)参照してください。<br /><br /> または、をオーバーライド `ImageField.GetDisplayImage()` します。 「」の例を参照してください <xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField> 。|
|任意の図形に背景画像を設定する|InitializeInstanceResources () をオーバーライドして、固定された ImageField を追加します。|
|図形を任意の深さに入れ子にする|再帰的な埋め込みツリーを設定します。 図形を含めるように BoundsRules を定義します。|
|要素の境界上の固定ポイントでコネクタをアタッチします。|図の小さなポートで表される埋め込みのターミナル要素を定義します。 BoundsRules を使用して、適切なポートを修正します。 回路図のサンプルについては、「 [視覚化およびモデリング SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)」を参照してください。|
|テキストフィールド他の値から派生した値が表示されます。|テキストデコレータを計算済みまたはカスタムのストレージドメインプロパティにマップします。 詳細については、「 [計算済みおよびカスタムストレージのプロパティ](../modeling/calculated-and-custom-storage-properties.md)」を参照してください。|
|モデル要素間または図形間での変更の反映|「 [Domain-Specific 言語での検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください。|
|ストアの外部にある他の Visual Studio 拡張機能などのリソースに変更を反映します。|「 [イベントハンドラーによって変更がモデル外に反映される](../modeling/event-handlers-propagate-changes-outside-the-model.md)」を参照してください。|
|プロパティウィンドウ関連要素のプロパティが表示されます。|プロパティ転送を設定します。 「 [プロパティウィンドウのカスタマイズ」を](../modeling/customizing-the-properties-window.md)参照してください。|
|プロパティのカテゴリ|[プロパティ] ウィンドウは、カテゴリと呼ばれるセクションに分かれています。 ドメインのプロパティの **カテゴリ** を設定します。 同じカテゴリ名を持つプロパティは同じセクションに表示されます。 また、リレーションシップロールの **カテゴリ** を設定することもできます。|
|ドメインプロパティへのユーザーアクセスを制御する|Set は、ドメインプロパティが実行時にプロパティウィンドウに表示されないようにするために、ブラウズが false に設定 **されてい** ます。 テキストデコレーターにマップすることもできます。<br /><br /> **UI 読み取り専用である** ため、ユーザーはドメインプロパティを変更できません。<br /><br /> ドメインプロパティへのプログラムアクセスは影響を受けません。|
|DSL のモデルエクスプローラーで、ノードの名前、アイコン、可視性を変更します。|「 [モデルエクスプローラーのカスタマイズ](../modeling/customizing-the-model-explorer.md)」を参照してください。|
|コピー、切り取り、および貼り付けを有効にする|DSL エクスプローラーで、[**エディター** ] ノードの [**コピー貼り付けを有効にする**] プロパティを設定します。|
|要素がコピーされるたびに参照リンクとそのターゲットをコピーします。 たとえば、項目に添付されたコメントをコピーします。|ソースロールの [ **コピーの伝達** ] プロパティを設定します (DSL 定義図では、ドメインリレーションシップの片側の行で表されます)。<br /><br /> より複雑な効果を実現するために、ProcessOnCopy をオーバーライドするコードを記述します。<br /><br /> 「 [コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。|
|要素が削除されたときに関連要素を削除、再親、または再リンクします。|リレーションシップロールの [ **削除の反映** 値を設定する。 より複雑な効果を実現するには、 `ShouldVisitRelationship` `ShouldVisitRolePlayer` `MyDslDeleteClosure` **DomainModel.cs** で定義されているクラスのメソッドとメソッドをオーバーライドします。|
|コピーとドラッグアンドドロップで図形のレイアウトと外観を保持します。|コピーしたに図形とコネクタを追加し `ElementGroupPrototype` ます。 オーバーライドする最も便利な方法は、 `ElementOperations.CreateElementGroupPrototype()`<br /><br /> 「 [コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。|
|現在のカーソル位置など、選択した場所に図形を貼り付けます。|`ClipboardCommandSet.ProcessOnCopy()` `ElementOperations.Merge().` 「[コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。|
|貼り付け時に追加のリンクを作成する|ProcessOnPasteCommand () をオーバーライドします。|
|このダイアグラム、他の Dsl および Windows 要素からのドラッグアンドドロップを有効にする|「[方法: ドラッグアンドドロップハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)」を参照してください。|
|図形またはツールを、親にドラッグした場合と同様に、ポートなどの子図形にドラッグできるようにします。|削除されたオブジェクトを親に転送するために、ターゲットオブジェクトクラスに要素マージディレクティブを定義します。 「 [要素の作成と移動をカスタマイズ](../modeling/customizing-element-creation-and-movement.md)する」を参照してください。|
|図形またはツールを図形上にドラッグし、追加のリンクまたはオブジェクトを作成できるようにします。 たとえば、リンク先のアイテムにコメントをドロップできるようにします。|ターゲットドメインクラスに要素マージディレクティブを定義し、生成するリンクを定義します。 複雑な場合は、カスタムコードを追加できます。 「 [要素の作成と移動をカスタマイズ](../modeling/customizing-element-creation-and-movement.md)する」を参照してください。|
|1つのツールで要素のグループを作成します。 たとえば、固定されたポートセットを持つコンポーネントなどです。|ToolboxHelper.cs でツールボックスの初期化メソッドをオーバーライドします。 要素とそれらの関係リンクを含む要素グループプロトタイプ (EGP) を作成します。 「 [ツールとツールボックスのカスタマイズ」を](../modeling/customizing-tools-and-the-toolbox.md)参照してください。<br /><br /> EGP にプリンシパル図形とポート図形を含めるか、EGP がインスタンス化されるときにポート図形を配置する BoundsRules を定義します。|
|1つの接続ツールを使用して、複数の種類のリレーションシップをインスタンス化します。|ツールによって呼び出された接続ビルダーにリンク接続ディレクティブ (LCD) を追加します。 Lcd は、2つの要素の型からリレーションシップの種類を決定します。 これを要素の状態に依存させるには、カスタムコードを追加します。 「 [ツールとツールボックスのカスタマイズ」を](../modeling/customizing-tools-and-the-toolbox.md)参照してください。|
|固定ツール-ユーザーは任意のツールをダブルクリックして、多数の図形やコネクタを連続して作成できます。|DSL エクスプローラーで、ノードを選択し `Editor` ます。 プロパティウィンドウでは、[ **固定ツールボックスアイテムを使用** する] を設定します。|
|メニューコマンドの定義|「[方法: 標準メニューコマンドを変更](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)する」を参照してください。|
|検証ルールを使用してモデルを制限する|「 [Domain-Specific 言語での検証」を](../modeling/validation-in-a-domain-specific-language.md)参照してください。|
|DSL からコード、構成ファイル、またはドキュメントを生成します。|[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)|
|モデルをファイルに保存する方法をカスタマイズします。|「 [File Storage および XML シリアル化のカスタマイズ」を](../modeling/customizing-file-storage-and-xml-serialization.md)参照してください。|
|データベースまたはその他のメディアにモデルを保存します。|*言語* docdata をオーバーライドする<br /><br /> 「 [File Storage および XML シリアル化のカスタマイズ」を](../modeling/customizing-file-storage-and-xml-serialization.md)参照してください。|
|複数の Dsl を統合して、1つのアプリケーションの一部として動作させることができます。|「 [Visual Studio Modelbus を使用](../modeling/integrating-models-by-using-visual-studio-modelbus.md)したモデルの統合」を参照してください。|
|DSL がサードパーティによって拡張されることを許可し、拡張機能を制御します。|[MEF による DSL の拡張](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [DSL ライブラリによる DSL 間でのクラスの共有](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [ロック ポリシーの定義と読み取り専用セグメントの作成](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>関連項目

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
- [Domain-Specific 言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
