---
title: コマンド配置要素 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739737"
---
# <a name="commandplacement-element"></a>コマンド配置要素
CommandPlacement 要素を使用すると、ボタン、グループ、およびメニューを複数のグループまたはメニューに含めることができ、 CommandPlacement 要素を使用すると、ユーザー インターフェイスの外観を変更するためにこれらの項目を完全に再定義する必要はありません。

 詳細については、「[ボタンの再利用可能なグループを作成する](../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

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
|guid|必須。 [Symbols 要素](../extensibility/symbols-element.md)で定義されているコマンド セットの GUID。|
|id|必須。 で定義されているメニュー、グループ、またはコマンドの ID を指定します`Symbols Element`。|
|priority|必須。 親要素内の項目の視覚的な位置を決定します。|
|条件|省略可能。 [「条件付き A 属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|必須。 配置する項目をホストするメニューまたはグループ。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド配置要素](../extensibility/commandplacements-element.md)|コマンド配置要素とコマンド配置要素のグループを指定します。|

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
- [コマンド配置要素](../extensibility/commandplacements-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
