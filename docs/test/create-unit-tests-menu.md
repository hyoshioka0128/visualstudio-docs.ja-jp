---
title: 単体テスト メソッド スタブを作成する
ms.date: 04/24/2020
ms.topic: how-to
helpviewer_keywords:
- unit testing, create unit tests
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5b2712210d4761edb90414e2a27beba74a3bacbf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288664"
---
# <a name="create-unit-test-method-stubs-with-the-create-unit-tests-command"></a>[単体テストの作成] コマンドを使用した単体テスト メソッド スタブの作成

**[単体テストの作成]** コマンドでは、単体テスト メソッド スタブが作成されます。 この機能を使用することで、テスト プロジェクト、テスト クラス、および内部にあるテスト メソッド スタブの構成が容易になります。

::: moniker range="vs-2017"
> [!NOTE]
> **[単体テストの作成]** メニュー コマンドは、.NET Framework を対象とする C# コードに対してのみ使用できます (.NET Core では使用できません)。
::: moniker-end
::: moniker range=">=vs-2019"
> [!NOTE]
> **[単体テストの作成]** メニュー コマンドは、C# コードに対してのみ使用できます。
::: moniker-end

**[単体テストの作成]** メニュー コマンドは拡張可能であり、MSTest、MSTest V2、NUnit、xUnit 用のテストを生成するために使用できます。

## <a name="get-started"></a>作業開始

作業を始めるには、テストするプロジェクトのコード エディターでメソッド、型、または名前空間を選択し、右クリックして、 **[単体テストの作成]** を選択します。 **[単体テストの作成]** ダイアログが開き、テストの作成方法を構成することができます。

![[単体テストの作成] コマンドの使用](media/createunittestcommand.png)

## <a name="set-unit-test-traits"></a>単体テストの特性を設定する

テストの自動化プロセスの一部としてこれらのテストを実行する予定の場合は、他のテスト プロジェクト (上記ダイアログの 2 番目のオプション) でテストを作成し、単体テストにその特徴を設定することを検討してください。 そうすることで、継続的インテグレーションまたは継続的配置パイプラインの一部として、これらの特定のテストを含めたり、除外したりすることがより容易になります。 特徴は、以下に示すように、単体テストに直接メタデータを追加して設定します。

![単体テストの特徴の設定](media/createunittest.png)

## <a name="use-third-party-unit-test-frameworks"></a>サード パーティの単体テスト フレームワークを使用する

NUnit または xUnit 用の単体テストを自動的に生成するには、Visual Studio Marketplace からこれらのテスト フレームワーク拡張機能のいずれかをインストールします。

* [テスト ジェネレーター用 NUnit 拡張機能](https://marketplace.visualstudio.com/items?itemName=NUnitDevelopers.TestGeneratorNUnitextension)
* [テスト ジェネレーター用 xUnit.net 拡張機能](https://marketplace.visualstudio.com/items?itemName=BradWilson.xUnitnetTestExtensions)

## <a name="when-should-i-use-this-feature"></a>この機能を使用するタイミング

この機能は単体テストを作成する必要がある場合は必ず使用しますが、テスト カバレッジが少ないか、存在しておらず、ドキュメントがない既存のコードをテストする場合に特に使用します。 つまり、コード指定が制限されているか存在しない場合です。 コードの監視対象動作の特徴を示す[スマート単体テスト](https://devblogs.microsoft.com/devops/introducing-smart-unit-tests/)に似たアプローチが効果的に実装されます。

ただし、この機能は、開発者がコードを記述し、それを使用して単体テストをブートストラップするときも、同様に適用されます。 コーディングのフロー内で、開発者はコードの特定部分の (テスト クラスとテスト プロジェクトが適切な) 単体テスト メソッド スタブをすばやく作成できます。

## <a name="see-also"></a>関連項目

- ["単体テストの作成" をする単体テスト メソッド スタブの作成](https://devblogs.microsoft.com/devops/creating-unit-test-method-stubs-with-create-unit-tests/)
- [単体テストのブログ投稿](https://devblogs.microsoft.com/devops/?s=unit+testing)
