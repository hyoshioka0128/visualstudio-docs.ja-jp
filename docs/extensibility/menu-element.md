---
title: メニュー要素 |マイクロソフトドキュメント
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
ms.openlocfilehash: 8dc4731f95e31781f6b10704d7cb14dc83e96d7a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702595"
---
# <a name="menu-element"></a>メニュー要素
1 つのメニュー項目を定義します。 コンテキスト、メニュー、メニューコントローラ、メニューコントローララッチ、ツールバー、およびツールウィンドウツールバーの6種類のメニューがあります。

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
|guid|必須。 GUID/ID コマンド識別子の GUID です。|
|id|必須。 GUID/ID コマンド ID の ID。|
|priority|省略可能。 メニューのグループ内のメニューの相対位置を指定する数値。|
|ツールバープライオリティインバンド|省略可能。 ウィンドウがドッキングされているときに、バンド内のツール バーの相対位置を指定する数値。|
|type|省略可能。 要素の種類を指定する列挙値。<br /><br /> 存在しない場合、既定の種類はメニューです。<br /><br /> Context<br /> ユーザーがウィンドウを右クリックしたときに表示されるショートカット メニュー。 ショートカット メニューには、次の特性があります。<br /><br /> - メニューをショートカット メニューとして表示する場合は、[**親**] フィールドと [**優先度]** フィールドを使用しません。<br />- サブメニューとして、またショートカットメニューとして使用することができます。 この場合、グループ**ID**と**優先度**の両方のフィールドが優先されます。<br />- 常に利用できるとは限りません。<br /><br /> ショートカット メニューは、次の条件に該当する場合にのみ表示されます。<br /><br /> - ホストするウィンドウが表示されます。<br />- VSPackage のマウス ハンドラーは、ウィンドウを右クリックして、コマンドを処理するメソッドを呼び出します。<br />- ショートカット メニューは、メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A>(推奨される方法) またはメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>を呼び出すことによって表示されます。<br /><br /> メニュー<br /> ドロップダウン メニューを提供します。 ドロップダウン メニューには、次の特性があります。<br /><br /> - その定義の中で親を尊重します。<br />- 親グループ、またはグループへのコマンド配置が必要です。<br />- 他の種類のメニューのサブメニューにすることができます。<br />- 親メニューが表示されるたびに自動的に表示されます。<br />- 表示する VSPackage コードの実装は必要ありません。<br /><br /> メニューコントローラ<br /> ツールバーで通常使用される分割ボタンのドロップダウン メニューを提供します。 メニューコントローラメニューには、次の特徴があります。<br /><br /> - 親またはコマンド配置を使用して別のメニューに含まれている必要があります。<br />- その定義の中で親を尊重します。<br />- 親としてメニューの任意の種類を持つことができます。<br />- 親メニューが表示されるたびに自動的に使用可能になります。<br />- メニューを表示するためにプログラムによるサポートは必要ありません。<br /><br /> 分割ボタンメニューのコマンドがメニューボタンに表示されます。 表示されるコマンドには、次のいずれかの特性があります。<br /><br /> - コマンドがまだ表示され、有効になっている場合に使用された最後のコマンドです。<br />- 最初に表示されたコマンドです。<br /><br /> メニューコントローララッチ<br /> コマンドをラッチとしてマークすることで、コマンドを既定の選択として指定できる分割ボタンのドロップダウン メニューを提供します。<br /><br /> ラッチコマンドは、メニューで選択済みとしてマークされているコマンドで、通常はチェックマークを表示します。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コマンドは、インターフェイスの`QueryStatus`メソッドの実装でOLECMDF_LATCHED フラグが設定されている場合、ラッチとしてマークできます。 メニューコントローララッチメニューには、次の特徴があります。<br /><br /> - 親グループまたはコマンド配置を介して別のメニューに含まれている必要があります。<br />- その定義の中で親を尊重します。<br />- 親としてメニューの任意の種類を持つことができます。<br />- 親メニューが表示される場合はいつでも使用できます。<br />- メニューを表示するためにプログラムによるサポートは必要ありません。<br /><br /> 分割ボタンメニューのコマンドがメニューボタンに表示されます。 表示されるコマンドには、次のいずれかの特性があります。<br /><br /> - ラッチされた最初の表示コマンドです。<br />- 最初に表示されたコマンドです。<br /><br /> ツール バー<br /> ツール バーを提供します。 ツールバーには、次の特性があります。<br /><br /> - 定義内の親を無視します。<br />- CommandPlacement を使用しても、グループのサブメニューを作成できません。<br />- [**表示**] メニュー**の [ツールバー** ] をクリックすると、常に表示できます。<br />- [VisibilityItem](../extensibility/visibilityitem-element.md)を使用して表示できます。<br />- 作成するコードは必要ありません。 ツールバーの作成方法の例については、「ツールバーの[追加](../extensibility/adding-a-toolbar.md)」を参照してください。<br /><br /> ツールウィンドウツールバー<br /> ツール バーが開発環境にアタッチされているのと同様に、特定のツール ウィンドウにアタッチされるツール バーを提供します。<br /><br /> - 定義内の親を無視します。<br />- CommandPlacement を使用しても、グループのサブメニューを作成できません。<br />- ツール バーをホストするツール ウィンドウが表示され、VSPackage がツール ウィンドウにツール バーを明示的に追加した場合にのみ表示されます。 これは通常、ツール ウィンドウフレームからツール バー ホスト プロパティ (<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost>インターフェイスで表される) を取得し、メソッドを呼び出すことによって<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A>、ツール ウィンドウを作成するときに行われます。|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|省略可能。 メニュー項目の親要素。|
|コマンドフラグ|必須。 [コマンド フラグ要素](../extensibility/command-flag-element.md)を参照してください。 メニューの有効なコマンド フラグの値は次のとおりです。<br /><br /> -   **常に作成します。**<br />-   **デフォルトドッキング**<br />-   **デフォルト非表示**- このフラグは、ツールバーの表示に影響しません。<br />-   **ドントキャッシュ**<br />-   **動的な可視性**- このフラグは、ツールバーの表示に影響しません。<br />-   **アイコンアンドテキスト**<br />-   **いいえカスタマイズ**<br />-   **リスト**<br />-   **ノーツールバー閉じる**<br />-   **テキストの変更**<br />-   **テキストはアンカーコマンド**|
|文字列|必須。 [「文字列要素](../extensibility/strings-element.md)」を参照してください。 子`ButtonText`要素を定義する必要があります。|
|Annotation|オプションのコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[メニュー要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|

## <a name="example"></a>例

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
    <CommandFlag>AlwaysCreate</CommandFlag>
    <Strings>
      <ButtonText>Edit Widget</ButtonText>
    </Strings>
    </Parent>
</Menu>
```

## <a name="see-also"></a>関連項目
- [ファイルのコマンド テーブル (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
