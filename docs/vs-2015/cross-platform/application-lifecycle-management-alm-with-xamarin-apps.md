---
title: Xamarin アプリを使用したアプリケーション ライフサイクル管理 (ALM) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: ff978cc2-5a25-46d6-921b-e51adaa65992
caps.latest.revision: 16
ms.author: crdun
manager: crdun
ms.openlocfilehash: 1a0ea4f611c5312331fa0e2f2f467b4189778f30
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300028"
---
# <a name="application-lifecycle-management-alm-with-xamarin-apps"></a>Xamarin アプリを使用したアプリケーション ライフサイクル管理 (ALM)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Xamarin では、Android、iOS、および Windows を対象とするクロスプラットフォームのモバイル アプリを、C#、.NET、および Visual Studio を使用して作成することができます。 Xamarin を利用すると、コードの大部分をプラットフォーム間で共有し、プラットフォーム固有にする必要のあるコードをごく一部に抑えることができます。 Xamarin 自体の詳細については、「[Visual Studio と Xamarin](../cross-platform/visual-studio-and-xamarin.md)」を参照してください。  
  
 最新のプラットフォーム向けのアプリ開発には、コードを記述するだけでなく、それ以外の多くのアクティビティが関係します。 これらのアクティビティは、アプリの完全なライフサイクルの中で DevOps (開発 + 運用) 期間になされるものあり、たとえば、作業のアジャイルな計画と追跡、コードの設計と実装、ソース コード リポジトリの管理、ビルドの実行、継続的に実行されるインテグレーションと展開の管理、テスト (単体テストと UI テストを含む)、開発環境と運用環境の両方におけるさまざまな形式の診断の実行、製品利用統計情報と分析によるアプリのパフォーマンスとユーザー動作のリアルタイムな監視などがあります。  
  
 Visual Studio、Visual Studio Team Services、および Team Foundation Server は、さまざまな DevOps 機能 (アプリケーション ライフサイクル管理 (ALM) とも呼ばれる) を提供しています。 これらの多くは、クロスプラットフォームのプロジェクトに完全に適用されます。  
  
 Xamarin アプリでは特にそう言えます。C# と .NET で構築し、いくつかの ALM ツールはそれらを中心に構築されているからです。 その他のツールでは、ビルド環境およびランタイム環境との緊密な統合が必要です。 Xamarin アプリは Windows 以外のプラットフォームでも実行でき、.NET の Mono 実装を使用しているため、Xamarin では特定の必要に合わせて専門ツールが提供されます。  
  
 次の表は、Visual Studio ALM 機能のうち Xamarin プロジェクトで機能するはずの機能と、制限がある機能を示しています。 各機能そのものの詳細については、リンク先のドキュメントを参照してください。  
  
## <a name="agile-tools"></a>アジャイル ツール  
 参照リンク: **[作業](https://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)** (Visual Studio Team Services または TFS (Team Explorer Everywhere など) を使用)  
  
 一般的なコメント: すべての計画機能と追跡機能は、プロジェクトの種類とコーディング言語には依存しません。  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|バックログとスプリントの管理|はい||  
|作業の追跡|はい||  
|チーム ルーム コラボレーション|はい||  
|かんばんボード|はい||  
|進行状況のレポートと視覚化|はい||  
  
## <a name="modeling"></a>モデリング  
 参照リンク: **[アーキテクチャの分析およびモデリング](../modeling/analyze-and-model-your-architecture.md)**  
  
 デザイン機能は、コーディング言語に依存しないか、または C# のような .NET 言語と一緒に機能します。 コードに関連する側面については「[ソフトウェア開発におけるアーキテクチャ図とモデル図の役割](../modeling/scenario-change-your-design-using-visualization-and-modeling.md#ModelingDiagramsTools)」を参照してください。  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|シーケンス図|はい||  
|依存関係グラフ|はい||  
|呼び出し階層|はい||  
|クラス デザイナー|はい||  
|アーキテクチャ エクスプローラー|はい||  
|UML 図 (ユース ケース、アクティビティ、クラス、コンポーネント、シーケンス、および DSL)|はい||  
|レイヤー図|はい||  
|レイヤー検証|はい||  
  
## <a name="code"></a>コード  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|[Team Foundation バージョン管理](https://msdn.microsoft.com/library/1d629052-c65d-4c5d-81eb-eaa4413fe285) または Visual Studio Team Services を使用|はい||  
|[Team Services で Git を使用した作業の開始](https://msdn.microsoft.com/library/32f46ecd-1b03-4ef0-a9c4-8a120da2b03f)|はい||  
|[コードの分析/コードの品質向上 (参照、変更提案など)](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)|はい||  
|[コード変更およびその他の履歴の検索](../ide/find-code-changes-and-other-history-with-codelens.md)|はい|ただし、実行時まで実装が解決しない、プラットフォームに固有の境界をまたぐ場合を除きます。|  
|[コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)|はい||  
  
## <a name="build"></a>ビルド  
 参照リンク: **[ビルド](/azure/devops/pipelines/index)**  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|オンプレミス TFS サーバー|はい|ビルド コンピューターに Xamarin がインストールされている必要があります。iOS 用にビルドするには、OSX コンピューターにリンクできる必要があります。 「 [Xamarin 用に TFS を構成する](https://docs.microsoft.com/azure/devops/repos/tfvc/overview?view=azure-devops) 」(Xamarin web サイト) を参照してください。|  
|Visual Studio Team Services にリンクされたオンプレミスのビルド サーバー|はい|手順については、[ビルド サーバー](https://msdn.microsoft.com/library/2d258a0a-f178-4e93-9da1-eba61151af3c)を参照してください。|  
|Visual Studio Team Services のホスト コントローラー サービス|はい|「[Build your Xamarin app](https://www.visualstudio.com/docs/build/apps/mobile/xamarin)」 (Xamarin アプリのビルド) を参照してください。|  
|事前スクリプトと事後スクリプトによるビルド定義|はい||  
|継続的な統合 (ゲート チェックインを含む)|はい|Git としての TFVC へのゲート チェックインのみ、チェックイン モデルではなく、プル要求モデルで機能します。|  
  
## <a name="testing"></a>Testing (テスト)  
 参照リンク: **[アプリケーションのテスト](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)**  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|テストの計画、テスト ケースの作成、およびテスト スイートの編成|はい||  
|手動テスト|はい||  
|テスト マネージャー (テストの記録と再生)|はい|Windows デバイスと Android エミュレーター (Visual Studio からのみ)。 [Xamarin Test Recorder](https://www.xamarin.com/test-cloud/recorder) を使用すると、すべてのデバイスの記録が可能です。|  
|コード カバレッジ|該当なし||  
|[コードの単体テスト](../test/unit-test-your-code.md)|はい|Windows と Android を対象にする場合は、組み込みの MSTest ツールを使用できます。 Windows、Android、および iOS で単体テストを実行するには、Xamarin では NUnit が推奨されています。 「 [Xamarin 用に TFS を構成する](https://docs.microsoft.com/azure/devops/repos/tfvc/overview?view=azure-devops) 」(Xamarin web サイト) を参照してください。|  
|[UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)|Windows のみ|Visual Studio の UI テスト レコーダーは Windows のみです。 すべてのプラットフォームについては、[Xamarin Test Recorder](https://www.xamarin.com/test-cloud/recorder) を参照してください。|  
  
## <a name="improve-code-quality"></a>コード品質の向上  
 参照リンク: **[コードの品質の向上](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)**  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|[マネージド コードの品質の分析](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|はい||  
|[コード クローン検出を使用した重複コードの検出](https://msdn.microsoft.com/library/a97cd5a6-5ffa-4104-9627-8e59e513654d)|はい||  
|[マネージド コードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|はい||  
|[パフォーマンス エクスプ ローラー](../profiling/performance-explorer.md)|いいえ|代わりに、Xamarin Studio の [Xamarin プロファイラー](https://docs.microsoft.com/xamarin/cross-platform/deploy-test/) を使用します。 Xamarin プロファイラーは現在プレビュー期間中であり、Windows を対象にした場合はまだ動作しないことに注意してください。|  
|[.NET Framework のメモリ分析の問題](../misc/analyze-dotnet-framework-memory-issues.md)|いいえ|Visual Studio ツールには、プロファイリング用の Mono フレームワークへのフックはありません。|  
  
## <a name="release-management"></a>リリース管理  
 参照リンク: **[リリース管理による配置の自動化](https://msdn.microsoft.com/library/vs/alm/release/overview)**  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|リリース プロセスの管理|はい||  
|スクリプトによるサイドローディング用のサーバーへの配置|はい||  
|アプリ ストアへのアップロード|一部|一部のアプリ ストアに対して、このプロセスを自動化することができる拡張機能が使用できます。  たとえば、[Google Play の拡張機能](https://marketplace.visualstudio.com/VSTS)については、[Visual Studio Team Services の拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play)を参照してください。|  
  
## <a name="monitor-with-hockeyapp"></a>HockeyApp による監視  
 参照リンク: **[HockeyApp による監視](https://www.hockeyapp.net/features/)**  
  
|機能|Xamarin でサポートされているかどうか|その他のコメント|  
|-------------|----------------------------|-------------------------|  
|クラッシュ分析、製品利用統計情報、およびベータ版の配布|はい||
