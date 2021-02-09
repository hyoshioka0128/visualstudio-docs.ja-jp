---
title: Button 要素 |Microsoft Docs
description: Button 要素は、ユーザーが操作できる要素を定義します。 ボタンは、ボタン、メニューボタン、および SplitDropDown という異なる種類にすることができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 51b202db9210fa5c1f3d5b26b5177cc0b5e1e0a2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927315"
---
# <a name="button-element"></a>Button 要素
ユーザーが操作できる要素を定義します。 ボタンには、ボタン、MenuButton、および SplitDropDown のさまざまな種類があります。

## <a name="syntax"></a>構文

```
<Button guid="guidMyCommandSet" id="MyCommand" priority="0x102" type="button">
  <Parent>... </Parent>
  <Icon>... </Icon>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Button>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|priority|任意。 優先度を示す数値です。|
|type|任意。 ボタンの種類を指定する列挙値。<br /><br /> 指定されていない場合は、ボタンを使用します。<br /><br /> Button<br /> ツールバーに表示される標準コマンド (通常はアイコンボタン)、メニュー、およびコンテキストメニュー。<br /><br /> MenuButton<br /> コマンドを実行せずに別のメニューを生成するメニュー項目。<br /><br /> SplitDropDown<br /> Microsoft Word の [標準] ツールバーの [元に戻す] および [やり直し] ボタンなどのコントロール。|
|条件|任意。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[親要素](../extensibility/parent-element.md)|任意。 ボタンの親要素。|
|[Icon 要素](../extensibility/icon-element.md)|任意。 ボタンに関連付けられているアイコン。|
|[Command flag 要素](../extensibility/command-flag-element.md)|必須。 ボタンの CommandFlag の有効な値は次のとおりです。<br /><br /> -AllowParams<br /><br /> - CommandWellOnly<br /><br /> -DefaultDisabled<br /><br /> -Defaul/Visible<br /><br /> -DontCache<br /><br /> -DynamicItemStart<br /><br /> -DynamicVisibility<br /><br /> -FixMenuController<br /><br /> -IconAndText<br /><br /> -NoButtonCustomize<br /><br /> -NoCustomize<br /><br /> -NoKeyCustomize<br /><br /> -NoShowOnMenuController<br /><br /> -Pict<br /><br /> -PostExec<br /><br /> - ProfferedCmd<br /><br /> -RouteToDocs<br /><br /> - TextCascadeUseBtn<br /><br /> -TextMenuUseButton<br /><br /> -TextChanges<br /><br /> -Text] ボタン<br /><br /> -TextContextUseButton<br /><br /> - TextMenuCtrlUseMenu<br /><br /> -TextMenuUseButton<br /><br /> -TextOnly|
|[Strings 要素](../extensibility/strings-element.md)|必須。 子の [Buttontext 要素](../extensibility/buttontext-element.md) を定義する必要があります。|
|注釈|コメント (省略可能)。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Buttons 要素](../extensibility/buttons-element.md)|グループボタン要素。|

## <a name="example"></a>例
 次の例では、 *vsct* ファイルでボタンを定義しています。

 ```xml
<Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
    <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
    <Icon guid="guidImages" id="bmpPic1" />
    <CommandFlag>TextChanges</CommandFlag>
    <Strings>
          <CommandName>cmdidMyCommand</CommandName>
          <ButtonText>My Command name</ButtonText>
    </Strings>
</Button>
 ```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
