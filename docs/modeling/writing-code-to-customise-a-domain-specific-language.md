---
title: ドメイン固有言語をカスタマイズする
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b67a50623eb1924c4a18b57524c409f7eba6ab20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546875"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>ドメイン固有言語をカスタマイズするコードを記述する

このセクションでは、カスタムコードを使用して、ドメイン固有言語でモデルにアクセス、変更、またはモデルを作成する方法について説明します。

DSL で動作するコードを記述できるコンテキストがいくつかあります。

- **カスタムコマンド。** ダイアグラムを右クリックして、ユーザーが呼び出すことができるコマンドを作成できます。このコマンドは、モデルを変更できます。 詳細については、「 [方法: ショートカットメニューにコマンドを追加](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)する」を参照してください。

- **検証。** モデルが正しい状態であることを確認するコードを記述できます。 詳細については、「 [ドメイン固有言語での検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください。

- **既定の動作をオーバーライドします。** DslDefinition. dsl から生成されるコードの多くの側面を変更できます。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。

- **テキスト変換。** モデルにアクセスするコードを含むテキストテンプレートを作成し、テキストファイルを生成することができます。たとえば、プログラムコードを生成します。 詳細については、「 [ドメイン固有言語からコードを生成する](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

- **その他の Visual Studio 拡張機能。** モデルの読み取りと変更を行う別の VSIX 拡張機能を作成できます。 詳細については、「[方法: プログラムコードでファイルからモデルを開く](../modeling/how-to-open-a-model-from-file-in-program-code.md)」を参照してください。

DslDefinition. dsl で定義したクラスのインスタンスは、 *メモリ内ストア* (IMS) または *ストア*と呼ばれるデータ構造に保持されます。 DSL で定義するクラスは、常にコンストラクターの引数としてストアを受け取ります。 たとえば、DSL が Example というクラスを定義しているとします。

`Example element = new Example (theStore);`

(通常のオブジェクトとしてではなく) ストアにオブジェクトを保持すると、いくつかの利点があります。

- **Transactions**。 一連の関連する変更を1つのトランザクションにグループ化することができます。

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     変更中に例外が発生し、最終的なコミット () が実行されない場合、ストアは以前の状態にリセットされます。 これにより、エラーによってモデルが不整合な状態にならないようにすることができます。 詳細については、「 [プログラムコードでのモデルの移動と更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

- **バイナリリレーションシップ**。 2つのクラス間のリレーションシップを定義する場合、両方のインスタンスには、もう一方の端に移動するプロパティがあります。 2つの端は常に同期されます。 たとえば、親と子という名前のロールを持つ親リレーションシップを定義する場合、次のように記述できます。

     `John.Children.Add(Mary)`

     次の式はどちらも true になります。

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     次のように記述すると、同じ効果を得ることもできます。

     `Mary.Parents.Add(John)`

     詳細については、「 [プログラムコードでのモデルの移動と更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

- **ルールとイベント**。 指定された変更が行われるたびに起動する規則を定義できます。 たとえば、モデル要素を使用して、図の図形を最新の状態に保つために、ルールが使用されます。 詳細については、「 [変更に対する応答と反映](../modeling/responding-to-and-propagating-changes.md)」を参照してください。

- **シリアル化**。 ストアには、ファイルに格納されているオブジェクトをシリアル化するための標準的な方法が用意されています。 シリアル化および逆シリアル化の規則をカスタマイズできます。 詳細については、「 [File Storage および XML シリアル化のカスタマイズ](../modeling/customizing-file-storage-and-xml-serialization.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語のカスタマイズおよび拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)