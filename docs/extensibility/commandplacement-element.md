---
title: CommandPlacement 要素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 2cbd7ac8-c55a-43d8-a26d-713b3d790016
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dcf9f23b5e860b895baa4c2a7a783f2ee15fcc77
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739737"
---
# <a name="commandplacement-element"></a>CommandPlacement 要素
CommandPlacement 要素を使用すると、ボタン、グループ、およびメニューを複数のグループまたはメニューに含めることができます。 CommandPlacement 要素を使用すると、ユーザーインターフェイスの外観を変更するために、これらの項目を完全に再定義する必要はありません。

 詳細については、「 [再利用可能なボタンのグループの作成](../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

## <a name="syntax"></a>構文

```
<CommandPlacement guid="guidMyCommandSet" id="MyCommand" priority="0x001" >
  <Parent>... </Parent>
</CommandPlacement>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 [Symbols 要素](../extensibility/symbols-element.md)で定義されているコマンドセットの guid。|
|id|必須。 に定義されている、配置するメニュー、グループ、またはコマンドの id `Symbols Element` 。|
|priority|必須。 親要素内の項目の視覚的な位置を決定します。|
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|必須。 配置する項目をホストするメニューまたはグループ。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandPlacements 要素](../extensibility/commandplacements-element.md)|Commandplacements 要素および Commandplacements 要素のグループを指定します。|

## <a name="example"></a>例

```
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>関連項目
- [CommandPlacements 要素](../extensibility/commandplacements-element.md)
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
