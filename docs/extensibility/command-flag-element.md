---
title: コマンドフラグ要素 |Microsoft Docs
description: コマンドフラグ要素によって、その親要素が変更されます。 親要素と子要素を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f9f9db3d7a8146bd7b44cf779fd62fd75803d86
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089642"
---
# <a name="command-flag-eelement"></a>コマンドフラグ Eelement
親要素を変更します。

## <a name="syntax"></a>構文

```
<CommandFlag>DynamicVisibility</CommandFlag>
```

## <a name="attributes-and-elements"></a>属性と要素
 次のセクションでは、有効な要素の値について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|値|説明|
|-----------|-----------------|
|AllowParams|コマンドの正規名を入力するときに、ユーザーが **コマンドウィンドウに** コマンドパラメーターを入力できることを示します。<br /><br /> 有効期間: `Button`|
|常に作成|メニューは、グループまたはボタンがない場合でも作成されます。<br /><br /> 有効期間: `Menu`|
|[CaseSensitive]|ユーザーエントリでは大文字と小文字が区別されます。<br /><br /> 有効期間: `Combo`|
|CommandWellOnly|コマンドがトップレベルメニューに表示されず、キーボードショートカットにバインドするなど、追加のシェルカスタマイズに使用できるようにする場合は、このフラグを適用します。 VSPackage をインストールした後、[ **オプション** ] ダイアログボックスを開き、[ **キーボード環境** ] カテゴリの下にあるコマンドの配置を編集して、これらのコマンドをカスタマイズできます。 このフラグは、ショートカットメニュー、ツールバー、メニューコントローラー、またはサブメニューの配置には影響しません。<br /><br /> 有効な対象: `Button` 、 `Combo`|
|DefaultDisabled|既定では、このコマンドを実装する VSPackage が読み込まれていないか、メソッドが呼び出されていない場合、コマンドは無効になり `QueryStatus` ます。<br /><br /> 有効な対象: `Button` 、 `Combo`|
|DefaultDocked|既定ではドッキングされます。 この設定は、常にドッキングされているため、ツールバーには適用されなくなりました。|
|Defaul/Visible|既定では、このコマンドを実装する VSPackage が読み込まれていない場合、または `QueryStatus` メソッドが呼び出されていない場合、コマンドは非表示になります。<br /><br /> これをフラグと組み合わせて使用することをお勧めし `DynamicVisibility` ます。<br /><br /> 有効な対象: `Button` 、 `Combo` 、 `Menu`|
|DontCache|開発環境では、 `QueryStatus` このコマンドのメソッドの結果はキャッシュされません。<br /><br /> メニューの場合、メニュー項目のテキストをキャッシュしないようにメニューコントローラーに指示します。 このフラグは、動的なテキストを持つ動的な項目または項目がメニューに含まれている場合に使用します。<br /><br /> 有効な対象: `Button` 、 `Menu`|
|DynamicItemStart|動的リストの先頭を示します。 これにより、 `QueryStatus` OLECMDERR_E_UNSUPPORTED フラグが返されるまでリスト項目に対してメソッドを連続して呼び出すことで、環境を構築できます。 これは、最近使用した (MRU) リストやウィンドウリストなどの項目に適しています。<br /><br /> 有効期間: `Button`|
|DynamicVisibility|コマンドの表示を変更するには、メソッドを使用する `QueryStatus` か、セクションに含まれているコンテキスト GUID を使用し `VisibilityConstraints` ます。<br /><br /> メニューおよびツールウィンドウのツールバーに表示されるコマンドに適用されますが、メインウィンドウに表示されるトップレベルのツールバーには適用されません。 OLECMDF_INVISIBLE フラグがメソッドから返された場合、最上位のツールバー項目は無効にすることができますが、非表示にすることはできません `QueryStatus` 。 ツールウィンドウのツールバーに表示されるツールバーコマンドは非表示にすることができます。<br /><br /> メニューでは、このフラグは、すべてのメンバーが非表示になっている場合に、自動的に非表示にする必要があることも示しています。 このフラグは、通常、トップレベルのメニューには既にこの動作があるため、サブメニューに割り当てられます。<br /><br /> このフラグは、フラグと組み合わせる必要があり `DefaultInvisible` ます。<br /><br /> 有効な対象: `Button` 、 `Combo` 、 `Menu`|
|フィルタ|「 [コンボ要素](../extensibility/combo-element.md)」の「フィルター処理キー」を参照してください。<br /><br /> 有効期間: `Combo`|
|FixMenuController|このコマンドがメニューコントローラーに配置されている場合、コマンドは常に既定値になります。つまり、メニューコントローラーボタン自体が選択されるたびに、コマンドが選択されます。 メニューコントローラーにフラグが設定されている場合、 `TextIsAnchorCommand` メニューコントローラーは、フラグが設定されているコマンドからもテキストを受け取り `FixMenuController` ます。<br /><br /> メニューコントローラーでは、1つのコマンドのみにフラグを設定する必要があり `FixMenuController` ます。 複数のコマンドがマークされている場合は、メニューの最後のコマンドが既定のコマンドになります。<br /><br /> 有効期間: `Button`|
|IconAndText|メニューとツールバーにアイコンとテキストを表示します。<br /><br /> 有効な対象: `Button` 、 `Combo` 、 `Menu`|
|NoAutoComplete|オートコンプリート機能が無効になっています。<br /><br /> 有効期間: `Combo`|
|NoButtonCustomize|ユーザーがこのボタンをカスタマイズできないようにします。<br /><br /> 有効な対象: `Button` 、 `Combo`|
|NoKeyCustomize|キーボードのカスタマイズを有効にしないでください。<br /><br /> 有効な対象: `Button` 、 `Combo`|
|NoShowOnMenuController|このコマンドがメニューコントローラーに配置されている場合、このコマンドはドロップダウンリストに表示されません。<br /><br /> 有効期間: `Button`|
|NotInTBList|は、使用可能なツールバーの一覧に表示されません。 これは、ツールバーのメニューの種類に対してのみ有効です。<br /><br /> 有効期間: `Menu`|
|NoToolbarClose|ユーザーはツールバーを閉じることができません。 これは、ツールバーのメニューの種類に対してのみ有効です。<br /><br /> 有効期間: `Menu`|
|Pict|ツールバーにはアイコンのみが表示され、メニューにはテキストのみが表示されます。 アイコンが指定されていない場合は、ツールバーのクリック可能な空白領域を表示します。<br /><br /> 有効期間: `Button`|
|PostExec|コマンドをブロックしないようにします。 開発環境は、処理前のすべてのクエリが完了するまで実行を延期します。<br /><br /> 有効期間: `Button`|
|RouteToDocs|コマンドは、アクティブなドキュメントにルーティングされます。<br /><br /> 有効期間: `Button`|
|StretchHorizontally|このフラグが設定されている場合、幅はコンボボックスの最小幅になります。また、ツールバーに空き領域がある場合、コンボボックスは使用可能なスペースを埋めるように拡大されます。 これは、ツールバーが水平方向にドッキングされていて、ツールバー上の1つのコンボボックスのみがフラグを使用できる場合にのみ発生します (最初のコンボボックス以外では、フラグはすべて無視されます)。<br /><br /> 有効期間: `Combo`|
|TextChanges|コマンドまたはメニューテキストは、通常、メソッドを使用して実行時に変更でき `QueryStatus` ます。<br /><br /> 有効な対象: `Button` 、 `Menu`|
|Text[テキストの置換] ボタン|有効期間: `Button`|
|TextIsAnchorCommand|メニューコントローラーの場合は、メニューのテキストが既定の (アンカー) コマンドから取得されます。 アンカーコマンドは、最後に選択またはラッチされたコマンドです。 このフラグが設定されていない場合、メニューコントローラーは独自のフィールドを使用し `MenuText` ます。 ただし、メニューコントローラーをクリックしても、そのコントローラーから最後に選択したコマンドが有効になります。<br /><br /> このフラグとフラグを組み合わせることをお勧めし `TextChanges` ます。<br /><br /> このフラグは、MenuController 型または Menucontroller ラッチ型のメニューにのみ適用されます。<br /><br /> 有効期間: `Menu`|
|TextMenuCtrlUseMenu|`MenuText`メニューコントローラーのフィールドを使用します。 既定のフィールドは `ButtonText` です。<br /><br /> 有効期間: `Button`|
|TextMenuUseButton|`ButtonText`メニューのフィールドを使用します。 既定のフィールドは、指定され `MenuText` ている場合はです。<br /><br /> 有効期間: `Button`|
|TextOnly|ツールバーまたはメニューにはテキストのみを表示しますが、アイコンが指定されている場合でもアイコンは表示しません。<br /><br /> 有効期間: `Button`|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Buttons 要素](../extensibility/buttons-element.md)|[ボタン要素](../extensibility/button-element.md)の要素のグループを提供します。|
|[Menus 要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio コマンドテーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
