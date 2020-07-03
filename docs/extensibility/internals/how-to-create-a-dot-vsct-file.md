---
title: '方法: を作成するVsct ファイル |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a571098deeeca0e8262d855c24d0bf1ce66be08e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905534"
---
# <a name="how-to-create-a-vsct-file"></a>方法: vsct ファイルを作成する

XML ベースの Visual Studio コマンドテーブル構成 (*vsct*) ファイルを作成するには、いくつかの方法があります。

- パッケージテンプレートに新しい VSPackage を作成することができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- XML ベースのコマンドテーブル構成コンパイラである*Vsct.exe*を使用すると、既存の*ctc*ファイルからファイルを生成できます。

- *Vsct.exe*を使用して、既存の*cto*ファイルから*vsct*ファイルを生成することができます。

- 新しい*vsct*ファイルを手動で作成することができます。

  この記事では、新しい*vsct*ファイルを手動で作成する方法について説明します。

### <a name="to-manually-create-a-new-vsct-file"></a>新しい vsct ファイルを手動で作成するには

1. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。

3. [**テンプレート**] ペインで [ **XML ファイル**] をクリックし、[**開く**] をクリックします。

4. [**表示**] メニューの [**プロパティ**] をクリックして、XML ファイルのプロパティを表示します。

5. [**プロパティ**] ウィンドウで、[**スキーマ**] プロパティの [**参照**] ボタンをクリックします。

6. XSD スキーマの一覧で、 *vsct*スキーマを選択します。 一覧に表示されていない場合は、[**追加**] をクリックし、ローカルドライブ上のファイルを見つけます。 完了したら [ **OK]** をクリックします。

7. XML ファイルに*CommandTable<* 入力し、 **tab**キーを押します。「」と入力してタグを閉じ *>* ます。

    この操作により、基本的な*vsct*ファイルが作成されます。

8. [Vsct xml スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)に従って、追加する xml ファイルの要素を入力します。 詳細については、「[作成した vsct ファイル](../../extensibility/internals/authoring-dot-vsct-files.md)」を参照してください。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>方法: 既存の ctc ファイルから vsct ファイルを作成する

既存のコマンドテーブルから XML ベース*の vsct*ファイルを作成できます *。 ctc*ソースファイル。 これにより、新しい XML ベースの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンド テーブル (VSCT) コンパイラ形式を利用できます。

### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>.ctc ファイルから .vsct ファイルを作成するには

1. Perl 言語のコピーを取得します。

2. Perl スクリプト*ConvertCTCToVSCT.pl*のコピーを取得します (通常は* \<Visual Studio SDK installation path> \VisualStudioIntegration\Tools\bin*フォルダーにあります)。

3. 変換する*ctc*ソースファイルのコピーを取得します。

4. 同じディレクトリにファイルを配置します。

5. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コマンドプロンプトウィンドウで、ディレクトリに移動します。

6. 型

   ```
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct
   ```

    ここで、 *Pkgcmd. ctc*は、 *Ctc*ファイルと pkgcmd の名前です *。 vsct*は、作成する*vsct*ファイルの名前です。

    この操作により、新しい*vsct* XML コマンドテーブルソースファイルが作成されます。 他の*vsct*ファイルと同様に、vsct コンパイラの*Vsct.exe*を使用して、ファイルをコンパイルできます。

   > [!NOTE]
   > XML コメントを再フォーマットすることにより、 *vsct*ファイルの読みやすさを向上させることができます。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>方法: 既存の cto ファイルから vsct ファイルを作成する

既存のバイナリ *. cto*ファイルから XML ベース*の vsct*ファイルを作成できます。 これを行うことで、新しいコマンド テーブル コンパイラ形式を活用できます。 このプロセスは、 *cto*ファイルが*ctc*ファイルからコンパイルされている場合でも機能します。 この*vsct*ファイルは、別の cto ファイルに編集してコンパイルできます。

### <a name="to-create-a-vsct-file-from-a-cto-file"></a>.cto ファイルから .vsct ファイルを作成するには

1. *Cto*ファイルとそれに対応する*ctsym*ファイルのコピーを取得します。

2. ファイルを*vsct.exe*コンパイラと同じディレクトリに配置します。

3. Visual Studio のコマンドプロンプトで、 *cto*ファイルと*ctsym*ファイルが格納されているディレクトリにアクセスします。

4. 型

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     ここで \<ctofilename\> 、は、 *cto*ファイルの名前です。は、 \<vsctfilename\> 作成する*vsct*ファイルの名前です。は、このファイル \<symfilename\> の *.ctsym*名前です。

     このプロセスでは、新しい*vsct* XML コマンドテーブルコンパイラファイルが作成されます。 他の *.vsct*ファイルと同様に、.vsct コンパイラの*vsct.exe*を使用して、ファイルを編集およびコンパイルできます。

## <a name="compile-the-code"></a>コードのコンパイル
 単に*vsct*ファイルをプロジェクトに追加しても、コンパイルは行われません。 ビルドプロセスに組み込む必要があります。

### <a name="to-add-a-vsct-file-to-project-compilation"></a>プロジェクトのコンパイルに vsct ファイルを追加するには

1. エディターでプロジェクトファイルを開きます。 プロジェクトが読み込まれている場合は、最初にアンロードする必要があります。

2. 次の例に示すように、要素を含む[ItemGroup 要素](../../msbuild/itemgroup-element-msbuild.md)を追加し `VSCTCompile` ます。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="TopLevelMenu.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>

    ```

     `ResourceName`要素は常にに設定する必要があり `Menus.ctmenu` ます。

3. プロジェクトに *.resx*ファイルが含まれている場合は、 `EmbeddedResource` 次の `MergeWithCTO` 例に示すように、要素を含む要素を追加します。

    ```xml
    <EmbeddedResource Include="VSPackage.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <ManifestResourceName>VSPackage</ManifestResourceName>
    </EmbeddedResource>

    ```

     このマークアップは、 `ItemGroup` 埋め込まれたリソースを含む要素内に配置する必要があります。

4. エディターで、通常は* \<ProjectName\> Package.cs*または* \<ProjectName\> .vb*という名前のパッケージファイルを開きます。

5. 次の `ProvideMenuResource` 例に示すように、属性を package クラスに追加します。

    ```csharp
    [ProvideMenuResource("Menus.ctmenu", 1)]
    ```

     最初のパラメーター値は、 `ResourceName` プロジェクトファイルで定義した属性の値と一致する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [作成した vsct ファイル](../../extensibility/internals/authoring-dot-vsct-files.md)
- [Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)
