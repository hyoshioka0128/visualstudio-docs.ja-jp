---
title: CommandPlacements 要素 |Microsoft Docs
description: Commandplacements 要素は、Commandplacements 要素とその他のコマンド配置グループをグループ化します。 CommandPlacements 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CommandPlacements
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 78a5724a-3b9f-4c78-9c0d-8faa3924f81c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 301fe17f3ad12bfd1e150d9bf48180be6cb62adc
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94974013"
---
# <a name="commandplacements-element"></a>CommandPlacements 要素
Commandplacements 要素は、Commandplacements 要素とその他のコマンド配置グループをグループ化します。

 CommandPlacements 要素は省略可能です。 コマンド、グループ、またはメニューが2次拠点に含まれていない場合は、このセクションを *vsct* ファイルに含める必要はありません。

## <a name="syntax"></a>構文

```xml
<CommandPlacements>
  <CommandPlacement>... </CommandPlacement>
  <CommandPlacement>... </CommandPlacement>
</CommandPlacements>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|CommandPlacements|CommandPlacement 要素とその他のコマンド配置グループをグループ化します。|
|[CommandPlacement 要素](../extensibility/commandplacement-element.md)|ボタン、グループ、およびメニューを複数のグループまたはメニューに含めることができるようにします。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|コマンドを表すすべての要素を定義します。|

## <a name="example"></a>例

```xml
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>関連項目
- [CommandPlacement 要素](../extensibility/commandplacement-element.md)
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
