---
title: 親要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c018505ba06762bf8426f266b24ee1835313c29
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702223"
---
# <a name="parent-element"></a>親要素
ボタンまたはコンボ ボックスの親はグループにしかできません。 メニューまたはグループの親は、他のメニューまたはグループである場合があります。 では、[この要素](../extensibility/commandplacement-element.md)は必須です。他のすべてのインスタンスでは、これはオプションです。 この要素を省略すると、親`Group_Undefined:0`が暗黙的に指定されます。

## <a name="syntax"></a>構文

```xml
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID です。|
|id|必須。 GUID/ID コマンド識別子の ID。|

### <a name="child-elements"></a>子要素
 None

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|統合開発環境 (IDE) に VSPackage が提供するコマンドを表すすべての要素を定義します。 たとえば、メニュー項目、メニュー、ツールバー、コンボ ボックスなどです。|
|[ボタン要素](../extensibility/buttons-element.md)|ボタン[要素の](../extensibility/button-element.md)グループ。|
|[メニュー要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|
|[Groups 要素](../extensibility/groups-element.md)|VSPackage のコマンド グループを定義するエントリが含まれています。|

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
