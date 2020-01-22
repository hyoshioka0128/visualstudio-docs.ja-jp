---
title: Visual Studio 2017 の Live Unit Testing での新機能
titleSuffix: ''
ms.date: 10/11/2017
ms.topic: conceptual
helpviewer_keywords:
- Live Unit Testing
- Live Unit Testing What's New
author: mikejo5000
ms.author: mikejo
ms.workload:
- dotnet
monikerRange: vs-2017
ms.openlocfilehash: 7f7ab0c257bfed4521e95d9da12eaa0b9e25a71e
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114275"
---
# <a name="whats-new-in-live-unit-testing-for-visual-studio-2017"></a>Visual Studio 2017 の Live Unit Testing での新機能

このトピックでは、Visual Studio 2017 バージョン 15.3 以降の Visual Studio の各バージョンの Live Unit Testing に追加された新機能を説明します。 Live Unit Testing の使用方法の詳細については、[Visual Studio での Live Unit Testing](live-unit-testing.md) に関するページを参照してください。

## <a name="version-154"></a>バージョン 15.4

Visual Studio 2017 バージョン 15.4 以降の Live Unit Testing には、さまざまな領域で機能改善があります。

- **検索性の改善**。 Visual Studio IDE では、Live Unit Testing 機能があることを知らないユーザーに、Live Unit Testing が有効になっていないときに単体テストを含むソリューションを開いた場合、Visual Studio IDE に金色のバーを表示します。 金色のバーでは、ユーザーは、Live Unit Testing の機能の詳細とそれを有効にする方法を知ることができます。 Live Unit Testing の前提条件が満たされていない場合についても、金色のバーにはその情報が表示されます。 次の設定があります。

  - テスト アダプターが見つかりません。
  - 古いバージョンのテスト アダプターが存在します。
  - ソリューションで参照されている NuGet パッケージの復元が必要です。

- **タスク センター通知との統合**。 Visual Studio IDE のタスク センターで、Live Unit Testing のバックグラウンド処理通知が表示されるようになりました。これにより、Live Unit Testing が有効になっている場合、何が起こっているのかユーザーが簡単に理解できます。 これにより、大規模なソリューションで Live Unit Testing を開始する際の主要な問題が解決されます。 今までは、カバレッジ アイコンが表示されるまでの数分間、ユーザーは Live Unit Testing が本当に有効になっており、それが動作しているか判断できませんでした。 その問題はもう解消されました。

- **MSTest フレームワーク バージョン 1 のサポート**:Live Unit Testing は、xUnit、NUnit、および MSTest の 3 つの一般的な単体テスト フレームワークで既に動作します。 今まで、Live Unit Testing は MSTest 単体テスト プロジェクトで MS Test バージョン 2 が使用されているときのみ動作していました。 Visual Studio 2017 バージョン 15.4 以降では、MSTest バージョン 1 もサポートするうようになりました。

- **信頼性とパフォーマンス**:Live Unit Testing では、プロジェクトが完全に読み込まれていないとき、Live Unit Testing のクラッシュを回避できるように、システムでそれがより検出されることが保証されるようになりました。 ビルドのパフォーマンスも向上しており、それにより、プロジェクト ファイルで何も変更されていないことをシステムが知っている場合に MSBuild プロジェクトの再評価が行わないようになりました。

- **その他のユーザー インターフェイスの強化**:右クリック ジェスチャのわかりにくい **[Live Test Set – Include/Exclude]\(ライブ テスト セット – 必要/必要なし\)** オプションが **[Live Unit Testing Include/Exclude]\(Live Unit Testing 必要/必要なし\)** に名称が変更されました。 **[テスト]**  >  **[Live Unit Testing]** メニューの **[Reset clean]\(クリーンのリセット\)** オプションが削除されました。 これには、現在、 **[ツール]**  >  **[オプション]**  >  **[Live Unit Testing]** の順に選択し、 **[Delete Persisted Data]\(永続データの削除\)** を選択してアクセスできます。

## <a name="version-153"></a>バージョン 15.3

Visual Studio 2017 バージョン 15.3 以降、Live Unit Testing 機能は、次の 2 つの主要な領域で機能強化されています。

- .NET Core および .NET Standard のサポート。 C# または Visual Basic のいずれかで記述された .NET Core および .NET Standard ソリューションで Live Unit Testing を使用できます。

- パフォーマンスの向上。 はじめて Live Unit Testing でテストを完全ビルドして実行したときは、大幅に高速化したことに驚くでしょう。 その後、同じソリューションで Live Unit Testing をもう一度開始したときも、大幅なパフォーマンスの向上を実感できるはずです。 Live Unit Testing で生成されたデータを永続化し、最新状態チェックでは可能な限りそのデータを再利用するようにしました。

主な変更点に加え、Live Unit Testing には次のような変更点があります。

- テスト メソッドと通常のメソッドを区別するために、新しいビーカー アイコンが使われます。 ビーカーが空の場合、特定のテストが Live Unit Testing に含まれていないことを意味します。

- Live Unit Testing のカバレッジ アイコンのポップアップ UI ウィンドウからテスト メソッドをクリックすると、UI ウィンドウ内でそのコンテキストからテストをデバッグできます。コード エディターを終了する必要がありません。 これは特に、失敗したテストを確認するときに便利です。

- [ツール]/[オプション]/[Live Unit Testing]/[全般] に、構成可能なオプションがいくつか追加されました。 Live Unit Testing に使用されるメモリに上限を設定できます。 オープン ソリューションのために、Live Unit Testing の永続的データのファイル パスも指定できます。

- [テスト]/[Live Unit Testing] のメニュー バーに、メニュー項目がいくつか追加されました。 **[Reset Clean]\(クリーンのリセット\)** は、永続的データを削除して再生成します。 **[オプション]** は、[ツール]/[オプション]/[Live Unit Testing]/[全般] に移動します。

- 次の属性をソース コードに指定することで、対象のテスト メソッドを Live Unit Testing から除外できるようになりました。

  - xUnit の場合: `[Trait("Category", "SkipWhenLiveUnitTesting")]`
  - NUnit の場合: `[Category("SkipWhenLiveUnitTesting")]`
  - MSTest の場合: `[TestCategory("SkipWhenLiveUnitTesting")]`

## <a name="see-also"></a>関連項目

- [Live Unit Testing の概要](live-unit-testing-intro.md)
- [Visual Studio での Live Unit Testing](live-unit-testing.md)
