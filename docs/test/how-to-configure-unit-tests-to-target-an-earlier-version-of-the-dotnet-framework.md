---
title: .NET Framework の旧バージョンを対象とした単体テスト
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
author: mikejo5000
ms.openlocfilehash: 32380ddc802d1421f39d4920073fc277876cfef4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596022"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>方法: .NET Framework の旧バージョンを対象とした単体テストを構成する

Microsoft Visual Studio でテスト プロジェクトを作成すると、最新バージョンの .NET Framework が対象として既定で設定されます。 また、以前のバージョンの Visual Studio からテスト プロジェクトをアップグレードすると、最新バージョンの .NET Framework を対象とするようにアップグレードされます。 プロジェクト プロパティを編集することによって、以前のバージョンの .NET Framework に対してプロジェクトを明示的に再ターゲットできます。

特定のバージョンの .NET Framework を対象とする単体テスト プロジェクトを作成することができます。 対象とするバージョンは 3.5 以降である必要があり、クライアント バージョンにすることはできません。 Visual Studio では、特定のバージョンを対象とする単体テストに対して次のような基本サポートが可能です。

- 単体テスト プロジェクトを作成して、特定のバージョンの .NET Framework の対象とすることができます。

- ローカル コンピューターの Visual Studio から特定のバージョンの .NET Framework を対象とする単体テストを実行できます。

- コマンド プロンプトから *MSTest.exe* を使用して、特定のバージョンの .NET Framework を対象とする単体テストを実行できます。

- ビルドの一部としてビルド エージェントで単体テストを実行できます。

**テスト用 SharePoint アプリケーション**

上記の機能を使用すると、Visual Studio で SharePoint アプリケーションの単体テストおよび統合テストを記述することもできます。 Visual Studio を使用した SharePoint アプリケーションの開発方法に関する詳細については、「[SharePoint ソリューションの作成](../sharepoint/create-sharepoint-solutions.md)」、「[SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)」、「[SharePoint コードの検証およびデバッグ](../sharepoint/verifying-and-debugging-sharepoint-code.md)」を参照してください。

**制限事項**

テスト プロジェクトを再ターゲットして、以前のバージョンの .NET Framework を使用する場合、次の制限が適用されます。

- .NET Framework 3.5 では、複数バージョン対応は、単体テストのみを含むテスト プロジェクトでサポートされています。 .NET Framework 3.5 は、コード化された UI テストまたはロード テストなど他のテストの種類をサポートしていません。 単体テスト以外のテストの種類では、再ターゲットはブロックされます。

- 以前のバージョンの .NET Framework で対象となっているテストの実行は、既定のホスト アダプターでのみサポートされます。 ASP.NET ホスト アダプターではサポートされていません。 ASP.NET 開発サーバーのコンテキストで実行する必要がある ASP.NET アプリケーションは、現在のバージョンの.NET Framework と互換性がある必要があります。

- .NET Framework 3.5 の複数バージョン対応をサポートしているテストを実行する場合、データ収集サポートは無効になります。 Visual Studio コマンドライン ツールを使用して、コード カバレッジを実行できます。

- .NET Framework 3.5 を使用する単体テストは、リモート コンピューターでは実行できません。

- 以前のクライアント バージョンのフレームワークに対して、単体テストを対象にすることはできません。

## <a name="retargeting-for-visual-basic-unit-test-projects"></a>Visual Basic 単体テスト プロジェクト用の再ターゲット

1. 新しい Visual Basic **単体テスト プロジェクト** プロジェクトを作成します。

2. **ソリューション エクスプローラー**で、新しい Visual Basic テスト プロジェクトの右クリック メニューから **[プロパティ]** を選択します。

     Visual Basic テスト プロジェクトのプロパティが表示されます。

3. 次の図に示すように、 **[コンパイル]** タブで **[詳細コンパイル オプション]** を選択します。

     ![詳細コンパイル オプション](../test/media/howtoconfigureunittest35frameworka.png)

4. 次の図の吹き出し B に示すように、 **[ターゲット フレームワーク (すべての構成)]** ドロップダウン リストを使用して、ターゲット フレームワークを **.NET Framework 3.5** 以降のバージョンに変更します。 クライアント バージョンは指定しません。

     ![[ターゲット フレームワーク] ドロップダウン リスト](../test/media/howtoconfigureunitest35frameworkstepb.png)

## <a name="retargeting-for-c-unit-test-projects"></a>C# 単体テスト プロジェクト用の再ターゲット

1. 新しい C# **単体テスト プロジェクト** プロジェクトを作成します。

2. **ソリューション エクスプローラー**で、新しい C# テスト プロジェクトの右クリック メニューから **[プロパティ]** を選択します。

   C# テスト プロジェクトのプロパティが表示されます。

3. **[アプリケーション]** タブの **[ターゲット フレームワーク]** を選択します。 次の図に示すように、ドロップダウン リストから **[.NET Framework 3.5]** またはそれ以降のバージョンを選択します。 クライアント バージョンは指定しません。

   ![[ターゲット フレームワーク] ドロップダウン リスト](../test/media/howtoconfigureunittest35frameworkcsharp.png)

## <a name="retargeting-for-ccli-unit-test-projects"></a>C++/CLI 単体テスト プロジェクト用の再ターゲット

1. 新しい C++ **単体テスト プロジェクト** プロジェクトを作成します。

   > [!WARNING]
   > Visual C++ に対して以前のバージョンの .NET Framework の C++/CLI 単体テストを作成するには、対応するバージョンの Visual Studio を使用する必要があります。

2. **ソリューション エクスプローラー**で、新しい C++ テスト プロジェクトから **[プロジェクトのアンロード]** を選択します。

3. **ソリューション エクスプローラー**で、アンロードされた C++ テスト プロジェクトを選択して、 **[\<プロジェクト名>.vcxproj の編集]** を選択します。

   エディターで *.vcxproj* ファイルが開きます。

4. `TargetFrameworkVersion` というラベルが付いた `PropertyGroup` で `"Globals"` をバージョン 3.5 以降のバージョンに設定します。 クライアント バージョンは指定しません。

    ```xml
    <PropertyGroup Label="Globals">
        <TargetName>DefaultTest</TargetName>
        <ProjectTypes>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}</ProjectTypes>
        <ProjectGUID>{CE16D77A-E364-4ACD-948B-1EB6218B0EA3}</ProjectGUID>
        <TargetFrameworkVersion>3.5</TargetFrameworkVersion>
        <Keyword>ManagedCProj</Keyword>
        <RootNamespace>CPP_Test</RootNamespace>
      </PropertyGroup>
    ```

5. *.vcxproj* ファイルを保存して閉じます。

6. **ソリューション エクスプローラー**で、新しい C++ テスト プロジェクトの右クリック メニューから **[プロジェクトの再読み込み]** を選択します。

## <a name="see-also"></a>参照

- [SharePoint ソリューションの作成](../sharepoint/create-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [[ビルドの詳細設定] ダイアログ ボックス (Visual Basic)](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)
