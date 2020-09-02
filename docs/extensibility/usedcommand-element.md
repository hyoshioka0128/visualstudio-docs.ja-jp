---
title: Used Command 要素 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65030c3fe24c3456b0c4c99a667362d2a4c67703
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698822"
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

## <a name="remarks"></a>解説
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
