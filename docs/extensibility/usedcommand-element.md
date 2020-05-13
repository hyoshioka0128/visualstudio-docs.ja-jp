---
title: 使用コマンド要素 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698822"
---
# <a name="usedcommand-element"></a>UsedCommand 要素
VSPackage が別の .vsct ファイルで定義されているコマンドにアクセスできるようにします。 たとえば、VSPackage がシェルで定義されている標準**のコピー**コマンドを[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]使用する場合は、コマンドを再実装せずにメニューまたはツール バーに追加できます。

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
|条件|省略可能。 [「条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|なし||

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[UsedCommands 要素](../extensibility/usedcommands-element.md)|グループ UsedCommand 要素とその他の UsedCommands グループ化します。|

## <a name="remarks"></a>Remarks
 `<UsedCommands>`要素にコマンドを追加することで、VSPackage は、VSPackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]がコマンドを必要とすることを環境に通知します。 パッケージで必要な`<UsedCommand>`コマンドの要素を追加する必要があります。 たとえば、Visual C++ 固有のコマンドをパッケージから呼び出す場合、そのコマンドの要素を含まない限り、Visual Web `<UsedCommand>` Developer のユーザーはこのコマンドを使用できません。

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
