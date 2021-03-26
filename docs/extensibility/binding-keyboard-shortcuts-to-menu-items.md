---
title: キーボードショートカットをメニュー項目にバインドする |Microsoft Docs
description: 既定のエディターまたはカスタムエディターのいずれかについて、Visual Studio のキーボードショートカットをカスタムボタン、メニュー項目、またはツールバーコマンドにマップする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88cc7d91ee8cd24daae278efdbfd35271412af40
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097306"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>メニュー項目にキーボードショートカットをバインドする
ショートカットキーをカスタムメニューコマンドにバインドするには、パッケージの *vsct* ファイルにエントリを追加するだけです。 このトピックでは、キーボードショートカットをカスタムボタン、メニュー項目、またはツールバーコマンドにマップする方法と、キーボードマップを既定のエディターで適用する方法、またはカスタムエディターに制限する方法について説明します。

 既存の Visual Studio のメニュー項目にキーボードショートカットを割り当てるには、「 [キーボードショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」を参照してください。

## <a name="choose-a-key-combination"></a>キーの組み合わせを選択する
 Visual Studio では、多くのキーボードショートカットが既に使用されています。 重複するバインドは検出が困難で、予期しない結果が生じる可能性があるため、複数のコマンドに同じショートカットを割り当てることはできません。 そのため、割り当てる前にショートカットが使用可能かどうかを確認することをお勧めします。

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>ショートカットキーが使用可能かどうかを確認するには

1. [**ツール**  >  **] [オプション**]  >  **[環境**] ウィンドウで、[**キーボード**] を選択します。

2. **で [新しいショートカットキーを使用** する (**グローバル**) に設定することを確認します。

3. [ **ショートカットキー** ] ボックスに、使用するキーボードショートカットを入力します。

    ショートカットが Visual Studio で既に使用されている場合、box **で現在使用されているショートカット** には、ショートカットで現在呼び出されているコマンドが表示されます。

4. マップされていないキーが見つかるまで、キーのさまざまな組み合わせを試してみてください。

   > [!NOTE]
   > **Alt** キーを使用するキーボードショートカットでは、メニューを開き、コマンドを直接実行することはできません。 そのため、 **Alt キー** を含むショートカットを入力すると、box **で現在使用されているショートカット** が空白になることがあります。ショートカットでメニューが表示されないことを確認するには、[**オプション**] ダイアログボックスを閉じて、キーを押します。

   次の手順では、既存の VSPackage にメニューコマンドがあることを前提としています。 その方法については、「 [メニューコマンドを使用して拡張機能を作成する」](../extensibility/creating-an-extension-with-a-menu-command.md)を参照してください。

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>コマンドにショートカットキーを割り当てるには

1. パッケージの *vsct* ファイルを開きます。

2. が `<KeyBindings>` `<Commands>` まだ存在しない場合は、の後に空のセクションを作成します。

   > [!WARNING]
   > キーバインドの詳細については、「 [キーバインド](../extensibility/keybinding-element.md)」を参照してください。

    セクションで、 `<KeyBindings>` エントリを作成 `<KeyBinding>` します。

    `guid` `id` 属性と属性を、呼び出すコマンドの属性に設定します。

    属性を `mod1` **Control**、 **Alt**、または **Shift** に設定します。

    キーバインドセクションは次のようになります。

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   キーボードショートカットに3つ以上のキーが必要な場合は、 `mod2` 属性と属性を設定し `key2` ます。

   ほとんどの場合、2番目の修飾子がなければ **Shift** キーを使用しないでください。これを押すと、ほとんどの英数字キーが大文字または記号を入力することになります。

   仮想キーコードを使用すると、関数キーや **Backspace** キーなど、文字が関連付けられていない特殊なキーにアクセスできます。 詳細については、「 [仮想キーコード](/windows/desktop/inputdev/virtual-key-codes)」を参照してください。

   Visual Studio エディターでコマンドを使用できるようにするには、 `editor` 属性をに設定 `guidVSStd97` します。

   カスタムエディターでのみコマンドを使用できるようにするには、 `editor` [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] カスタムエディターを含む VSPackage を作成したときにパッケージテンプレートによって生成されたカスタムエディターの名前に属性を設定します。 名前の値を検索するには、 `<Symbols>` `<GuidSymbol>` `name` 属性が "." で終わるノードのセクションを調べ `editorfactory` ます。これはカスタムエディターの名前です。

## <a name="example-1"></a>例 1
 この例では、  +  + という名前のパッケージで、という名前のコマンドにキーボードショートカットの Ctrl Alt **C** をバインド `cmdidMyCommand` `MyPackage` します。

```
<CommandTable>
. . .
<Commands>
. . .
</Commands>
<KeyBindings>
  <KeyBinding guid="guidMyPackageCmdSet" id="cmdidMyCommand"
      key1="C" mod1="CONTROL" mod2="ALT" editor="guidVSStd97" />
</KeyBindings>
. . .
</CommandTable>
```

## <a name="example-2"></a>例 2
 この例では、  + という名前のプロジェクト内のという名前のコマンドに、キーボードショートカット Ctrl **B** をバインド `cmdidBold` `TestEditor` します。 このコマンドは、カスタムエディターでのみ使用でき、他のエディターでは使用できません。

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>こちらもご覧ください
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
