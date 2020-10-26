---
title: '方法: を作成するVsct ファイル |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a2483c000bb7c9446ac51bb94ef4006a7b2ac89f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158345"
---
# <a name="how-to-create-a-vsct-file"></a>方法: .Vsct ファイルを作成する
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

XML ベースの Visual Studio コマンドテーブル構成 (vsct) ファイルを作成するには、いくつかの方法があります。  
  
- パッケージテンプレートに新しい VSPackage を作成することができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
- XML ベースのコマンドテーブル構成コンパイラである Vsct.exe を使用すると、既存の ctc ファイルからファイルを生成できます。  
  
- Vsct.exe を使用して、既存の cto ファイルから vsct ファイルを生成することができます。  
  
- 新しい vsct ファイルを手動で作成することができます。  
  
  このトピックでは、新しい vsct ファイルを手動で作成する方法について説明します。  
  
### <a name="to-manually-create-a-new-vsct-file"></a>新しい vsct ファイルを手動で作成するには  
  
1. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]を起動します。  
  
2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[ファイル]** をクリックします。  
  
3. [ **テンプレート** ] ペインで [ **XML ファイル** ] をクリックし、[ **開く**] をクリックします。  
  
4. [ **表示** ] メニューの [ **プロパティウィンドウ** ] をクリックして、XML ファイルのプロパティを表示します。  
  
5. [ **プロパティ** ] ウィンドウで、[スキーマ] プロパティの参照ボタン ([...]) をクリックします。  
  
6. XSD スキーマの一覧で、vsct スキーマを選択します。 一覧に表示されていない場合は、[ **追加** ] をクリックし、ローカルドライブ上のファイルを見つけます。 完了したら [ **OK]** をクリックします。  
  
7. XML ファイルで、「」と入力し、 `<CommandTable` tab キーを押します。 「」と入力してタグを閉じ `>` ます。  
  
     これにより、基本的な vsct ファイルが作成されます。  
  
8. [Vsct スキーマ](../../extensibility/vsct-xml-schema-reference.md)に従って、追加する XML ファイルの要素を入力します。 詳細については、「作成」を参照してください [。Vsct ファイル](../../extensibility/internals/authoring-dot-vsct-files.md)  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 単に vsct ファイルをプロジェクトに追加しても、コンパイルは行われません。 ビルドプロセスに組み込む必要があります。  
  
### <a name="to-add-a-vsct-file-to-project-compilation"></a>プロジェクトのコンパイルに vsct ファイルを追加するには  
  
1. エディターでプロジェクトファイルを開きます。 プロジェクトが読み込まれている場合は、最初にアンロードする必要があります。  
  
2. 次の例に示すように、VSCTCompile 要素を含む [ItemGroup 要素](../../msbuild/itemgroup-element-msbuild.md) を追加します。  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="TopLevelMenu.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
  
    ```  
  
     には、必ずを設定する必要があり `Menus.ctmenu` ます。  
  
3. プロジェクトに .resx ファイルが含まれている場合は、次の例に示すように、MergeWithCTO 要素を含む EmbeddedResource 要素を追加します。  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <ManifestResourceName>VSPackage</ManifestResourceName>  
    </EmbeddedResource>  
  
    ```  
  
     このマークアップは、埋め込まれたリソースを含む ItemGroup 要素内に配置する必要があります。  
  
4. エディターで、通常は *projectname*Package.cs または *projectname*パッケージ .vb という名前のパッケージファイルを開きます。  
  
5. 次の例に示すように、package クラスに "package" リソース属性を追加します。  
  
    ```csharp  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    ```  
  
     最初のパラメーター値は、プロジェクトファイルで定義した、属性の値と一致している必要があります。  
  
## <a name="see-also"></a>参照  
 [文書.Vsct ファイル](../../extensibility/internals/authoring-dot-vsct-files.md)   
 [Visual Studio コマンドテーブル (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [方法: を作成する既存のからの vsct ファイル。Ctc ファイル](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file.md)   
 [方法: を作成する既存のからの vsct ファイル。Cto ファイル](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)   
 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
