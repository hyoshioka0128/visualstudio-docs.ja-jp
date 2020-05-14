---
title: コマンド要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3ea2400cca19a02475caecec3d022e0b78794ae4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739692"
---
# <a name="commands-element"></a>Commands 要素
VSPackage ツール バーのコマンドのコレクションを表します。 コレクションには、メニュー、グループ、ボタン、コンボ、ビットマップの 5 つのサブセクションを含めることができます。

 各サブセクションの子要素 (たとえば\<、メニュー>) は、GUID と数値識別子のペアである一意のコマンド ID によって識別されます。 GUID は "コマンド セット" を識別し、論理的に関連するコマンドをグループ化するために使用されます。 VSPackage は、他の VSPackages によって定義されているコマンド ID との衝突を避けるために、独自のコマンド セットを定義する必要があります。

## <a name="syntax"></a>構文

```xml
<Commands package="GuidMyPackage" >
  <Menus>... </Menus>
  <Groups>... </Groups>
  <Buttons>... </Buttons>
  <Combos>... </Combos>
  <Bitmaps>... </Bitmaps>
</Commands>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|package|コマンドを提供する VSPackage を識別する GUID。<br /><br /> たとえば、パッケージ="guidVsPackage1Pkg"。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[メニュー要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|
|[Groups 要素](../extensibility/groups-element.md)|VSPackage のコマンド グループを定義するエントリが含まれています。|
|[ボタン要素](../extensibility/buttons-element.md)|ボタン要素をグループ化します。|
|[ビットマップ要素](../extensibility/bitmaps-element.md)|ビットマップ要素をグループ化します。|
|[コンボ要素](../extensibility/combos-element.md)|コンボ要素をグループ化します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンドを表すすべての要素を定義します。 使用可能な要素は、メニュー項目、メニュー、ツールバー、およびコンボ ボックスです。|

## <a name="example"></a>例
 次の例は、[コマンド要素](../extensibility/commands-element.md)を使用する方法を示しています。

```
<Commands package="guidMyPackage">
    <Menus>
      <Menu Condition="'%(DEBUG)' != 'true'"
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"
        priority="0x0000" type="Menu">
        <Annotation>
          <Documentation>this is an annotation</Documentation>
          <AppInfo>
            <CustomData>
              <CustomSubElement>Some data</CustomSubElement>
            </CustomData>
          </AppInfo>
        </Annotation>
        <CommandFlag>AlwaysCreate</CommandFlag>
        <Strings>
          <ButtonText>MainMenu</ButtonText>
        </Strings>
      </Menu>
  </Menus>
<Commands>
```

## <a name="see-also"></a>関連項目
- [VSPackages がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
