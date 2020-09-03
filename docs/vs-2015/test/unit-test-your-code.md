---
title: コードの単体テスト | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, unit tests
- unit tests, verifying code with
- testing code, automated tests
ms.assetid: c191de3e-3f3b-471e-b828-29ec24e80e2c
caps.latest.revision: 64
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7a8b9a4b52fce5fb838c12ccf057fd0e80619cd7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851258"
---
# <a name="unit-test-your-code"></a>コードの単体テスト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

単体テストを実行することにより、開発者およびテスト担当者は、[!INCLUDE[csharp_current_short](../includes/csharp-current-short-md.md)]、[!INCLUDE[vb_current_short](../includes/vb-current-short-md.md)]、および [!INCLUDE[cpp_current_short](../includes/cpp-current-short-md.md)] のプロジェクトでクラスのメソッドに論理エラーがないかどうかをすばやく確認できます。

 単体テスト ツールには次の要素が含まれます。

1. **テストエクスプローラー。** テスト エクスプローラーを使用すると、単体テストを実行して結果を表示することができます。 テスト エクスプローラーは、サードパーティ製のフレームワークを含めて、エクスプローラーのアダプターがあるすべての単体テスト フレームワークを使用できます。

2. **マネージド コード用の Microsoft 単体テスト フレームワーク。** マネージド コード用の Microsoft 単体テスト フレームワークは、Visual Studio と共にインストールされ、.NET コードをテストするためのフレームワークを提供します。

3. **C++ 用の Microsoft 単体テスト フレームワーク。** C++ 用の Microsoft 単体テスト フレームワークは、Visual Studio と共にインストールされ、ネイティブ コードをテストするためのフレームワークを提供します。

4. **コード カバレッジ ツール。** テスト エクスプローラーで、単体テストが 1 つのコマンドから実行する製品コードの量を確認できます。

5. **Microsoft Fakes 分離フレームワーク。** Microsoft Fakes 分離フレームワークによって、テスト対象コード内の依存関係を作成する実稼働コードおよびシステム コード向けの代替クラスおよび代替メソッドを作成できます。 関数の Fake デリゲートを実装して、依存関係オブジェクトの動作と出力を制御します。

   また、[IntelliTest](../test/generate-unit-tests-for-your-code-with-intellitest.md) を使用して .NET コードを確認し、テスト データと単体テストのスイートを生成することもできます。 コードにある各ステートメントについて、そのステートメントを実行するテスト入力が生成されます。 コード内の各条件付き分岐について、ケース分析が実行されます。

## <a name="key-tasks"></a>主なタスク
 単体テストを理解および作成するには、次のトピックを参照してください。

|タスク|関連するトピック|
|-----------|-----------------------|
|**クイック スタートおよびチュートリアル:** 次のトピックでは、Visual Studio での単体テストについてコード例から学習できます。|-   [チュートリアル: マネージド コードに対する単体テストの作成と実行](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)<br />-   [クイックスタート: テストエクスプローラーによるテスト駆動開発](../test/quick-start-test-driven-development-with-test-explorer.md)<br />-   [既存の C++ アプリケーションへの単体テストの追加](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)<br />-   [テストエクスプローラーを使用したネイティブコードの単体テスト](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c)|
|**テスト エクスプローラーによる単体テスト:** テスト エクスプローラーによって、さらに生産性が高く効率的な単体テストを作成できることを学習します。|-   [単体テストの基本](../test/unit-test-basics.md)<br />-   [単体テストプロジェクトを作成する](../test/create-a-unit-test-project.md)<br />-   [テストエクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)<br />-   [サードパーティ製の単体テストフレームワークをインストールする](../test/install-third-party-unit-test-frameworks.md)<br />-   [Visual Studio 2010 からの単体テストのアップグレード](https://msdn.microsoft.com/9bb75856-f68a-4de2-a084-b08a947a1172)|
|**マネージド コードの単体テスト:**|-   [マネージド コード用の Microsoft 単体テスト フレームワークを使用した .NET Framework 用単体テストの記述](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)|
|**C++ コードの単体テスト**|-   [C++ 用の Microsoft 単体テスト フレームワークを使用した C++ 用単体テストの記述](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)|
|**単体テストの分離**|-   [Microsoft フェイクを使用したテストでのコードの分離](../test/isolating-code-under-test-with-microsoft-fakes.md)|
|**コード カバレッジを使用して、単体テストでテストされたプロジェクトのコードの割合を調べる:**[!INCLUDE[vsprvsts](../includes/vsprvsts-md.md)] のテスト ツールのコード カバレッジ機能について学習します。|-   [コードカバレッジを使用してテストされているコードの量を確認する](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)|
|**単体テストにロード テストを使用したストレスおよびパフォーマンスの分析の実行:** ロード テストを作成し、それに単体テストを追加すると、アプリケーションのパフォーマンスおよびストレスの問題を分離するのに役立ちます。 **注:** ロード テストを作成して使用するには、Visual Studio Enterprise が必要です。|-   [ロード テストの作成と編集](https://msdn.microsoft.com/e2985d15-60a7-4177-93b4-f986c2936337)<br />-   [方法: ロード テスト シナリオに、Web パフォーマンス テストと単体テストを追加する](https://msdn.microsoft.com/03cc073e-9bdf-4530-ae46-504a51884594)<br />-   [方法: ロード テスト シナリオから、Web パフォーマンス テストと単体テストを削除する](https://msdn.microsoft.com/3d6128d2-82b0-42fc-bda2-23a8aa03be07)|
|**品質ゲートの設定と適用:** 品質ゲートを作成し、コードがチェックインされる前にテストを実行することで、コードの品質を保証できます。|-   [品質ゲートの設定と適用](https://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)|
|**単体テストの種類の拡張:** 単体テスト フレームワークにはない場合がある機能をテストに追加できます。 たとえば、テストを通常のユーザーとして実行するかどうかを指定するテスト プロパティを追加できます。 また、フレームワークを拡張して、行の属性をメソッドに追加し、テスト内でその行のデータを使用することもできます。|単体テスト フレームワークを拡張する方法のサンプル コードについては、次の [Microsoft Web サイト](https://msdn.microsoft.com/vstudio/ff420671.aspx)を参照してください。|
|**テストのオプションを設定する:** たとえば、テスト結果が格納される場所を指定できます。|[.runsettings ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)|

## <a name="related-tasks"></a>関連タスク
 [Microsoft テスト マネージャーでのテスト結果の確認](https://msdn.microsoft.com/9fb3e429-78df-4fe2-89ed-0ad1db0738f4)

 テスト結果とその扱い方 (テスト結果を表示、保存、発行する方法など) について説明します。

 [Microsoft Visual Studio を使用したシステムテストの実行](https://msdn.microsoft.com/library/19fae5c4-5798-4c4c-b531-3e8f901b1130)

 [!INCLUDE[TCMext](../includes/tcmext-md.md)] を使用するのではなく、Visual Studio を使用して自動テストを実行する方法へのリンクを示します。

## <a name="reference"></a>関連項目
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting> UnitTesting 名前空間について説明します。この名前空間には、単体テストをサポートする属性、例外、アサート、およびその他のクラスが用意されています。

 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Web> Unittesting. Web 名前空間について説明します。この名前空間は、および Web サービスの単体テストのサポートを提供することによって UnitTesting 名前空間を拡張し [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ます。

## <a name="external-resources"></a>外部リソース

### <a name="videos"></a>ビデオ
 [Channel 9: XAML を使用した Windows ストア アプリのビルドの単体テスト](https://channel9.msdn.com/Events/BUILD/BUILD2011/TOOL-529T)

### <a name="forums"></a>フォーラム
 [Visual Studio の単体テスト](https://social.msdn.microsoft.com/Forums/en/vsunittest/threads)

### <a name="guidance"></a>ガイダンス
 [Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 2 章: 単体テスト: 内部のテスト](https://msdn.microsoft.com/library/jj159340.aspx)

### <a name="reference"></a>関連項目
 [単体テストのコンテンツ インデックス](https://blogs.msdn.com/b/mathew_aniyan/archive/2012/05/17/content-index-for-unit-test.aspx)

## <a name="see-also"></a>参照
 [アプリケーションをテストする](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)[コード品質の向上](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)
