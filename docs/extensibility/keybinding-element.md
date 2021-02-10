---
title: キーバインド要素 |Microsoft Docs
description: キーバインド要素は、コマンドのキーボードショートカットを指定します。 コマンドには、単一キーバインドとデュアルキーバインドの両方を関連付けることができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ce96da36a8c6eff0fda71d8a5d077721876ab8b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943349"
---
# <a name="keybinding-element"></a>キーバインド要素
キーバインド要素は、コマンドのキーボードショートカットを指定します。

 コマンドには、単一キーバインドとデュアルキーバインドの両方を関連付けることができます。 1つのキーバインドの例としては、 + [**保存**] コマンドの Ctrl **S** があります。 デュアルキーバインドでは、コマンドをトリガーするために2つの連続するキーの組み合わせが必要です。 2つのキーのバインドの例として、 <strong>ctrl *+</strong> k、ctrl <strong>+</strong> k *<strong>、</strong>* ブックマークの設定などがあります。

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
|エディター|必須。 エディターの GUID は、このショートカットキーがアクティブになる編集コンテキストを示します。 グローバルバインドスコープの値は "guidVSStd97" です。|
|key1|必須。 有効な値には、すべての種類の英数字を含めることができます。また、2桁の16進値の前に0x と [VK_constants](/windows/desktop/inputdev/virtual-key-codes)を指定します。|
|mod1|任意。 スペースで区切られた **Ctrl**、 **Alt**、および **Shift** の任意の組み合わせ。|
|key2|任意。 有効な値には、すべての種類の英数字を含めることができます。また、2桁の16進値の前に0x と [VK_constants](/windows/desktop/inputdev/virtual-key-codes)を指定します。|
|mod2|任意。 スペースで区切られた **Ctrl**、 **Alt**、および **Shift** の任意の組み合わせ。|
|エミュレーター|任意。|
|条件|任意。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent||
|注釈||

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[キーバインド要素](../extensibility/keybindings-element.md)|キーバインド要素とその他のキーバインドグループをグループ化します。|

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
- [キーバインド要素](../extensibility/keybindings-element.md)
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
