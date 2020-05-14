---
title: メニュー コマンドのローカライズ |マイクロソフトドキュメント
ms.date: 10/08/2019
ms.topic: conceptual
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d363b495eb84dc3bfeabd7bf7c5d05fabcbc4d36
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702945"
---
# <a name="localize-menu-commands"></a>ローカライズ メニュー コマンド

メニューおよびツール バー コマンドのローカライズされたテキストを提供するには、VSPackage 用にローカライズされた *.vsct*ファイルとローカライズされた *.resx*ファイルを作成し、プロジェクト ファイルを更新して変更を反映します。

インストール エクスペリエンスをローカライズする方法については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="localize-command-names"></a>コマンド名のローカライズ

VSPackages では、メニュー コマンドとツール バー ボタンは *.vsct*ファイルで定義されます。

1. **ソリューション エクスプローラー**で *、.vsct*ファイルの名前を*ファイル名.vsct からファイル名**.en-US.vsct*に変更します。

2. ローカライズされた言語ごとに*ファイル名.en-US.vsct*のコピーを作成します。

    各コピー*のファイル名に名前を付けます。ロケール}.vsct* *、{ロケール}は*特定のカルチャ名です。 カルチャ名の値の一覧については、「 [Microsoft によって割り当てられたロケール ID](/windows/uwp/publish/supported-languages)」を参照してください。

    これらの*ファイル名。Locale.vsct*ファイルには、パッケージのローカライズされたメニュー テキストが含まれます。

3. 各*ファイル名を開きます。テキストをローカライズするためのロケール.vsct*ファイル。

   1. 特定の言語に合わせて[ButtonText](../extensibility/buttontext-element.md)要素の値を変更します。

   2. ローカライズされたアイコンを提供する場合は、[ターゲット](../extensibility/bitmap-element.md)ファイルを指すビットマップ値を変更します。

      次の例は、ファミリー ツリー エクスプローラー ツール ウィンドウを開くコマンドの英語およびスペイン語のボタン テキストを示しています。

      [*ファミリーツリー.en-US.vsct*]

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

    [*FamilyTree.es-ES.vsct*]

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

## <a name="localize-other-text-resources"></a>他のテキスト リソースをローカライズする

コマンド名以外のテキスト リソースは、リソース (*.resx*) ファイルで定義されます。

1. *VSPackage.resx*を*VSPackage.en-US.resx*に名前を変更します。

2. ローカライズされた言語ごとに*VSPackage.en-US.resx*ファイルのコピーを作成します。

     各コピーに*名前を付けます。ロケール}.resx*、{*ロケール}* は特定のカルチャ名です。

3. *リソースの名前を変更します*。 *Resources.en-US.resx*

4. ローカライズされた言語ごとに*Resources.en-US.resx*ファイルのコピーを作成します。

     各コピーに*リソースに名前を付けます。ロケール}.resx*、{*ロケール}* は特定のカルチャ名です。

5. 各 *.resx*ファイルを開いて、特定の言語およびカルチャに合わせて文字列値を変更します。 ツール ウィンドウのタイトル バーのローカライズされたリソース定義を次の例に示します。

     [*リソース.en-US.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Family Tree Explorer</value>
    </data>
    ```

     [*Resources.es-ES.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Explorador del arbol genealogico</value>
    </data>
    ```

## <a name="incorporate-localized-resources-into-the-project"></a>ローカライズされたリソースをプロジェクトに組み込む

ローカライズされたリソースを組み込むには *、assemblyinfo.cs*ファイルとプロジェクト ファイルを変更する必要があります。

1. **ソリューション エクスプローラー**の **[プロパティ]** ノードから、エディターで*assemblyinfo.cs*または*assemblyinfo.vb*を開きます。

2. 次のエントリを追加します。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     これにより、米国英語が既定の言語として設定されます。

3. プロジェクトをアンロードします。

4. エディタでプロジェクト ファイルを開きます。

5. ルート`Project`要素で、既定の`PropertyGroup`言語に一致`UICulture`する要素を持つ要素を追加します。

    ```xml
    <PropertyGroup>
      <UICulture>en-US</UICulture>
    </PropertyGroup>
    ```

     これにより、WINDOWS プレゼンテーション ファンデーション (WPF) コントロールの既定の UI カルチャとして、米国英語が設定されます。

6. 要素を`ItemGroup`含む`EmbeddedResource`要素を見つけます。

7. `EmbeddedResource` *VSPackage.en-US.resx*を呼び出す要素で`ManifestResourceName`、次のように`LogicalName`設定`VSPackage.en-US.Resources`されている要素に置き換えます。

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

8. ローカライズされた言語ごとに、 の`EmbeddedResource``VsPackage.en-US`要素をコピーし、コピーの**Include**属性と**LogicalName**要素をターゲット ロケールに設定します。

9. ローカライズされた`VSCTCompile`各要素に、次`ResourceName`の例に示`Menus.ctmenu`すように、 を指す要素を追加します。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

10. プロジェクト ファイルを保存し、プロジェクトを再読み込みします。

11. プロジェクトをビルドします。

     これにより、メイン アセンブリと、各言語のリソース アセンブリが作成されます。 展開プロセスのローカライズについては[、「VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [アプリケーションのグローバル化とローカライズ](../ide/globalizing-and-localizing-applications.md)
