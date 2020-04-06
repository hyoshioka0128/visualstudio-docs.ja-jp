---
title: 可視性アイテム要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9129d64e430d661bbdd8f7682e64c93650570211
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698147"
---
# <a name="visibilityitem-element"></a>可視性項目要素
この`VisibilityItem`要素は、コマンドとツールバーの静的な表示を決定します。 すべてのエントリは、コマンドまたはメニュー、および関連付けられたコマンド UI コンテキストを識別します。 Visual Studio は、コマンド、メニュー、およびツール バー、およびそれらの表示を検出します。 IDE では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>このメソッドを使用して、コマンド UI コンテキストがアクティブかどうかを判断します。

 VSPackage が読み込まれた後、Visual Studio はコマンドの可視性が VSPackage`VisibilityItem`ではなくによって決定されることを想定しています。 コマンドの可視性を判断するには、コマンドの<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>実装方法に応じて、イベント<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>ハンドラーまたはメソッドを実装します。

 要素を持つコマンドまたはメニュー`VisibilityItem`は、関連付けられたコンテキストがアクティブな場合にのみ表示されます。 コマンドコンテキストの組み合わせごとにエントリを含めることで、1 つまたは複数のコマンド UI コンテキストに 1 つのコマンド、メニュー、またはツールバーを関連付けることができます。 コマンドまたはメニューが複数のコマンド UI コンテキストに関連付けられている場合、関連付けられているコマンド UI コンテキストのいずれかがアクティブになっているときに、コマンドまたはメニューが表示されます。

 この`VisibilityItem`要素は、コマンド、メニュー、およびツールバーにのみ適用され、グループには適用されません。 関連する`VisibilityItem`要素を持たない要素は、親メニューがアクティブである場合には常に表示されます。

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
|id|必須。 GUID/ID コマンド ID の ID。|
|context|必須。 コマンドが表示される UI コンテキスト。|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素
 None

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[可視性制約要素](../extensibility/visibilityconstraints-element.md)|この`VisibilityConstraints`要素は、コマンドとツールバーのグループの静的な可視性を決定します。|

## <a name="remarks"></a>Remarks
 標準の Visual Studio UI コンテキストは *、Visual Studio SDK のインストール パス*\VisualStudioIntegration\Common\Inc\vsshlids.h<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>ファイルおよび クラス<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>で定義されています。 より完全な UI コンテキストのセットがクラスで<xref:Microsoft.VisualStudio.VSConstants>定義されます。

## <a name="example"></a>例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [可視性制約要素](../extensibility/visibilityconstraints-element.md)
- [コマンド テーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
