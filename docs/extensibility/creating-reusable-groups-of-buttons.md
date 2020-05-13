---
title: ボタンの再利用可能なグループを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddfba6701890f73ce6438ddc03a338912841a37d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739466"
---
# <a name="create-reusable-groups-of-buttons"></a>再利用可能なボタンのグループを作成する
コマンド グループは、メニューまたはツールバーに常に一緒に表示されるコマンドのコレクションです。 任意のコマンド グループを使用するには *、.vsct*ファイルの CommandPlacements セクション内の別の親メニューに割り当てます。

 コマンド グループには通常ボタンが含まれますが、他のメニューやコンボ ボックスを含めることもできます。

## <a name="to-create-a-reusable-group-of-buttons"></a>再利用可能なボタンのグループを作成するには

1. という名前`ReusableButtons`の VSIX プロジェクトを作成します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. プロジェクトが開いたら、**再利用可能**なコマンドという名前のカスタム コマンド項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログで **、[Visual C#** > **の機能拡張**] に移動し、[**カスタム コマンド**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を*ReusableCommand.cs*に変更します。

3. *vsct*ファイルで、シンボル セクションに移動し、プロジェクトのグループとコマンドを含む GuidSymbol 要素を見つけます。 名前を付ける必要があります。

4. 次の例に示すように、グループに追加する各ボタンに IDSymbol を追加します。

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     既定では、コマンド項目テンプレートは **、MyMenuGroup**という名前のグループと、指定した名前のボタンと、それぞれに対する IDSymbol エントリを作成します。

5. [グループ] セクションで、シンボル セクションで指定したものと同じ GUID と ID 属性を持つグループ要素を作成します。 次の例のように、既存のグループを使用することも、コマンド テンプレートによって提供されるエントリを使用することもできます。 このグループは **、[ツール]** メニューに表示されます。

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>再利用するボタンのグループを作成するには

1. コマンドまたはメニューは、コマンドまたはメニューの定義で親として使用するか、CommandPlacements セクションを使用してグループ内にコマンドまたはメニューを配置することによって、グループに配置できます。

     [ボタン] セクションで、グループを親として持つボタンを定義するか、次の例に示すように、パッケージ テンプレートによって提供されるボタンを使用します。

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2. ボタンを複数のグループに表示する必要がある場合は、コマンドセクションの後に配置する必要がある CommandPlacements セクションに、そのボタンのエントリを作成します。 次の例に示すように、配置するボタンの GUID と ID 属性を設定し、その Parent 要素の GUID と ID をターゲット グループの GUID と ID に設定します。

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    > 「優先順位」フィールドの値によって、新規コマンド・グループ内のコマンドの位置が決まります。 CommandPlacement 要素で設定された優先順位は、項目定義で設定された優先順位よりも優先されます。 優先順位値が低いコマンドは、優先順位値が高いコマンドの前に表示されます。 重複した優先順位値は許可されますが **、devenv /setup**コマンドがレジストリから最終的なインターフェイスを作成する順序が一貫していない可能性があるため、同じ優先順位値を持つコマンドの相対位置は保証されません。

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>再利用可能なボタンのグループをメニューに配置するには

1. セクションにエントリを`CommandPlacements`作成します。 要素の GUID と`CommandPlacement`ID をグループの GUID と ID に設定し、親の GUID と ID をターゲットの場所の親の GUID と ID に設定します。

    コマンド配置セクションは、コマンド セクションの直後に配置する必要があります。

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    コマンド グループは、複数のメニューに含めることができます。 親メニューは、作成したもの、または *(ShellCmdDef.vsct または SharedCmdDef.vsct* *SharedCmdDef.vsct*で説明されているように) によって[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]提供されるメニュー、または別の VSPackage で定義されているメニューにすることができます。 親メニューが最終的に VSPackage によって表示されるショートカット メニューに[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]接続されている限り、親レイヤーの数は無制限です。

    次の例では、他のボタンの右側にある**ソリューション エクスプローラー**のツール バーにグループを配置します。

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
