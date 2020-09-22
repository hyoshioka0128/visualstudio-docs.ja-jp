---
title: 再利用可能なボタンのグループの作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
caps.latest.revision: 45
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6ac1fd0dc242ae8b8979a3f420f5e1c4d837f62b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841988"
---
# <a name="creating-reusable-groups-of-buttons"></a>再利用可能なボタンのグループの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コマンドグループは、メニューまたはツールバーに常に一緒に表示されるコマンドのコレクションです。 任意のコマンドグループは、vsct ファイルの CommandPlacements セクションの別の親メニューに割り当てて再利用できます。  
  
 通常、コマンドグループにはボタンが含まれていますが、他のメニューやコンボボックスを含めることもできます。  
  
### <a name="to-create-a-reusable-group-of-buttons"></a>再利用可能なボタンのグループを作成するには  
  
1. という名前の VSIX プロジェクトを作成 `ReusableButtons` します。 詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. プロジェクトが開いたら、 **Reusablecommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **ReusableCommand.cs**に変更します。  
  
3. . Vsct ファイルで、[シンボル] セクションにアクセスし、プロジェクトのグループとコマンドを含む GuidSymbol 要素を見つけます。 GuidReusableCommandPackageCmdSet という名前にする必要があります。  
  
4. 次の例に示すように、グループに追加する各ボタンの IDSymbol を追加します。  
  
    ```xml  
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">  
        <IDSymbol name="MyMenuGroup" value="0x1020" />  
        <IDSymbol name="ReusableCommandId" value="0x0100" />  
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />  
    </GuidSymbol>  
    ```  
  
     既定では、コマンド項目テンプレートによって、 **Mygroup** という名前のグループと、指定した名前を持つボタンと、それぞれの idsymbol エントリが作成されます。  
  
5. [Groups] セクションで、[Symbols] セクションで指定したものと同じ GUID 属性と ID 属性を持つ Group 要素を作成します。 また、次の例に示すように、既存のグループを使用するか、コマンドテンプレートによって提供されるエントリを使用することもできます。 このグループは、[ **ツール** ] メニューに表示されます。  
  
    ```xml  
    <Groups>  
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">  
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>  
        </Group>  
    </Groups>  
    ```  
  
### <a name="to-create-a-group-of-buttons-for-reuse"></a>再利用するためのボタンのグループを作成するには  
  
1. コマンドまたはメニューをグループに含めるには、そのグループをコマンドまたはメニューの定義で親として使用するか、コマンドまたはメニューを [CommandPlacements] セクションを使用してグループに配置します。  
  
     [ボタン] セクションで、次の例に示すように、グループを親として持つボタンを定義するか、パッケージテンプレートによって提供されるボタンを使用します。  
  
    ```xml  
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">  
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>Invoke ReusableCommand</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
2. 1つのボタンを複数のグループに表示する必要がある場合は、コマンドセクションの後に配置する必要がある CommandPlacements セクションにそのエントリを作成します。 次の例に示すように、CommandPlacement 要素の GUID 属性と ID 属性を、配置するボタンと一致するように設定してから、その親要素の GUID と ID をターゲットグループの GUID と ID に設定します。  
  
    ```xml  
    <CommandPlacements>  
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">  
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />  
        </CommandPlacement>  
    </CommandPlacements>  
    ```  
  
    > [!NOTE]
    > Priority フィールドの値によって、新しいコマンドグループ内のコマンドの位置が決まります。 CommandPlacement 要素で設定された優先順位は、項目定義のセットをオーバーライドします。 優先順位値が低いコマンドは、優先順位値が高いコマンドの前に表示されます。 優先順位値の重複は許可されていますが、 **devenv/setup** コマンドがレジストリから最終的なインターフェイスを作成する順序に一貫性がないため、同じ優先順位値を持つコマンドの相対的な位置は保証できません。  
  
### <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>メニューに再利用可能なボタンのグループを配置するには  
  
1. セクションにエントリを作成 `CommandPlacements` します。 要素の GUID と ID をグループの GUID と ID に設定 `CommandPlacement` し、親の guid と id をターゲットの場所のものに設定します。  
  
     CommandPlacements セクションは、Commands セクションの直後に配置する必要があります。  
  
    ```xml  
    <CommandTable>  
    ...  
      <Commands>... </Commands>  
      <CommandPlacements>... </CommandPlacements>  
    ...   
    </CommandTable>  
    ```  
  
     コマンドグループは、複数のメニューに含めることができます。 親メニューは、作成したものにすることができます。これは、によって提供されるもの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (shellcmddef. vsct または SharedCmdDef. vsct で説明)、または別の VSPackage で定義されているものです。 親メニューが最終的に [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] VSPackage によって表示されるショートカットメニューに接続されている限り、親レイヤーの数は無制限です。  
  
     次の例では、グループを [ **ソリューションエクスプローラー** ] ツールバーの他のボタンの右側に配置します。  
  
    ```xml  
    <CommandPlacements>  
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0xF00">  
          <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>  
        </CommandPlacement>  
    </CommandPlacements>  
    ```  
  
    ```xml  
    <CommandPlacements>  
      <CommandPlacement guid="guidButtonGroupCmdSet" id="MyMenuGroup"   
          priority="0x605">  
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS" />  
      </CommandPlacement>  
    </CommandPlacements>  
  
    ```
