---
title: MSTestV2 への更新
description: MSTestV1 から MSTestV2 に更新する方法について説明します
ms.custom: SEO-VS-2020
ms.date: 02/26/2021
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.Migrate
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ffe45c444321a7efbaee0a2eb5729850a06c5910
ms.sourcegitcommit: 99b66b0f4ced46ead0b2506a103f974f40cc0076
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2021
ms.locfileid: "103366269"
---
# <a name="upgrade-from-mstestv1-to-mstestv2"></a>MSTestV1 から MSTestV2 へのアップグレード

テスト プロジェクトをアップグレードするには、 *.csproj* で参照されている MSTest バージョンを MSTestV1 から MSTestV2 に再ターゲットします。 MSTestV1 のすべての機能が MSTestV2 に導入されたわけではないため、エラーを解決するためにいくつかの変更が必要になる場合があります。 機能しなくなった機能については、「[MSTestV2 でサポートされていない MSTestV1 の機能](#mstestv1-features-that-are-not-supported-in-mstestv2)」を参照してください。 これらの一部は、テストから削除する必要がある場合があります。

1. 単体テスト プロジェクトから Microsoft.VisualStudio.QualityTools.UnitTestFramework へのアセンブリ参照を削除します。
2. nuget.org の [MSTest.TestFramework](https://www.nuget.org/packages/MSTest.TestFramework) および [MSTest.TestAdapter](https://www.nuget.org/packages/MSTest.TestAdapter/) のパッケージを含む NuGet パッケージ参照を MSTestV2 に追加します。NuGet パッケージ マネージャー コンソールで、次のコマンドを実行してパッケージをインストールできます。

    ```console
    PM> Install-Package MSTest.TestAdapter -Version 2.1.2
    PM> Install-Package MSTest.TestFramework -Version 2.1.2
    ```

### <a name="old-style-csproj-example"></a>旧スタイルの .csproj の例

MSTestV1 をターゲットとするサンプル *.csproj*:

```xml
<Reference Include="Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
  <Private>False</Private>
</Reference>
```

MSTestV2 をターゲットにするようになったサンプル *.csproj*:

```xml
<Reference Include="Microsoft.VisualStudio.TestPlatform.TestFramework, Version=14.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
  <HintPath>..\packages\MSTest.TestFramework.2.1.2\lib\net45\Microsoft.VisualStudio.TestPlatform.TestFramework.dll</HintPath>
</Reference>
```

> [!NOTE]
> コード化された UI テストまたは Web ロード テストのテスト プロジェクトは、MSTestV2 と互換性がありません。 これらのプロジェクト タイプは非推奨になっています。 詳細については、[コード化された UI テストの非推奨化](https://devblogs.microsoft.com/devops/changes-to-coded-ui-test-in-visual-studio-2019/)と [Web ロード テストの非推奨化](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)に関するページをご覧ください。

### <a name="sdk-style-csproj-net-core-and-net-5"></a>SDK スタイルの .csproj (.NET Core および .NET 5)

*.csproj* が新しい SDK スタイルの *.csproj* の場合、MSTestV2 を既に使用している可能性があります。 [MSTestV2](https://www.nuget.org/packages/MSTest.TestFramework) と [MSTestV2 アダプター](https://www.nuget.org/packages/MSTest.TestAdapter/) の NuGet パッケージは、NuGet で見つけることができます。

例:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="16.7.1" />
  <PackageReference Include="MSTest.TestAdapter" Version="2.1.1" />
  <PackageReference Include="MSTest.TestFramework" Version="2.1.1" />
</ItemGroup>
```

## <a name="why-upgrade-to-mstestv2"></a>MSTestV2 にアップグレードする理由

2016 で、MSTestV2 を使用して MSTest フレームワークを進化させる次のステップをリリースしました。 この変更の詳細については、アナウンスの[ブログ記事](https://devblogs.microsoft.com/devops/taking-the-mstest-framework-forward-with-mstest-v2/)をご覧ください。

* MSTestV2 は [NuGet パッケージ](https://www.nuget.org/packages/MSTest.TestFramework/)として提供されるため、より簡単に取得および更新できます。
* MSTestV2 は[オープン ソース](https://github.com/microsoft/testfx)です。
* 統一されたアプリプラットフォームのサポート – MSTestV2 は、.NET Framework、.NET Core、ASP.NET Core、UWP にわたって一貫したアプリプラットフォーム サポートを提供する統合実装です。 詳細については、[こちら](https://blogs.msdn.microsoft.com/devops/2016/09/01/announcing-mstest-v2-framework-support-for-net-core-1-0-rtm/)を参照してください。
* この実装は完全なクロス プラットフォーム (Windows、Linux、Mac) です。 詳細については、[こちら](https://blogs.msdn.microsoft.com/devops/2017/04/05/mstest-v2-is-open-source/)を参照してください。
* MSTestV2 は、.NET Framework 4.5.0 以降、.NET Core 1.0 以降 (ユニバーサル Windows アプリ 10 以降)、ASP.NET Core 1.0 以降、.NET 5 以降へのターゲット設定をサポートしています。
* 統一された単一のエンドユーザー拡張メカニズムを提供します。 詳細については、[こちら](https://blogs.msdn.microsoft.com/devops/2017/07/18/extending-mstest-v2/)を参照してください。
* すべての MSTest ベースのテスト プロジェクトに対して均一な `DataRow` サポートを提供します。 詳細については、[こちら](https://blogs.msdn.microsoft.com/devops/2017/02/25/mstest-v2-now-and-ahead/)を参照してください。
* クラスまたはアセンブリのレベルに `TestCategory` 属性を配置できるようにします。 詳細については、[こちら](https://blogs.msdn.microsoft.com/devops/2017/02/25/mstest-v2-now-and-ahead/)を参照してください。
* 別のアセンブリで定義されている基底クラスのテスト メソッドが検出され、派生テスト クラスから実行されるようになりました。 この変更により、派生テスト クラスの型との一貫性のある動作が実現されます。 互換性の理由でこの動作が必要ない場合は、次の実行設定を使用して元に戻すことができます。

    ```xml
    <RunSettings>    
    <MSTest> 
      <EnableBaseClassTestMethodsFromOtherAssemblies>false</EnableBaseClassTestMethodsFromOtherAssemblies> 
    </MSTest> 
    </RunSettings>
    ```

* [アセンブリ内でのテストの並列実行](https://github.com/Microsoft/testfx-docs/blob/master/RFCs/004-In-Assembly-Parallel-Execution.md)によって、並列実行をより細かく制御できます。 これにより、アセンブリ内のテストを並行して実行できるようになります。
* `TestClass` の `TestCleanup` メソッドは、対応する `TestInitialize` メソッドが失敗した場合でも呼び出されます。 [問題の詳細情報](https://github.com/Microsoft/testfx/issues/250)。
* `AssemblyInitialize` と `ClassInitialize` にかかった時間は、テスト期間にはカウントされません。 この変更により、テストのタイムアウトへの影響が制限されます。
* 実行不可能なテストは、`.runsettings` ファイルのアダプター ノードの一部である `MapNotRunnableToFailed` タグを使用して、失敗としてマークするように構成できます。

    ```xml
    <RunSettings>    
    <MSTest> 
      <MapNotRunnableToFailed>true</MapNotRunnableToFailed> 
    </MSTest> 
    </RunSettings>
    ```

## <a name="mstestv1-features-that-are-not-supported-in-mstestv2"></a>MSTestV2 でサポートされていない MSTestV1 の機能

*   テストを "順序指定テスト" に含めることはできません。
*   このアダプターでは、 *.testsettings* ファイルを使用した構成はサポートされていません。 テストの実行構成には、新しい [ *.runsettings* ファイル](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)を使用します。
*   アダプターでは、 *.vsmdi* ファイルとして指定されたテスト リストはサポートされていません。
*   "コード化された UI テスト プロジェクト" と "Web パフォーマンスとロード テストのプロジェクト" タイプはサポートされていません。 詳細については、[コード化された UI テストの非推奨化](https://devblogs.microsoft.com/devops/changes-to-coded-ui-test-in-visual-studio-2019/)と [Web ロード テストの非推奨化](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)に関するページをご覧ください。

## <a name="see-also"></a>関連項目

- [`.runsettings` を使用してテストの実行を構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [コードの単体テスト](../test/unit-test-your-code.md)
- [テスト エクスプローラーを使用して単体テストをデバッグする](../test/debug-unit-tests-with-test-explorer.md)
