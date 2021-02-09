---
title: VisibilityItem 要素 |Microsoft Docs
description: VisibilityItem 要素は、コマンドおよびツールバーの静的表示を決定します。 エントリは、コマンドまたはメニュー、および関連付けられているコマンド UI コンテキストを識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16615dfdbfd7e9762046e37899ecf23619837ae2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926017"
---
# <a name="visibilityitem-element"></a>VisibilityItem 要素
要素は、 `VisibilityItem` コマンドおよびツールバーの静的表示を決定します。 すべてのエントリは、コマンドまたはメニュー、および関連付けられたコマンド UI コンテキストを識別します。 Visual Studio では、コマンド、メニュー、ツールバー、およびそれらを定義する Vspackage が読み込まれていないかどうかが検出されます。 IDE では、メソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> コマンド UI コンテキストがアクティブかどうかを判断します。

 VSPackage が読み込まれた後、Visual Studio では、ではなく VSPackage によってコマンドの可視性が求められ `VisibilityItem` ます。 コマンドの可視性を判断するには、コマンドを <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 実装した <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法に応じて、イベントハンドラーまたはメソッドを実装します。

 要素を含むコマンドまたはメニューは、 `VisibilityItem` 関連付けられたコンテキストがアクティブな場合にのみ表示されます。 1つのコマンド、メニュー、またはツールバーを1つ以上のコマンド UI コンテキストと関連付けるには、各コマンドコンテキストの組み合わせのエントリを追加します。 コマンドまたはメニューが複数のコマンド UI コンテキストに関連付けられている場合は、関連付けられているコマンド UI コンテキストのいずれかがアクティブになっていると、コマンドまたはメニューが表示されます。

 要素は、 `VisibilityItem` グループではなく、コマンド、メニュー、およびツールバーにのみ適用されます。 関連要素を持たない要素は、 `VisibilityItem` 親メニューがアクティブになっている場合は常に表示されます。

## <a name="syntax"></a>構文

```xml
<VisibilityItem
  guid ="="cmdGuidMyProductCommands"
  id=="cmdidAddWidget"
  context="guidNotViewSourceMode"/>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|context|必須。 コマンドが表示される UI コンテキスト。|
|条件|任意。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素
 なし

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)|要素は、 `VisibilityConstraints` コマンドおよびツールバーのグループを静的に表示するかどうかを決定します。|

## <a name="remarks"></a>解説
 標準の Visual Studio UI コンテキストは、 *Visual STUDIO SDK のインストールパス*\VisualStudioIntegration\Common\Inc\vsshlids.h ファイルだけでなく、クラスおよびクラスでも定義されてい <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> ます。 UI コンテキストの完全なセットは、クラスで定義されてい <xref:Microsoft.VisualStudio.VSConstants> ます。

## <a name="example"></a>例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)
- [Visual Studio コマンドテーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
