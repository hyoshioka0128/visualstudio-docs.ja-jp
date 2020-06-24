---
title: サードパーティ製の単体テスト フレームワークをインストールする
ms.date: 04/01/2019
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: fb9a08d0d3119724e8db631841aca35c6c6e9fe5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286974"
---
# <a name="install-unit-test-frameworks"></a>単体テスト フレームワークのインストール

Visual Studio テスト エクスプローラーでは、エクスプローラーに対するアダプター インターフェイスが開発されている任意の単体テスト フレームワークからテストを実行できます。 フレームワークをインストールすると、バイナリがコピーされ、サポートされている言語用の Visual Studio プロジェクト テンプレートが追加されます。 テンプレートを使用してプロジェクトを作成する際、フレームワークはテスト エクスプ ローラーに登録されます。

Visual Studio ソリューションには異なるフレームワークを使用する単体テスト プロジェクトと、異なる言語を対象とした単体テスト プロジェクトを含めることができます。

[MSTest](getting-started-with-unit-testing.md) は Visual Studio で提供されているテスト フレームワークであり、既定でインストールされます。

## <a name="acquire-frameworks"></a>フレームワークを取得する

サード パーティ製の単体テスト フレームワークをインストールするには、**NuGet パッケージ マネージャー**を使用します。

1. テスト コードが含まれているプロジェクトを右クリックして、 **[NuGet パッケージの管理]** を選択します。

2. **NuGet パッケージ マネージャー**で、インストールするテスト フレームワークを検索して、 **[インストール]** をクリックします。

   ![Visual Studio の NuGet パッケージ マネージャー](media/vs-2019/nuget-package-manager.png)

## <a name="update-to-the-latest-test-adapters"></a>最新のテスト アダプターに更新する

テスト検出と実行のエクスペリエンスを向上させるには、最新の安定したテスト アダプターに更新します。 MSTest、NUnit、および xUnit テスト アダプターへの更新の詳細については、[Visual Studio ブログ](https://devblogs.microsoft.com/visualstudio/test-experience-improvements/)を参照してください。

### <a name="to-update-to-the-latest-stable-test-adapter-version"></a>最新の安定したテスト アダプター バージョンに更新するには

1. **[ツール]**  >  **[NuGet Package Manager]**  >  **[Manage NuGet Packages for Solution...]** を選択して、ソリューション用の Nuget Package Manager を開きます。

2. **[更新]** タブをクリックし、インストールされている MSTest、NUnit または xUnit テスト アダプターを検索します。

3. 各テスト アダプターを選択し、ドロップダウン メニューから最新の安定したバージョンを選択します。

4. **[インストール]** ボタンを選択します。

   ![テスト アダプターをアップグレードする](media/install-adapter-upgrade.png)

## <a name="see-also"></a>参照

- [コードの単体テスト](../test/unit-test-your-code.md)
