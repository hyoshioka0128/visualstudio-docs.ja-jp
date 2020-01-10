---
title: XML エディターの IntelliSense 機能
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2b26f214-cc3a-46bf-b260-14eb8e599182
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 609684452190bf7471f90fee75f66dbb2fcbec8e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592387"
---
# <a name="xml-editor-intellisense-features"></a>XML エディターの IntelliSense 機能

XML エディターでは、Visual Studio で提供されている他の言語のエディターに相当する、フル機能の IntelliSense を利用できます。 このセクションでは、XML スキーマ定義言語 (XSD) ドキュメントと XSLT ドキュメントで IntelliSense を使用する方法について説明します。

## <a name="intellisense-in-an-xsd-document"></a>XSD ドキュメント内の IntelliSense

ドキュメントにスキーマが関連付けられると、XML エディター ツールバーの **オブジェクトメンバーリストを表示** ボタンを `"<"` またはクリックするたびに、期待される要素のドロップダウンリストが表示されます。

![[オブジェクトメンバーリストの表示] ボタン](media/display-object-member-list-xml.png)

スキーマを XML ドキュメントに関連付ける方法の詳細については、「 [xml ドキュメントの検証](../xml-tools/xml-document-validation.md)」を参照してください。

開始タグの内部で「SPACE」と入力しても、現在の要素に追加できる属性をすべて示したドロップダウン リストを表示できます。

属性値に `"="` と入力するか、値のために開始引用符を入力した場合も、その属性で使用できる値の一覧を表示できます。 この場合、値を提示させるには、スキーマで `xsd:enumeration` ファセットを通じて列挙値が提供されているか、属性が `Boolean` 型である必要があります。 `xml:lang` や、`simpleType` から派生した `xsd:language` に関しても、IntelliSense によって既知の言語コードの一覧が提供されます。 名前空間の宣言に関しては、IntelliSense によって既知の `targetNamespace` 値の一覧が提供されます。

IntelliSense が提供する使用可能な値の一覧は、要素が `">"` であるときに、開始タグを閉じるために `simpleType` を入力した場合にも表示されます。 要素に関する動作は、前のパラグラフで説明した属性に関する動作に似ています。

このような IntelliSense の一覧には、関連付けられているスキーマで見つかった `xsd:annotation` および `xsd:documentation` の情報に基づくツール ヒントも表示されます。

## <a name="intellisense-in-an-xslt-document"></a>XSLT ドキュメント内の IntelliSense

XSLT ドキュメントに名前付きテンプレートまたは属性を追加した後は、IntelliSense を使用して次の項目を挿入できます。

- 属性セット名。

- テンプレート モード。

- テンプレート名。

- 特定のモードのパラメーター名。

- 特定の名前付きテンプレートのパラメーター名。

詳細については、「[チュートリアル: XSLT IntelliSense の使用](../xml-tools/walkthrough-using-xslt-intellisense.md)」を参照してください。

## <a name="auto-completion"></a>オートコンプリート

XML エディターでは、必要な XML 構文が自動的に入力されるため、XML の編集も容易になっています。 たとえば、次の開始タグを入力します。

`<book>`

XML エディターにより終了タグが入力され、カーソルが開始タグの後に置かれます。 この例を次に示します ("&#124;" カーソル位置に注意してください)。

`<book>`&#124;`</book>`

属性値には常に引用符が必要であるため、XML エディターは引用符を自動的に入力します。 たとえば、次のように入力します。

`<book title=`

XML エディターにより引用符が追加され、カーソルが引用符の間に置かれます。

`<book title="`&#124;`"`

同様に、XML エディターは次の XML 構文も自動的に挿入します。

- 処理命令の終了 : `?>`

- CDATA ブロックの終了 : `]]>`

- コメントの終了 : `-->`

- DTD 宣言の終了 : `>`

また、IntelliSense リストから名前空間の修飾された要素または属性を選択し、その要素または属性の名前空間がまだスコープ内にない場合は、XML エディターで名前空間の宣言を挿入することもできます。

たとえば、IntelliSense の一覧から `e:Book` 要素を選択したときに、プレフィックスが、ドキュメント内で宣言されていない `http://books` 名前空間に関連付けられている場合は、XML エディターによって必要な名前空間宣言が自動的に挿入されます。 結果の XML テキストを次に示します。

`<e:Book xmlns:e="http://books"`

## <a name="brace-matching"></a>かっこの照合

XML エディターでは、中かっこを強調表示することにより、閉じたばかりの要素について即座にフィードバックを返します。 また、キーボードショートカット (**Ctrl**+ **]** ) を使用して、1つの中かっこから対応する中かっこにジャンプすることもできます。

XML エディターは、この動作を次の項目に対して行います。

- 対応する開始タグと終了タグ

- "\<" または ">" 山かっこのペア。

- コメントの開始と終了

- 処理命令の開始と終了

- CDATA ブロックの開始と終了

- DTD 宣言の開始と終了

- 属性の開始と終了の引用符

## <a name="modify-the-intellisense-options"></a>IntelliSense オプションを変更する

IntelliSense とオートコンプリートの機能は、既定で有効になっています。 ただし、**ツール** > **オプション**の設定を変更することで、これを変更することができます。

**[その他]** ページの **[自動挿入]** セクションでは、次の動作を制御します。

|[名前]|説明|
|-|-----------------|
|終了タグ|新しい要素の終了タグを挿入します。|
|属性値の引用符|新しい属性の名前を入力するときに属性値の引用符を挿入します。|
|その他のマークアップ|コメント、CDATA、DOCTYPE、処理命令、およびその他のマークアップ宣言を完了します。|

### <a name="to-change-the-auto-completion-behavior"></a>オートコンプリートの動作を変更するには

1. **[ツール]** メニューの **[オプション]** を選択します。

2. **[テキストエディター]** 、 **[XML]** の順に展開し、 **[その他]** を選択します。

3. **[自動挿入]** セクションに変更を加え、 **[OK]** をクリックします。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
- [IntelliSense の使用](../ide/using-intellisense.md)
- [チュートリアル: XSLT IntelliSense の使用](../xml-tools/walkthrough-using-xslt-intellisense.md)
