---
title: Strings 要素 |Microsoft Docs
description: Strings 要素には、ButtonText 子要素と、その他の省略可能な子要素が含まれています。 テキスト文字列内のアンパサンドは、ショートカットキーを指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a0bd9ad9b8059eb7fd566c1e0c26a938af6d18b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089902"
---
# <a name="strings-element"></a>文字列要素
Strings 要素には、少なくとも **Buttontext** 子要素が含まれている必要があります。 その他のすべての子要素は省略可能です。 ' & ' や ' < ' などの無効な XML 文字は、エンティティ (' ' と ' ' など) としてコーディングする必要があり &amp; &lt; ます。

 テキスト文字列内のアンパサンドは、コマンドのショートカットキーを指定します。

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
|language|省略可能。 Language = "."。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|ButtonText|このフィールドとコマンド定義内の5つの次のテキストフィールドを使用すると、さまざまなメニューに表示されるテキストを指定できます。 既定では、この `ButtonText` フィールドはメニューコントローラーに表示されます。 フィールドは、 `ButtonText` 他のテキストフィールドが空白の場合にも既定値になります。 `ButtonText`他のテキストフィールドが指定されている場合でも、フィールドを空白にすることはできません。|
|ToolTipText|フィールドは、 `ToolTipText` メニュー項目のツールヒントに表示されるテキストを指定します。<br /><br /> `ToolTipText`フィールドが空白の場合は、 `ButtonText` フィールドが使用されます。|
|MenuText|`MenuText`このフィールドは、コマンドがメインメニュー、ツールバー、ショートカットメニュー、またはサブメニュー上にある場合に、コマンドに対して表示されるテキストを指定します。 `MenuText`フィールドが空白の場合、統合開発環境 (IDE) はフィールドを使用し `ButtonText` ます。 `MenuText`フィールドはローカライズにも使用できます。<br /><br /> ショートカットメニューの場合、 `MenuText` フィールドはショートカットメニューのツールバーに表示される名前です。これにより、IDE のショートカットメニューをカスタマイズできます。 そのため、ショートカットメニューの名前を指定してください。たとえば、"Shortcut" ではなく "ウィジェットパッケージのショートカットメニュー" を使用します。<br /><br /> `MenuText`フィールドが指定されていない場合 `ButtonText` は、フィールドが使用されます。|
|CommandName|このフィールドは、[ `CommandName` **ユーザー設定**] ダイアログボックスの [**コマンド**] タブの [キーボード] カテゴリに表示されるテキストを指定します ([**ツール**] メニューの [**カスタマイズ**] をクリックして利用できます)。|
|CanonicalName|英語のフィールドは、コマンド `CanonicalName` の名前を英語のテキストで指定します。これは、メニュー項目を実行するために **コマンド** ウィンドウに入力できます。 IDE では、文字、数字、アンダースコア、または埋め込み期間以外の文字は除去されます。 次に、このテキストをフィールドに連結し `ButtonText` て、コマンドを定義します。 たとえば、[**ファイル**] メニューの [**新しいプロジェクト**] がコマンド NewProject になります。<br /><br /> 英語の `CanonicalName` フィールドが指定されていない場合、IDE はフィールドを使用 `ButtonText` し、文字、数字、アンダースコア、および埋め込み期間以外のすべてを除去します。 たとえば、ボタンテキスト "&定義コマンド..."は DefineCommands になり、アンパサンド、スペース、および省略記号が削除されます。<br /><br /> `TextChanges`フラグが指定されていて、コマンドのテキストが変更された場合、**コマンド** ウィンドウによって認識される対応するコマンドは変更されません。元のフィールドまたは英語のフィールドの正規の形式が維持され `ButtonText` `CanonicalName` ます。|
|LocCanonicalName|`LocCanonicalName`フィールドは、英語のフィールドと同じように動作し `CanonicalName` ますが、ローカライズされたコマンドテキストを指定できます。 両方の正規フィールドを指定できます。 IDE では、 **コマンド** ウィンドウに入力されたテキストを解析してコマンドに関連付けるだけなので、英語と英語以外のテキストの両方を同じコマンドに関連付けることができます。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Button 要素](../extensibility/button-element.md)|ユーザーが操作できる要素を定義します。|
|[Menu 要素](../extensibility/menu-element.md)|1つのメニュー項目を定義します。|
|[Combo 要素](../extensibility/combo-element.md)|コンボボックスに表示されるコマンドを定義します。|

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
