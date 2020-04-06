---
title: ボタン要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05bd73764e96a27a92d741f144c222acc48fa518
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739928"
---
# <a name="button-element"></a>ボタン要素
ユーザーが対話できる要素を定義します。 ボタン、メニューボタン、および分割ドロップダウンの種類のボタンを使用できます。

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
|guid|必須。 GUID/ID コマンド識別子の GUID です。|
|id|必須。 GUID/ID コマンド ID の ID。|
|priority|省略可能。 優先順位を指定する数値。|
|type|省略可能。 ボタンの種類を指定する列挙値。<br /><br /> 指定しない場合は、ボタンを使用します。<br /><br /> Button<br /> ツール バー (通常はアイコンボタン)、メニュー、およびコンテキスト メニューに表示される標準コマンド。<br /><br /> メニューボタン<br /> コマンドを実行せず、別のメニューを生成するメニュー項目。<br /><br /> スプリットドロップダウン<br /> Word の標準ツールバーの [元に戻す] ボタンや [やり直し] ボタンなどのコントロール。|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[親要素](../extensibility/parent-element.md)|省略可能。 ボタンの親要素。|
|[アイコン要素](../extensibility/icon-element.md)|省略可能。 ボタンに関連付けられているアイコン。|
|[コマンド フラグ要素](../extensibility/command-flag-element.md)|必須。 ボタンの有効なコマンド フラグ値は次のとおりです。<br /><br /> - 許可パラム<br /><br /> - コマンドウェルオンズのみ<br /><br /> - デフォルト無効<br /><br /> - デフォルト不可視<br /><br /> - ドントキャッシュ<br /><br /> - ダイナミックアイテムスタート<br /><br /> - ダイナミック可視性<br /><br /> - メニューコントローラー<br /><br /> - アイコンアンドテキスト<br /><br /> - ボタンなしカスタマイズ<br /><br /> - いいえカスタマイズ<br /><br /> - ノーキーカスタマイズ<br /><br /> - ノーショーオンメニューコントローラ<br /><br /> - ピクト<br /><br /> - ポストエクセ<br /><br /> - プルプロエティコマンド<br /><br /> - ルートトドックス<br /><br /> - テキストカスケードユースブタン<br /><br /> - テキストメニュー使用ボタン<br /><br /> - テキストの変更<br /><br /> - テキストの変更ボタン<br /><br /> - テキストコンテキストユースボタン<br /><br /> - テキストメニューCtrlメニュー<br /><br /> - テキストメニュー使用ボタン<br /><br /> - テキストのみ|
|[文字列要素](../extensibility/strings-element.md)|必須。 子[のボタンテキスト要素](../extensibility/buttontext-element.md)を定義する必要があります。|
|Annotation|オプションのコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ボタン要素](../extensibility/buttons-element.md)|ボタン要素をグループ化します。|

## <a name="example"></a>例
 次の例では *、.vsct*ファイルにボタンを定義します。

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
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
