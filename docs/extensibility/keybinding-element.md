---
title: キーバインド要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b458e70a9a85c11707c50da2e16e3aa73f51bc12
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703146"
---
# <a name="keybinding-element"></a>キーバインド要素
KeyBinding 要素は、コマンドのキーボード ショートカットを指定します。

 コマンドには、単一キーとデュアルキーの両方のバインディングを関連付けることができます。 1 つのキー・バインディングの例として、「**保存**」コマンドの**Ctrl**+**S**があります。 デュアル・キー・バインディングでは、コマンドをトリガーするために 2 つの連続したキーの組み合わせが必要です。 二重キーバインドの例としては<strong>、Ctrl*+</strong>K<strong>+</strong><strong>、Ctrl</strong>K** を使用してブックマークを設定します。

## <a name="syntax"></a>構文

```
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。|
|id|必須。|
|エディター|必須。 エディター GUID は、このキーボード ショートカットがアクティブになる編集コンテキストを示します。 グローバル バインディング スコープの値は "guidVSStd97" です。|
|key1|必須。 有効な値には、すべての入力可能な英数字、および 0x と[VK_constants](/windows/desktop/inputdev/virtual-key-codes)が付いた 2 桁の 16 進数値が含まれます。|
|モッド1|省略可能。 **Ctrl** **、Alt、** および**Shift**の任意の組み合わせをスペースで区切ります。|
|key2|省略可能。 有効な値には、すべての入力可能な英数字、および 0x と[VK_constants](/windows/desktop/inputdev/virtual-key-codes)が付いた 2 桁の 16 進数値が含まれます。|
|モッズ2|省略可能。 **Ctrl** **、Alt、** および**Shift**の任意の組み合わせをスペースで区切ります。|
|エミュレーター|省略可能。|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent||
|Annotation||

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[キーバインディング要素](../extensibility/keybindings-element.md)|グループキーバインド要素とその他のキーバインドグループ。|

## <a name="example"></a>例

```
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>関連項目
- [キーバインディング要素](../extensibility/keybindings-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
