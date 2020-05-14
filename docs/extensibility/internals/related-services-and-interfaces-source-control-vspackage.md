---
title: 関連サービスとインターフェイス (ソース管理 VSPackage) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 533f1bf4fcfbaebb25ec10908abf4a46ddacd521
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705629"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>関連サービスとインターフェイス (ソース管理 VSPackage)
このセクションでは、ソース管理 VSPackage 関連のすべてのインターフェイスを[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]示します。 ソース管理 VSPackage は、これらのインターフェイスの一部を実装し、ソース管理タスクを実行するために他のを使用します。

## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>ソース管理 VS パッケージによって実装されるインターフェイスと VS パッケージ用のインターフェイス
 次のインターフェイスは[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]で説明され、ソース管理の VSPackage は、目的の機能セットに応じてそれらのサブセットを実装します。 一部のインターフェイスは必須としてマークされ、すべてのソース管理 VSPackage によって実装する必要があります。

 パッケージが実装していないインターフェイスの場合は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]既定の実装を提供します。 既定の実装は、VSPackage が登録されていない場合にプロジェクトが制御されていない場合に設計されていることに注意してください。 適切に記述されたソース管理 VSPackage は、これらのインターフェイスの既定の実装に残すのではなく、必要なすべてのインターフェイスを実装します。

 ソース管理の VSPackage は、次のインターフェイスの一部またはすべてをカプセル化するプライベート サービスを実装する必要があります。

 インターフェイスは次のとおりです。

- 必須: 適切なエンティティ (ソース管理 VSPackage、ソース管理スタブ、プロジェクト) インターフェイスを実装する必要があります。

- 推奨: エンティティはこのインターフェイスを実装する必要があります。それ以外の場合、ソース管理の機能が制限される可能性があります。

- オプション: エンティティは、このインターフェイスを実装して、より豊富な機能セットを提供できます。

| インターフェイス | 目的 | によって実装される | 実装。 |
| - | - |--------------------------|-------------|
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | エディターは、ファイルを変更または保存する前に、このインターフェイスを呼び出します。 ソース管理の VSPackage は、ファイルをチェックアウトするか、チェックアウトが失敗した場合に操作を拒否できます。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | このインターフェイスは、プロジェクトの基本的なソース管理機能を提供します。 | ソース管理 VS パッケージ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> | この<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>インターフェイスは、<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>関数を使用するか、実装しているオブジェクトを にキャスト`IVsHierarchy`することによって取得`IVsSccProject2`されます。 プロジェクト内のソース管理下にあるファイルを取得したり、プロジェクトに現在のソース管理の状態または場所を通知するために使用されます。 | Project | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> | 統合モジュールは、このインターフェイスを使用して、現在アクティブな VSPackage を設定します。 | ソース管理 VS パッケージ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> | このインターフェイスは、サブスクリプション モデルに基づいています。 VSPackage は、ドキュメント イベントを受信し、発生しようとしているイベントにシェルによって通知されることを通知できます。 によって実装および処理され、VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を実装する`IVsTrackProjectDocumentsEvents2`イベントが渡されます。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | このインターフェイスは、バッチ処理、同期された読み取り/書き`OnQueryAddFiles`込み操作、および高度なメソッドを提供します。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> | **ソリューション エクスプローラー**とプロジェクトは、新しいファイルがプロジェクトに追加されたとき、またはファイルやフォルダーの名前が変更されたり、プロジェクトから削除されたりしたときに、このインターフェイスを呼び出します。 ソース管理 VSPackage プロジェクト ファイルをチェックアウトまたは操作をキャンセルできます。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3> | **ソリューション エクスプローラー**とプロジェクトは、IVstrackProjectDocuments3 インターフェイスのメソッドに対する呼び出しに応答して、このインターフェイスを呼び出します。 ソース管理 VSPackage は、バッチ処理操作を追跡し、読み取り/書き込み`OnQueryAddFiles`操作を同期し、より高度なメソッドを操作できます。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation> | このインターフェイスは、Web プロジェクトの参加管理をサポートします。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip> | このインターフェイスは、プロジェクト内のソース管理されたファイルのツールヒントを取得するために使用されます。 | ソース管理 VS パッケージ | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl> | このインターフェイスは、名前空間拡張をサポートします。 | ソース管理 VS パッケージ | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution> | VSPackage は、このインターフェイスを使用して、名前空間の拡張機能を統合する、**新規作成**、**開く**、または**保存**ダイアログ ボックス。 したがって、プロジェクトは作成時にソース管理に自動的に追加されるか、保存操作が有効な場合はソース管理に追加されます。 | ソース管理 VS パッケージ | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> | VSPackage は、このインターフェイスを使用して **、追加**のグリフをソリューション エクスプローラー のノードのソース管理グリフとして定義します。 | ソース管理 VS パッケージ | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl> | Web プロジェクトの **[追加**] ダイアログ ボックスでは、このインターフェイスが使用されます。 ソース管理の場所を参照し、その場所にあるソース管理リポジトリに以前に追加された Web プロジェクトを開くためのメソッドを提供します。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> | このインターフェイスは、ソース管理からプロジェクトを非同期 (バックグラウンド) 読み込みをサポートします。 | ソース管理 VS パッケージ | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents> | このインターフェイスを使用すると、プロジェクトは、 によって<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>開始された非同期読み込みの進行状況を監視できます。 | Project | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | このインターフェイスを使用すると、IDE はアクティブなソース管理 VSPackage を照会できます。 IDE は、アクティブなソース管理 VSPackage が登録されていない場合でも意味を持つソース管理設定の値を照会します。 このインターフェイスは によって実装され、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]処理されます。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> | このインターフェイスは、ソース管理の VSPackage を登録するときに使用されます。 | ソース管理スタブ | 必須 |
| <xref:EnvDTE.SourceControl> | このインターフェイスはオートメーションで使用されます。 そのため、UI を表示せずに実行できる関数のみを公開します。 | ソース管理 VS パッケージ | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> | このインターフェイスは、ソース管理設定をソリューション (.sln) ファイルに保存するために使用されます。 設定には、ソース管理の場所とソース管理の状態フラグが含まれます。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> | このインターフェイスは、ソース管理の設定をソリューション オプション (.suo) ファイルに保存するために使用されます。 これには、現在のユーザーの参加場所など、ユーザー固有のソース管理設定が含まれる場合があります。 | ソース管理 VS パッケージ | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> | このインターフェイスは、ソリューションを閉じる前にプロジェクト ファイルをチェックインしたり、プロジェクトを開くときにソース管理から新しいファイルを取得したりする操作を実行するためにイベントを監視するために使用されます。 | ソース管理 VS パッケージ | 推奨 |

## <a name="see-also"></a>関連項目
- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
