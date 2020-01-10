---
title: キーボードショートカットをメニュー項目にバインドする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0396d3290ef870fb2c2c7b7b49c774b66397077c
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852213"
---
# <a name="binding-keyboard-shortcuts-to-menu-items"></a>キーボード ショートカットのメニュー項目へのバインド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ショートカットキーをカスタムメニューコマンドにバインドするには、パッケージの vsct ファイルにエントリを追加するだけです。 このトピックでは、キーボードショートカットをカスタムボタン、メニュー項目、またはツールバーコマンドにマップする方法と、キーボードマップを既定のエディターで適用する方法、またはカスタムエディターに制限する方法について説明します。  
  
 既存の Visual Studio のメニュー項目にキーボードショートカットを割り当てるには、「[キーボードショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」を参照してください。  
  
## <a name="choosing-a-key-combination"></a>キーの組み合わせの選択  
 Visual Studio では、多くのキーボードショートカットが既に使用されています。 重複するバインドは検出が困難で、予期しない結果が生じる可能性があるため、複数のコマンドに同じショートカットを割り当てることはできません。 そのため、割り当てる前にショートカットが使用可能かどうかを確認することをお勧めします。  
  
#### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>ショートカットキーが使用可能かどうかを確認するには  
  
1. ツール、オプション、**環境** ウィンドウで、**キーボード** を選択します。  
  
2. **で 新しいショートカットキーを使用**する (**グローバル**) に設定することを確認します。  
  
3. **[ショートカットキー]** ボックスに、使用するキーボードショートカットを入力します。  
  
    ショートカットが Visual Studio で既に使用されている場合、box**で現在使用されているショートカット**には、ショートカットで現在呼び出されているコマンドが表示されます。  
  
4. マップされていないキーが見つかるまで、キーのさまざまな組み合わせを試してみてください。  
  
   > [!NOTE]
   > ALT キーを使用するキーボードショートカットでは、メニューを開き、コマンドを直接実行することはできません。 そのため、ALT キーを含むショートカットを入力すると、box**で現在使用されているショートカット**が空白になることがあります。 ショートカットでメニューが表示されないことを確認するには、 **[オプション]** ダイアログボックスを閉じて、キーを押します。  
  
   次の手順では、既存の VSPackage にメニューコマンドがあることを前提としています。 その方法については、「[メニューコマンドを使用して拡張機能を作成する」](../extensibility/creating-an-extension-with-a-menu-command.md)を参照してください。  
  
#### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>コマンドにショートカットキーを割り当てるには  
  
1. パッケージの vsct ファイルを開きます。  
  
2. `<Commands>` の後に空の `<KeyBindings>` セクションが存在しない場合は作成します。  
  
   > [!WARNING]
   > キーバインドの詳細については、「[キーバインド](../extensibility/keybinding-element.md)」を参照してください。  
  
    [`<KeyBindings>`] セクションで、`<KeyBinding>` エントリを作成します。  
  
    `guid` 属性と `id` 属性を、呼び出すコマンドの属性に設定します。  
  
    `mod1` 属性を**Control**、 **Alt**、または**Shift**に設定します。  
  
    キーバインドセクションは次のようになります。  
  
   ```xml  
   <KeyBindings>  
       <KeyBinding guid="<name of command set>" id="<name of command id>"  
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>  
   </KeyBindings>  
  
   ```  
  
   キーボードショートカットに3つ以上のキーが必要な場合は、`mod2` 属性と `key2` 属性を設定します。  
  
   ほとんどの場合、2番目の修飾子がなければ**Shift**キーを使用しないでください。これを押すと、ほとんどの英数字キーが大文字または記号を入力することになります。  
  
   仮想キーコードを使用すると、関数キーや**BACKSPACE**キーなど、文字が関連付けられていない特殊なキーにアクセスできます。 詳細については、「[仮想キーコード](https://msdn2.microsoft.com/library/ms645540.aspx)」を参照してください。  
  
   Visual Studio エディターでコマンドを使用できるようにするには、`editor` 属性を `guidVSStd97`に設定します。  
  
   このコマンドをカスタムエディターでのみ使用できるようにするには、カスタムエディターを含む VSPackage を作成したときに [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] パッケージテンプレートによって生成されたカスタムエディターの名前に `editor` 属性を設定します。 名前の値を確認するには、`name` 属性が "`editorfactory`" で終わる `<GuidSymbol>` ノードの `<Symbols>` セクションを調べます。これはカスタムエディターの名前です。  
  
## <a name="example"></a>使用例  
 この例では、キーボードショートカットの CTRL + ALT + C キーを `MyPackage`という名前のパッケージ内の `cmdidMyCommand` という名前のコマンドにバインドします。  
  
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
  
## <a name="example"></a>使用例  
 この例では、`TestEditor`という名前のプロジェクト内の `cmdidBold` という名前のコマンドに、キーボードショートカットの CTL + B をバインドします。 このコマンドは、カスタムエディターでのみ使用でき、他のエディターでは使用できません。  
  
```xml  
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />  
```  
  
## <a name="see-also"></a>参照  
 [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
