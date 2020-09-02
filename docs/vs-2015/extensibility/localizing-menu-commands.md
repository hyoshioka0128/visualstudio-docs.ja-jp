---
title: メニューコマンドのローカライズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c879072b55729e249b1aecd665d6f470f4138a75
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686134"
---
# <a name="localizing-menu-commands"></a>メニュー コマンドのローカライズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ローカライズされた vsct ファイルと VSPackage のローカライズされた .resx ファイルを作成し、プロジェクトファイルを更新して変更内容を反映することで、メニューとツールバーのコマンドにローカライズされたテキストを提供できます。  
  
 インストールエクスペリエンスをローカライズする方法の詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。  
  
## <a name="localizing-command-names"></a>コマンド名のローカライズ  
 Vspackage では、メニューコマンドとツールバーボタンは、vsct ファイルで定義されています。  
  
1. **ソリューションエクスプローラー**で、vsct ファイルの名前を*filename*. vsct から*filename*. en-us. vsct に変更します。  
  
2. ローカライズされた言語ごとに、 *ファイル名*. en-us. vsct のコピーを作成します。  
  
    各コピー *ファイル*名に名前を指定します。*Locale*. vsct。ここで、 *locale* は特定のカルチャ名です。 カルチャ名の値の一覧については、「 [Microsoft によって割り当てられたロケール id](https://msdn.microsoft.com/library/windows/apps/jj657969.aspx)」を参照してください。  
  
    これらの *ファイル名*。*ロケール*の vsct ファイルには、パッケージのローカライズされたメニューテキストが含まれます。  
  
3. 各 *ファイル名*を開きます。テキストをローカライズするための*ロケール*の vsct ファイル。  
  
   1. [Buttontext](../extensibility/buttontext-element.md)要素の値を、特定の言語に合わせて変更します。  
  
   2. ローカライズされたアイコンを指定する場合は、ターゲットファイルを指すように [ビットマップ](../extensibility/bitmap-element.md) 値を変更します。  
  
      次の例では、ファミリツリーエクスプローラーのツールウィンドウを開くコマンドの英語とスペイン語のボタンテキストを示しています。  
  
      [FamilyTree。 vsct]  
  
   ```xml  
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">  
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>  
     <Icon guid="guidImages" id="bmpPic2" />  
     <Strings>  
       <CommandName>cmdidFamilyTree</CommandName>  
       <ButtonText>Family Tree Explorer</ButtonText>  
     </Strings>  
   </Button>  
   ```  
  
    [FamilyTree.es。 vsct]  
  
   ```xml  
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">  
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>  
     <Icon guid="guidImages" id="bmpPic2" />  
     <Strings>  
       <CommandName>cmdidFamilyTree</CommandName>  
       <ButtonText>Explorar el arbol genealogico</ButtonText>  
     </Strings>  
   </Button>  
  
   ```  
  
## <a name="localizing-other-text-resources"></a>他のテキストリソースのローカライズ  
 コマンド名以外のテキストリソースは、リソース (.resx) ファイルで定義されています。  
  
1. VSPackage の名前を VSPackage に変更します。  
  
2. ローカライズされた各言語の VSPackage ファイルのコピーを作成します。  
  
     各コピー VSPackage に名前を指定します。*Locale*.resx。ここで、 *locale* は特定のカルチャ名です。  
  
3. リソースの名前を .Resources. en-us. .resx に変更します。  
  
4. 各ローカライズされた言語のリソースのコピーを作成します。  
  
     各コピーリソースに名前を指定します。*Locale*.resx。ここで、 *locale* は特定のカルチャ名です。  
  
5. 各 .resx ファイルを開き、特定の言語とカルチャに合わせて文字列値を変更します。 次の例は、ツールウィンドウのタイトルバーのローカライズされたリソース定義を示しています。  
  
     [Resources. en-us. .resx]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Family Tree Explorer</value>  
    </data>  
    ```  
  
     [Resources.es]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Explorador del arbol genealogico</value>  
    </data>  
  
    ```  
  
## <a name="incorporating-localized-resources-into-the-project"></a>ローカライズされたリソースをプロジェクトに組み込む  
 ローカライズされたリソースを組み込むには、assemblyinfo.cs ファイルとプロジェクトファイルを変更する必要があります。  
  
1. **ソリューションエクスプローラー**の [**プロパティ**] ノードで、エディターの assemblyinfo.cs または assemblyinfo を開きます。  
  
2. 次のエントリを追加します。  
  
    ```csharp  
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]  
    ```  
  
     これにより、既定の言語として英語 (米国) が設定されます。  
  
3. プロジェクトをアンロードします。  
  
4. エディターでプロジェクトファイルを開きます。  
  
5. 要素を `ItemGroup` 含む要素を探し `EmbeddedResource` ます。  
  
6. VSPackage を呼び出す要素で、要素を `EmbeddedResource` 要素に置き換え、次のよう `ManifestResourceName` `LogicalName` にをに設定し `VSPackage.en-US.Resources` ます。  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.en-US.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <LogicalName>VSPackage.en-US.Resources</LogicalName>  
    </EmbeddedResource>  
    ```  
  
7. 次の例に示すように、ローカライズされた言語ごとに、  `EmbeddedResource` VsPackage の要素をコピーし、コピーの **Include** 属性と **logicalname** 要素をターゲットのロケールに設定します。  
  
8. `VSCTCompile` `ResourceName` 次の `Menus.ctmenu` 例に示すように、ローカライズされた各要素に、を指す要素を追加します。  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
    ```  
  
9. プロジェクトファイルを保存し、プロジェクトを再度読み込みます。  
  
10. プロジェクトをビルドします。  
  
     これにより、各言語のメインアセンブリとリソースアセンブリが作成されます。 配置プロセスのローカライズの詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)   
 [MenuCommands と OleMenuCommands](../misc/menucommands-vs-olemenucommands.md)   
 [グローバライズとローカライズ](https://msdn.microsoft.com/library/9a59696b-d89b-45bd-946d-c75da4732d02)
