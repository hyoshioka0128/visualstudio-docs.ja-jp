---
title: Menu 要素 |Microsoft Docs
description: Menu 要素は、1つのメニュー項目を定義します。 メニューの種類は、コンテキスト、メニュー、MenuController、Menucontroller ラッチ、Toolbar、および ToolWindowToolbar です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f20e05c50bf208490edd237299653a3caa6b559f
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97616076"
---
# <a name="menu-element"></a>Menu 要素
1つのメニュー項目を定義します。 これらは、コンテキスト、メニュー、MenuController、Menucontroller ラッチ、Toolbar、および ToolWindowToolbar の6種類のメニューです。

## <a name="syntax"></a>構文

```xml
<Menu guid="guidMyCommandSet" id="MyCommand" priority="0x100" type="button">
  <Parent>... </Parent>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Menu>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|priority|省略可能。 メニューのグループ内のメニューの相対位置を指定する数値。|
|ToolbarPriorityInBand|省略可能。 ウィンドウがドッキングされているときのバンド内のツールバーの相対位置を指定する数値。|
|type|省略可能。 要素の種類を指定する列挙値。<br /><br /> 存在しない場合、既定の型は Menu です。<br /><br /> コンテキスト<br /> ユーザーがウィンドウを右クリックしたときに表示されるショートカットメニュー。 ショートカットメニューには、次の特性があります。<br /><br /> -メニューがショートカットメニューとして表示される場合、は **親** フィールドと **優先順位** フィールドを使用しません。<br />-サブメニューとして、またはショートカットメニューとしても使用できます。 この場合、 **グループ ID** と **優先順位** の両方のフィールドが尊重されます。<br />-常に使用できるとは限りません。<br /><br /> ショートカットメニューは、次の条件に該当する場合にのみ表示されます。<br /><br /> -それをホストするウィンドウが表示されます。<br />-VSPackage のマウスハンドラーは、ウィンドウを右クリックして、コマンドを処理するメソッドを呼び出します。<br />-ショートカットメニューは、 <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A> メソッド (推奨される方法) またはメソッドを呼び出すことによって表示され <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> ます。<br /><br /> メニュー<br /> ドロップダウンメニューを提供します。 ドロップダウンメニューには、次の特性があります。<br /><br /> -定義内の親を尊重します。<br />-親グループ、またはグループへの CommandPlacement が必要です。<br />-他の種類のメニューのサブメニューでもかまいません。<br />-親メニューが表示されるたびに自動的に表示されます。<br />-VSPackage コードを表示するために実装する必要はありません。<br /><br /> MenuController<br /> ツールバーで通常使用される分割ボタンのドロップダウンメニューを提供します。 MenuController メニューには、次の特性があります。<br /><br /> -親または CommandPlacement を使用して別のメニューに含める必要があります。<br />-定義内の親を尊重します。<br />-任意の種類のメニューを親として持つことができます。<br />-親メニューが表示されるたびに、自動的に使用できるようになります。<br />-メニューを表示するために、プログラムによるサポートは必要ありません。<br /><br /> 分割ボタンメニューのコマンドがメニューボタンに表示されます。 表示されるコマンドには、次のいずれかの特性があります。<br /><br /> -これは、コマンドが引き続き表示され、有効になっている場合に使用された最後のコマンドです。<br />-これは最初に表示されるコマンドです。<br /><br /> Menuコントローラーのラッチ<br /> コマンドをラッチ済みとしてマークすることにより、コマンドを既定の選択として指定できる分割ボタンのドロップダウンメニューを提供します。<br /><br /> ラッチされたコマンドは、選択としてメニューでマークされたコマンドで、通常はチェックマークが表示されます。 コマンドは、インターフェイスのメソッドの実装で OLECMDF_LATCHED フラグが設定されている場合、ラッチとしてマークでき `QueryStatus` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 Menuコントローラーのラッチには、次の特性があります。<br /><br /> -親グループまたは CommandPlacement を使用して別のメニューに含める必要があります。<br />-定義内の親を尊重します。<br />-任意の種類のメニューを親として持つことができます。<br />-親メニューが表示されるたびに使用できるようになります。<br />-メニューを表示するために、プログラムによるサポートは必要ありません。<br /><br /> 分割ボタンメニューのコマンドがメニューボタンに表示されます。 表示されるコマンドには、次のいずれかの特性があります。<br /><br /> -これは、最初に表示されるコマンドであり、ラッチされます。<br />-これは最初に表示されるコマンドです。<br /><br /> ツール バー<br /> ツールバーを提供します。 ツールバーには、次の特性があります。<br /><br /> -定義内の親を無視します。<br />-CommandPlacement を使用しても、グループのサブメニューを作成することはできません。<br />-[**表示**] メニューの [**ツールバー** ] をクリックすると、いつでも表示できます。<br />- [VisibilityItem](../extensibility/visibilityitem-element.md)を使用して表示できます。<br />-作成するコードは必要ありません。 ツールバーの作成方法の例については、「 [ツールバーの追加](../extensibility/adding-a-toolbar.md)」を参照してください。<br /><br /> ToolWindowToolbar<br /> ツールバーが開発環境にアタッチされるのと同じように、特定のツールウィンドウに関連付けられているツールバーを提供します。<br /><br /> -定義内の親を無視します。<br />-CommandPlacement を使用しても、グループのサブメニューを作成することはできません。<br />-ツールバーをホストするツールウィンドウが表示され、VSPackage がツールバーをツールウィンドウに明示的に追加した場合にのみ表示されます。 これは通常、ツールウィンドウが作成されるときに、ツールウィンドウのフレームからツールバーのホストプロパティ (インターフェイスによって表される) を取得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> し、メソッドを呼び出すことによって行われ <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> ます。|
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|省略可能。 メニュー項目の親要素。|
|CommandFlag|必須。 「 [Command flag 要素](../extensibility/command-flag-element.md)」を参照してください。 メニューの有効な CommandFlag 値は次のとおりです。<br /><br /> -   **常に作成**<br />-   **DefaultDocked**<br />-   **Defaul/visible** -このフラグは、ツールバーの表示には影響しません。<br />-   **DontCache**<br />-   **Dynamicvisibility** -このフラグは、ツールバーの表示には影響しません。<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextChanges**<br />-   **TextIsAnchorCommand**|
|文字列|必須。 「 [Strings 要素](../extensibility/strings-element.md)」を参照してください。 子 `ButtonText` 要素を定義する必要があります。|
|Annotation|コメント (省略可能)。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Menus 要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|

## <a name="example"></a>例

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit"/>
  <CommandFlag>AlwaysCreate</CommandFlag>
  <Strings>
    <ButtonText>Edit Widget</ButtonText>
  </Strings>
</Menu>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
