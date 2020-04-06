---
title: メニュー項目へのキーボードショートカットのバインド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94feafbc614be61aaa4eef9e26669c0fbe901ed5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740026"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>キーボード ショートカットをメニュー項目にバインドする
カスタム メニュー コマンドにキーボード ショートカットをバインドするには、パッケージの *.vsct*ファイルにエントリを追加するだけです。 このトピックでは、カスタム ボタン、メニュー項目、またはツール バー コマンドにキーボード ショートカットを割り当てる方法と、既定のエディターでキーボード マップを適用する方法、またはカスタム エディターにキーボード マップを適用する方法について説明します。

 既存の Visual Studio メニュー項目にキーボード ショートカットを割り当てるには、「[キーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」を参照してください。

## <a name="choose-a-key-combination"></a>キーの組み合わせを選択する
 多くのキーボード ショートカットは、Visual Studio で既に使用されています。 重複するバインディングは検出が困難であり、予期しない結果が生じる可能性があるため、同じショートカットを複数のコマンドに割り当てないようにしてください。 したがって、割り当てる前にショートカットの可用性を確認することをお勧めします。

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>キーボード ショートカットの使用可能性を確認するには

1. [**ツール** > **オプション** > **環境**] ウィンドウで、[**キーボード**] を選択します。

2. [**新しいショートカットを使用する]** が **[グローバル]** に設定されていることを確認します。

3. [**ショートカット キーを押す**] ボックスに、使用するショートカット キーを入力します。

    ショートカットが Visual Studio で既に使用されている場合、[**ショートカット**] ボックスには、ショートカットが現在呼び出しているコマンドが表示されます。

4. マップされていないキーが見つかるまで、キーの異なる組み合わせを試してください。

   > [!NOTE]
   > **Alt を**使用するキーボード ショートカットはメニューを開き、コマンドを直接実行しないことがあります。 したがって **、Alt**を含むショートカットを入力すると、[**現在使用されている**ショートカット] ボックスが空白になることがあります。ショートカットでメニューが開かないことを確認するには、[**オプション]** ダイアログ ボックスを閉じ、キーを押します。

   次の手順では、メニュー コマンドを使用して既存の VSPackage があることを前提としています。 その場合は、メニュー コマンドを使用して[拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)を参照してください。

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>コマンドにキーボード ショートカットを割り当てるには

1. パッケージの *.vsct*ファイルを開きます。

2. まだ存在しない`<KeyBindings>`場合は、`<Commands>`の後に空のセクションを作成します。

   > [!WARNING]
   > キーバインドの詳細については、「[キーバインド](../extensibility/keybinding-element.md)」を参照してください。

    セクションで`<KeyBindings>`、エントリを作成`<KeyBinding>`します。

    属性と`guid``id`属性を、呼び出すコマンドの属性に設定します。

    属性を`mod1` **[コントロール**]、[ **Alt**] 、または **[Shift]** に設定します。

    KeyBindings セクションは次のようになります。

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   キーボード ショートカットに 3 つ以上のキーが`mod2`必要`key2`な場合は、 および 属性を設定します。

   ほとんどの場合 **、Shift キー**を押すとほとんどの英数字キーが大文字または記号を入力するので、2 番目の修飾子を指定せずに Shift を使用しないでください。

   仮想キー コードを使用すると、ファンクション キーや**バックスペース**キーなど、関連付けられていない特殊キーにアクセスできます。 詳細については、[仮想キー コードを](/windows/desktop/inputdev/virtual-key-codes)参照してください。

   Visual Studio エディターでコマンドを使用できるようにするには、属性を`editor`に`guidVSStd97`設定します。

   コマンドをカスタム エディターでのみ使用できるようにするには、カスタム エディターを`editor`含む VSPackage を作成したときに[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]パッケージ テンプレートによって生成されたカスタム エディターの名前に属性を設定します。 名前の値を見つけるには、`<Symbols>`属性が`<GuidSymbol>``name`" で`editorfactory`終わるノードのセクションを参照してください。これはカスタム エディターの名前です。

## <a name="example"></a>例
 この例では、キーボード ショートカットの**Ctrl**+**Ctrl Alt**+**C**を、 という名前`cmdidMyCommand``MyPackage`のパッケージ内のコマンドにバインドします。

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

## <a name="example"></a>例
 次の使用例は、キーボード ショートカットの**Ctrl**+**B** B`cmdidBold`を、`TestEditor`という名前のプロジェクトのコマンドにバインドします。 このコマンドは、カスタム エディターでのみ使用でき、他のエディターでは使用できません。

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
