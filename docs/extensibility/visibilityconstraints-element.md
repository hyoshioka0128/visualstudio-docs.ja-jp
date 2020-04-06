---
title: 可視性制約要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VisibilityConstraints
helpviewer_keywords:
- VSCT XML schema elements, VisibilityConstraints
- VisibilityConstraints element (VSCT XML schema)
ms.assetid: d6dcd314-6fe4-4693-a189-91fa026c7b34
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1aaa9573b883910ac6fa5d921a9bc79ce1c1cf3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698193"
---
# <a name="visibilityconstraints-element"></a>可視性制約要素
VisibilityConstraints要素は、コマンドとツールバーのグループの静的な可視性を決定します。 可視性は、VSPackage を[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]読み込まずに統合開発環境 (IDE) によって制御されます。

## <a name="syntax"></a>構文

```xml
<VisibilityConstraints>
  <VisibilityItem />
  <VisibilityItem />
</VisibilityConstraints>
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
|[可視性項目要素](../extensibility/visibilityitem-element.md)|コマンドとツール バーの静的な表示を決定します。|
|[可視性制約](../extensibility/visibilityconstraints-element.md)|コマンドとツールバーのグループの静的な表示を決定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンド (メニュー項目、メニュー、ツールバー、コンボ ボックスなど) を表す要素をすべて定義します。|

## <a name="example"></a>例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>関連項目
- [可視性項目要素](../extensibility/visibilityitem-element.md)
- [コマンド テーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
