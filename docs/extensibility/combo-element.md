---
title: コンボ要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 18ff9d9e20ec221a86f1cce5f9c43a4e47ed6dc2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739823"
---
# <a name="combo-element"></a>コンボ要素
コンボ ボックスに表示されるコマンドを定義します。 コンボ ボックスには、次の 4 種類があります: ドロップダウン コンボ、動的コンボ、インデックスコンボ、および MRUCombo。

## <a name="syntax"></a>構文

```xml
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">
  <Parent>... </Parent
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</combo>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID です。|
|id|必須。 GUID/ID コマンド ID の ID。|
|既定の幅|必須。 コンボ ボックスのピクセル幅を指定する整数。|
|一覧|必須。 コンボ ボックスに表示される項目の一覧を取得するために、アクティブなコマンド ターゲットに送信される ID。 ID は、コントロールと同じ GUID スコープ内に置かれる。|
|priority|省略可能。 優先順位を指定する数値。|
|type|省略可能。 ボタンの種類を指定する列挙値。<br /><br /> 指定しない場合は、ボタンを使用します。<br /><br /> ドロップダウンコンボ<br /> VSPackage は、このコンボ ボックスの内容を入力する役割を担います。 ユーザーは、このドロップダウンのテキスト ボックスに何も入力できません。<br /><br /> ダイナミックコンボ<br /> VSPackage は、このコンボ ボックスの内容を入力する役割を担います。 ユーザーはこのコンボを編集し、その中の項目を選択することもできます。<br /><br /> インデックスコンボ<br /> DynamicCombo と同じですが、テキストではなく項目のインデックスを上げる点が異なります。<br /><br /> MRUコンボ<br /> VSPackage の代わりに統合開発環境 (IDE) によって満たされます。  ユーザーはこのコンボ ボックスで編集できます。 IDE は、コンボ ボックスごとに最後の 16 個のエントリまで記憶します。<br /><br /> ユーザーがコンボ ボックスで何かを選択するか、新しいものを入力すると、IDE は適切な VSPackage を通知します。|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|省略可能。 ボタンの親要素。|
|コマンドフラグ|必須。 [コマンド フラグ要素](../extensibility/command-flag-element.md)を参照してください。 ボタンの有効なコマンド フラグ値は次のとおりです。<br /><br /> - 大文字と小文字を区別する<br /><br /> - コマンドウェルオンズのみ<br /><br /> - デフォルト無効<br /><br /> - デフォルト不可視<br /><br /> - ダイナミック可視性<br /><br /> - フィルタキー<br /><br /> - アイコンアンドテキスト<br /><br /> - オートコンプリートなし<br /><br /> - ボタンなしカスタマイズ<br /><br /> - いいえカスタマイズ<br /><br /> - ノーキーカスタマイズ<br /><br /> - 水平ストレッチ|
|文字列|必須。 [「文字列要素](../extensibility/strings-element.md)」を参照してください。 子のボタンテキスト要素を定義する必要があります。|
|Annotation|オプションのコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド要素](../extensibility/commands-element.md)|VSPackage ツール バーのコマンドのコレクションを表します。|

## <a name="example"></a>例

```xml
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>

<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  priority="0x0500" type="DropDownCombo" defaultWidth="100"
  idCommandList="cmdidGetInsertOptionsList">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
