---
title: コマンド配置要素 |マイクロソフトドキュメント
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
ms.openlocfilehash: a72b087652a654b563fd4e00bacc52290a29fe1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739699"
---
# <a name="commandplacements-element"></a>コマンド配置要素
コマンド配置要素は、コマンド配置要素とその他のコマンド配置グループをグループ化します。

 要素は省略可能です。 コマンド、グループ、またはメニューをセカンダリの場所に含める必要がない場合は *、.vsct*ファイルにこのセクションを含める必要はありません。

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
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|コマンド配置|コマンド配置要素とその他のコマンド配置のグループをグループ化します。|
|[コマンド配置要素](../extensibility/commandplacement-element.md)|複数のグループまたはメニューに含めるボタン、グループ、およびメニューを有効にします。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|コマンドを表す要素をすべて定義します。|

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
- [コマンド配置要素](../extensibility/commandplacement-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
