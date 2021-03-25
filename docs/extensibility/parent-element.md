---
title: 親要素 |Microsoft Docs
description: 親要素は、要素がボタン、コンボボックス、メニュー、またはグループの親であることを指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ac914fd3245982af89facb97ff2d528b410da99
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090383"
---
# <a name="parent-element"></a>親要素
ボタンまたはコンボボックスの親は、グループのみになることができます。 メニューまたはグループの親は、他のメニューまたはグループの場合もあります。 [Commandplacement 要素](../extensibility/commandplacement-element.md)では、この要素は必須です。それ以外のすべてのインスタンスでは、省略可能です。 この要素が省略された場合、の親は `Group_Undefined:0` 暗黙的に指定されます。

## <a name="syntax"></a>構文

```xml
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|

### <a name="child-elements"></a>子要素
 なし

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が統合開発環境 (IDE) に提供するコマンドを表すすべての要素を定義します。 たとえば、メニュー項目、メニュー、ツールバー、コンボボックスなどです。|
|[Buttons 要素](../extensibility/buttons-element.md)|グループ [ボタン要素](../extensibility/button-element.md) の要素。|
|[Menus 要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|
|[Groups 要素](../extensibility/groups-element.md)|VSPackage のコマンドグループを定義するエントリが含まれています。|

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
