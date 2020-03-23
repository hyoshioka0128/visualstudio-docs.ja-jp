---
title: '方法 : を作成するVsct ファイル |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3155ff69db461e652b11ff6e8ec6d405000244f
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301573"
---
# <a name="how-to-create-a-vsct-file"></a>方法 : .vsct ファイルを作成する

XML ベースの Visual Studio コマンド テーブル構成 (*.vsct*) ファイルを作成するには、いくつかの方法があります。

- パッケージ テンプレートに新しい VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を作成できます。

- XML ベースのコマンド テーブル構成コンパイラ*Vsct.exe*を使用して、既存の *.ctc*ファイルからファイルを生成できます。

- *Vsct.exe*を使用して、既存の *.cto*ファイルから *.vsct*ファイルを生成できます。

- 新しい *.vsct*ファイルを手動で作成できます。

  この資料では、新しい *.vsct*ファイルを手動で作成する方法について説明します。

### <a name="to-manually-create-a-new-vsct-file"></a>新しい .vsct ファイルを手動で作成するには

1. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。

3. **[テンプレート] ペイン**で **、[XML ファイル**] をクリックし、[**開く**] をクリックします。

4. [**表示**] メニューの **[プロパティ**] をクリックして、XML ファイルのプロパティを表示します。

5. [**プロパティ]** ウィンドウで、[スキーマ] プロパティの [**参照**] ボタン**を**クリックします。

6. XSD スキーマの一覧で *、vsct.xsd*スキーマを選択します。 一覧にない場合は、[**追加**] をクリックして、ローカル ドライブ上のファイルを探します。 完了したら **、[OK] をクリックします**。

7. XML ファイルに *「コマンド テーブル<」* と入力し **、Tab**キーを押します。タグを閉じるには*>*、「」と入力します。

    この操作により、基本的な *.vsct*ファイルが作成されます。

8. 追加する XML ファイルの要素を[、VSCT XML スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)に従って入力します。 詳細については、「 [.vsct ファイルの作成](../../extensibility/internals/authoring-dot-vsct-files.md)」を参照してください。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>方法 : 既存の .ctc ファイルから .vsct ファイルを作成する

既存のコマンド テーブルの *.ctc*ソース ファイルから XML ベースの *.vsct*ファイルを作成できます。 これにより、新しい XML ベースの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コマンド テーブル (VSCT) コンパイラ形式を利用できます。

### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>.ctc ファイルから .vsct ファイルを作成するには

1. Perl 言語のコピーを取得します。

2. *通常\<、Visual Studio SDK のインストール パス>\VisualStudioIntegration\ツール\bin*フォルダーにある Perl スクリプト*ConvertCTCToVSCT.pl*のコピーを取得します。

3. 変換する *.ctc*ソース ファイルのコピーを取得します。

4. 同じディレクトリにファイルを配置します。

5. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コマンド プロンプト ウィンドウで、ディレクトリに移動します。

6. Type

   ```
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct
   ```

    *ここで、PkgCmd.ctc*は *.ctc*ファイルの名前で *、PkgCmd.vsct*は作成する *.vsct*ファイルの名前です。

    この操作により、新しい *.vsct* XML コマンド テーブル ソース ファイルが作成されます。 *Vsct.exe 、VSCT*コンパイラを使用して、他の *.vsct*ファイルをコンパイルできます。

   > [!NOTE]
   > XML コメントを再フォーマットすることにより *、.vsct*ファイルの読みやすさを向上させることができます。

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>方法 : 既存の .cto ファイルから .vsct ファイルを作成する

既存のバイナリ *.cto*ファイルから XML ベースの *.vsct*ファイルを作成できます。 これを行うことで、新しいコマンド テーブル コンパイラ形式を活用できます。 このプロセスは *、.cto*ファイルが *.ctc*ファイルからコンパイルされた場合でも機能します。 *.vsct*ファイルを編集して、別の .cto ファイルにコンパイルできます。

### <a name="to-create-a-vsct-file-from-a-cto-file"></a>.cto ファイルから .vsct ファイルを作成するには

1. *cto*ファイルとそれに対応する *.ctsym*ファイルのコピーを取得します。

2. *vsct.exe*コンパイラと同じディレクトリにファイルを配置します。

3. Visual Studio のコマンド プロンプトで *、.cto*ファイルと *.ctsym*ファイルが格納されているディレクトリに移動します。

4. Type

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     ここで\<、ctofilename\>は *.cto*ファイルの\<名前\>、vsctfilename は作成する *.vsct*ファイルの名前、\<およびシン\>プファイル名は *.ctsym*ファイルの名前です。

     このプロセスは、新しい *.vsct* XML コマンド テーブル コンパイラ ファイルを作成します。 *vsct.exe 、vsct*コンパイラを使用して、他の *.vsct*ファイルと同様に、ファイルを編集およびコンパイルできます。

## <a name="compile-the-code"></a>コードのコンパイル
 プロジェクトに *.vsct*ファイルを追加するだけでは、コンパイルは行われません。 ビルド プロセスに組み込む必要があります。

### <a name="to-add-a-vsct-file-to-project-compilation"></a>プロジェクトのコンパイルに .vsct ファイルを追加するには

1. エディタでプロジェクトファイルを開きます。 プロジェクトがロードされている場合は、最初にアンロードする必要があります。

2. 次の例に示すように、要素`VSCTCompile`を含む[ItemGroup 要素](../../msbuild/itemgroup-element-msbuild.md)を追加します。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="TopLevelMenu.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>

    ```

     要素`ResourceName`は常に に`Menus.ctmenu`に設定する必要があります。

3. プロジェクトに *.resx*ファイルが含まれている場合`EmbeddedResource`は、次の`MergeWithCTO`例に示すように、要素を含む要素を追加します。

    ```xml
    <EmbeddedResource Include="VSPackage.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <ManifestResourceName>VSPackage</ManifestResourceName>
    </EmbeddedResource>

    ```

     このマークアップは、埋め`ItemGroup`込みリソースを含む要素内に入る必要があります。

4. 通常、*\<プロジェクト名Package.csまたは\>**\<プロジェクト名\>パッケージ.vb*という名前のパッケージ ファイルをエディターで開きます。

5. 次の`ProvideMenuResource`例に示すように、パッケージ クラスに属性を追加します。

    ```csharp
    [ProvideMenuResource("Menus.ctmenu", 1)]
    ```

     最初のパラメーター値は、プロジェクト ファイルで`ResourceName`定義した属性の値と一致する必要があります。

## <a name="see-also"></a>関連項目
- [作成者 .vsct ファイル](../../extensibility/internals/authoring-dot-vsct-files.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)