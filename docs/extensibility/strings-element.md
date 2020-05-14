---
title: 文字列要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: db44db8926b523665a21c00b710dcee55749ab89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699731"
---
# <a name="strings-element"></a>文字列要素
文字列要素には、少なくとも **、ボタンテキスト**子要素が含まれている必要があります。 その他の子要素はすべて省略可能です。 '&' や '<' などの無効な XML 文字は、エンティティ&amp;('&lt;' ' および ' など) としてコーディングする必要があります。

 テキスト文字列内のアンパサンドは、コマンドのキーボード ショートカットを指定します。

## <a name="syntax"></a>構文

```
<Strings>
  <ButtonText>... </ButtonText>
  <CommandName>... </CommandName>
</Strings>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|language|省略可能。 言語="."|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|ボタンテキスト|このフィールドとコマンド定義の次の 5 つのテキストフィールドを使用すると、さまざまなメニューに表示されるテキストを指定できます。 デフォルトでは、この`ButtonText`フィールドはメニューコントローラに表示されます。 他`ButtonText`のテキスト フィールドが空白の場合も、このフィールドが既定値になります。 他`ButtonText`のテキスト フィールドが指定されていても、フィールドを空白にすることはできません。|
|Tooltiptext|この`ToolTipText`フィールドは、メニュー項目のツールヒントに表示されるテキストを指定します。<br /><br /> フィールドが`ToolTipText`空白の場合は、`ButtonText`フィールドが使用されます。|
|メニューテキスト|この`MenuText`フィールドは、コマンドがメイン メニュー、ツールバー、ショートカット メニュー、またはサブメニューにある場合に表示されるテキストを指定します。 フィールドが`MenuText`空白の場合、統合開発環境 (IDE) はフィールド`ButtonText`を使用します。 この`MenuText`フィールドは、ローカリゼーションにも使用できます。<br /><br /> ショートカット メニューの`MenuText`場合、フィールドは[ショートカット メニュー]ツールバーに表示される名前で、IDE のショートカット メニューをカスタマイズできます。 したがって、ショートカット メニューに名前を付ける方法は具体的に指定してください。たとえば、「ショートカット」ではなく「ウィジェットパッケージショートカットメニュー」を使用します。<br /><br /> フィールドが`MenuText`指定されていない場合は、フィールド`ButtonText`が使用されます。|
|CommandName|この`CommandName`フィールドは、[**ユーザー設定**] ダイアログ ボックスの [**コマンド**] タブのキーボード カテゴリに表示されるテキストを指定します **([ツール]** メニューの [**ユーザー設定**] をクリックして使用できます)。|
|正規名|English`CanonicalName`フィールドは、コマンド・ウィンドウでメニュー項目を実行するために入力できる **、英語**のテキストでコマンドの名前を指定します。 IDE は、文字、数字、アンダースコア、または埋め込みピリオド以外の文字を取り除きます。 このテキストは、`ButtonText`フィールドに連結されてコマンドを定義します。 たとえば、[**ファイル]** メニューの **[新しいプロジェクト**] がコマンドの [ファイル.NewProject] になります。<br /><br /> 英語`CanonicalName`のフィールドが指定されていない場合、IDE はフィールド`ButtonText`を使用し、文字、数字、アンダースコア、および埋め込みピリオドを除くすべての文字を削除します。 たとえば、ボタンテキスト「コマンドを定義&.」とします。は、アンパサンド、スペース、および省略記号が削除される DefineCommands になります。<br /><br /> フラグが`TextChanges`指定され、コマンドのテキストが変更された場合、コマンド ウィンドウで認識される対応する**コマンド**は変更されません。元`ButtonText`のフィールドまたは英語`CanonicalName`のフィールドの正規形式のままです。|
|ロクナニカル名|フィールド`LocCanonicalName`は English`CanonicalName`フィールドと同じ動作をしますが、ローカライズされたコマンド テキストを指定できます。 両方の標準フィールドを指定できます。 IDE は**コマンド**ウィンドウに入力されたテキストを解析し、コマンドに関連付けるだけなので、英語と英語以外の両方のテキストを同じコマンドに関連付けることができます。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Button 要素](../extensibility/button-element.md)|ユーザーが対話できる要素を定義します。|
|[Menu 要素](../extensibility/menu-element.md)|単一のメニュー項目を定義します。|
|[Combo 要素](../extensibility/combo-element.md)|コンボ ボックスに表示されるコマンドを定義します。|

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
