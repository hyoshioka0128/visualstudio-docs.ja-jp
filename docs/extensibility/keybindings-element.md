---
title: キーバインディング要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- KeyBindings
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBindings element (VSCT XML schema)
ms.assetid: 26a15d5c-ddea-4977-af7f-d795ff09c7ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: df1720286007d8f6acf073c21f5b2dcc8486782c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703134"
---
# <a name="keybindings-element"></a>キーバインディング要素
KeyBindings 要素グループキーバインド要素およびその他のキーバインドグループ。

## <a name="syntax"></a>構文

```xml
<KeyBindings>
  <KeyBinding>... </KeyBinding>
  <KeyBinding>... </KeyBinding>
</KeyBindings>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[キーバインド要素](../extensibility/keybinding-element.md)|コマンドのキーボード ショートカットを指定します。|
|[Keybindings](../extensibility/keybindings-element.md)|グループキーバインド要素とその他のキーバインドグループ。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|コマンドを表す要素をすべて定義します。|

## <a name="example"></a>例

```xml
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>関連項目
- [キーバインド要素](../extensibility/keybinding-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
