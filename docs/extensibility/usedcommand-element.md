---
title: Used Command 要素 |Microsoft Docs
description: VSPackage は、別の vsct ファイルで定義されているコマンドにアクセスできるようにするコマンド要素です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 30ff89cba5dbc1e54afaf51fb659e07c29e53009
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060225"
---
# <a name="usedcommand-element"></a>UsedCommand 要素
VSPackage が別の vsct ファイルで定義されているコマンドにアクセスできるようにします。 たとえば、VSPackage がシェルによって定義されている標準の **コピー** コマンドを使用する場合、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コマンドを再実装せずにメニューまたはツールバーに追加できます。

## <a name="syntax"></a>構文

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 コマンドを識別する GUID ID ペアの GUID。|
|id|必須。 コマンドを識別する GUID ID ペアの ID。|
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|なし||

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[UsedCommands 要素](../extensibility/usedcommands-element.md)|グループ化されたコマンド要素とその他の実行コマンドグループ。|

## <a name="remarks"></a>注釈
 VSPackage は、要素にコマンドを追加することにより、 `<UsedCommands>` [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage がコマンドを必要とすることを環境に通知します。 `<UsedCommand>`パッケージが必要とするすべてのバージョンおよび構成に含まれていない可能性があるすべてのコマンドに対して、要素を追加する必要があります。 たとえば、パッケージが Visual C++ に固有のコマンドを呼び出すと、コマンドに要素を含めない限り、Visual Web Developer のユーザーはこのコマンドを使用できません `<UsedCommand>` 。

## <a name="example"></a>例

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>関連項目
- [UsedCommands 要素](../extensibility/usedcommands-element.md)
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
