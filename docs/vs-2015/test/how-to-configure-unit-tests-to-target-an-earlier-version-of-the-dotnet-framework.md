---
title: '方法: .NET Framework の旧バージョンを対象とした単体テストを構成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: adb6c011-5abd-41d2-8ead-08cd7579bf37
caps.latest.revision: 14
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fd212eb304e6cba022b067b8b432cf00fc3f87ba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660548"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>方法: .NET Framework の旧バージョンを対象とした単体テストを構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft Visual Studio でテスト プロジェクトを作成すると、最新バージョンの .NET Framework が対象として既定で設定されます。 また、以前のバージョンの Visual Studio からテスト プロジェクトをアップグレードすると、最新バージョンの .NET Framework を対象とするようにアップグレードされます。 プロジェクト プロパティを編集することによって、以前のバージョンの .NET Framework に対してプロジェクトを明示的に再ターゲットできます。

 特定のバージョンの .NET Framework を対象とする単体テスト プロジェクトを作成することができます。 対象とするバージョンは 3.5 以降である必要があり、クライアント バージョンにすることはできません。 Visual Studio では、特定のバージョンを対象とする単体テストに対して次のような基本サポートが可能です。

- 単体テスト プロジェクトを作成して、特定のバージョンの .NET Framework の対象とすることができます。

- ローカル コンピューターの Visual Studio から特定のバージョンの .NET Framework を対象とする単体テストを実行できます。

- コマンド プロンプトから MSTest.exe を使用して、特定のバージョンの .NET Framework を対象とする単体テストを実行できます。

- ビルドの一部としてビルド エージェントで単体テストを実行できます。

  **テスト用 SharePoint アプリケーション**

  上記の機能を使用すると、Visual Studio で SharePoint アプリケーションの単体テストおよび統合テストを記述することもできます。 Visual Studio を使用した SharePoint アプリケーションの開発方法に関する [!INCLUDE[crabout](../includes/crabout-md.md)] は、「[SharePoint ソリューションの作成](https://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)」、「[SharePoint ソリューションのビルドとデバッグ](https://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae)」、および「[SharePoint コードの検証およびデバッグ](https://msdn.microsoft.com/library/b5f3bce2-6a51-41b1-a292-9e384bae420c)」を参照してください。

  **制限事項**

  テスト プロジェクトを再ターゲットして、以前のバージョンの .NET Framework を使用する場合、次の制限が適用されます。

- .NET Framework 3.5 では、複数バージョン対応は、単体テストのみを含むテスト プロジェクトでサポートされています。 .NET Framework 3.5 は、コード化された UI テストまたはロード テストなど他のテストの種類をサポートしていません。 単体テスト以外のテストの種類では、再ターゲットはブロックされます。

- 以前のバージョンの .NET Framework で対象となっているテストの実行は、既定のホスト アダプターでのみサポートされます。 ASP.NET ホスト アダプターではサポートされていません。 ASP.NET 開発サーバーのコンテキストで実行する必要がある ASP.NET アプリケーションは、現在のバージョンの.NET Framework と互換性がある必要があります。

- .NET Framework 3.5 の複数バージョン対応をサポートしているテストを実行する場合、データ収集サポートは無効になります。 Visual Studio コマンドライン ツールを使用して、コード カバレッジを実行できます。

- .NET Framework 3.5 を使用する単体テストは、リモート コンピューターでは実行できません。

- 以前のクライアント バージョンのフレームワークに対して、単体テストを対象にすることはできません。

### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-basic-unit-test-projects"></a>Visual Basic 単体テスト プロジェクト用に特定のバージョンの .NET Framework を再ターゲットする

1. 新しい Visual Basic 単体テスト プロジェクトを作成します。 **[ファイル]** メニューの **[新規作成]** を選択し、**[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **[インストールされているテンプレート]** の **[Visual Basic]** を展開します。 **[テスト]**、**[テスト プロジェクト]** テンプレートの順に選択します。

3. **[名前]** テキスト ボックスに Visual Basic テスト プロジェクトの名前を入力し、**[OK]** をクリックします。

4. ソリューション エクスプローラーで、新しい Visual Basic テスト プロジェクトのショートカット メニューから **[プロパティ]** を選択します。

     Visual Basic テスト プロジェクトのプロパティが表示されます。

5. 次の図に示すように、[ **コンパイル** ] タブで [ **詳細コンパイルオプション** ] を選択します。

     ![詳細コンパイル オプション](../test/media/howtoconfigureunittest35frameworka.png "HowToConfigureUnitTest35FrameworkA")

6. 次の図の吹き出し B に示すように、 **[ターゲット フレームワーク (すべての構成)]** ドロップダウン リストを使用して、ターゲット フレームワークを **.NET Framework 3.5** 以降のバージョンに変更します。 クライアント バージョンは指定しません。

     ![ターゲットフレームワークのドロップダウンリスト&#45;](../test/media/howtoconfigureunitest35frameworkstepb.png "HowToConfigureUniTest35FrameworkStepB")

### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-c-unit-test-projects"></a>Visual C# 単体テスト プロジェクト用に特定のバージョンの .NET Framework を再ターゲットする

1. 新しい Visual C# 単体テスト プロジェクトを作成します。 **[ファイル]** メニューの **[新規作成]** を選択し、**[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **[インストールされているテンプレート]** の **[Visual C#]** を展開します。 **[テスト]**、**[テスト プロジェクト]** テンプレートの順に選択します。

3. **[名前]** テキスト ボックスに Visual C# テスト プロジェクトの名前を入力し、**[OK]** をクリックします。

4. ソリューション エクスプローラーで、新しい Visual C# テスト プロジェクトのショートカット メニューから **[プロパティ]** を選択します。

     Visual C# テスト プロジェクトのプロパティが表示されます。

5. 次の図に示すように、**[アプリケーション]** タブで、**[ターゲット フレームワーク]** を選択し、ドロップダウン リストから **.NET Framework 3.5** 以降のバージョンを選択して、ターゲット フレームワークを変更します。 クライアント バージョンは指定しません。

     ![ターゲットフレームワークのドロップダウンリスト&#45;](../test/media/howtoconfigureunittest35frameworkcsharp.png "HowToConfigureUnitTest35FrameworkCSharp")

### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-ccli-unit-test-projects"></a>C++/CLI 単体テスト プロジェクト用に特定のバージョンの .NET Framework を再ターゲットする

1. 新しい C++ 単体テスト プロジェクトを作成します。 **[ファイル]** メニューで、**[新規作成]** を選択し、**[プロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

    > [!WARNING]
    > Visual C++ に対して以前のバージョンの .NET Framework の C++/CLI 単体テストを作成するには、対応するバージョンの Visual Studio を使用する必要があります。 たとえば、.NET Framework 3.5 を対象とする場合、[!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] と [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] Service Pack 1.をインストールする必要があります。

2. **[インストールされているテンプレート]** の **[Visual C ++]** を展開します。 **[テスト]**、**[テスト プロジェクト]** テンプレートの順に選択します。

3. **[名前]** テキスト ボックスに Visual C++ テスト プロジェクトの名前を入力し、**[OK]** をクリックします。

4. ソリューション エクスプローラーで、新しい Visual C++ テスト プロジェクトから **[プロジェクトのアンロード]** を選択します。

5. ソリューションエクスプローラーで、アンロードされた Visual C++ テストプロジェクトを選択し、[ ** \<project name> .Vcxproj の編集**] を選択します。

     エディターで .vcxproj ファイルが開きます。

6. `"Globals"` というラベルが付いた `PropertyGroup` で `TargetFrameworkVersion` をバージョン 3.5 以降のバージョンに設定します。 クライアント バージョンは指定しません。

    ```
    <PropertyGroup Label="Globals">
        <TargetName>DefaultTest</TargetName>
        <ProjectTypes>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}</ProjectTypes>
        <ProjectGUID>{CE16D77A-E364-4ACD-948B-1EB6218B0EA3}</ProjectGUID>
        <TargetFrameworkVersion>3.5</TargetFrameworkVersion>
        <Keyword>ManagedCProj</Keyword>
        <RootNamespace>CPP_Test</RootNamespace>
      </PropertyGroup>

    ```

7. .vcxproj ファイルを保存して閉じます。

8. ソリューション エクスプローラーで、新しい Visual C++ テスト プロジェクトのショートカット メニューから **[プロジェクトの再読み込み]** を選択します。

## <a name="see-also"></a>参照
 [既存のコードの単体テストを作成して実行](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173)する[sharepoint ソリューションを作成](https://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)[およびデバッグする Sharepoint ソリューションのビルドとデバッグ Sharepoint ソリューションの](https://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae) [[詳細コンパイラの設定] ダイアログボックス (Visual Basic)](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)
