---
title: 関連サービスとインターフェイス (ソース管理 VSPackage)
titleSuffix: ''
description: Visual Studio SDK のソース管理 VSPackage に関連するインターフェイスについて説明します。 パッケージは、いくつかのインターフェイスを実装し、他のインターフェイスをソース管理に使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3cb7811816c4ad7a7ca6f6f0220f185799ee8b77
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837191"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>関連サービスとインターフェイス (ソース管理 VSPackage)

ここでは、のすべてのソース管理 VSPackage に関連するインターフェイスの一覧を示し [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。 ソース管理 VSPackage は、これらのインターフェイスの一部を実装し、他のインターフェイスを使用してソース管理タスクを実行します。

## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>およびによって実装された、ソース管理 Vspackage のインターフェイス

 次のインターフェイスについては、「」で説明してい [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ます。また、ソース管理 VSPackage は、必要な機能セットに応じてそれらのサブセットを実装します。 一部のインターフェイスは必須としてマークされており、すべてのソース管理 VSPackage によって実装される必要があります。

 パッケージが実装していないインターフェイスの場合、には [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 既定の実装が用意されています。 既定の実装は、VSPackage が登録されておらず、プロジェクトが制御されていない場合に備えて設計されていることに注意してください。 適切に記述されたソース管理 VSPackage は、これらのインターフェイスの既定の実装に残すのではなく、必要なすべてのインターフェイスを実装します。

 ソース管理 VSPackage は、次のインターフェイスの一部またはすべてをカプセル化するプライベートサービスを実装する必要があります。

 インターフェイスは次のとおりです。

- 必須: 適切なエンティティ (ソース管理 VSPackage、ソース管理スタブ、プロジェクト) は、インターフェイスを実装する必要があります。

- 推奨: エンティティは、このインターフェイスを実装する必要があります。それ以外の場合は、ソース管理機能が制限されることがあります。

- 省略可能: エンティティはこのインターフェイスを実装して、より豊富な機能セットを提供できます。

| インターフェイス | 目的 | 実装 | 導入? |
| - | - |--------------------------|-------------|
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | エディターは、ファイルを変更または保存する前に、このインターフェイスを呼び出します。 ソース管理 VSPackage は、チェックアウトに失敗した場合にファイルをチェックアウトしたり、操作を拒否したりできます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | このインターフェイスは、プロジェクトの基本的なソース管理機能を提供します。たとえば、ソース管理を使用したプロジェクトの登録と登録解除や、基本的なソース管理のグリフのサポートなどを行うことができます。 | ソース管理 VSPackage | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> | このインターフェイスは、関数を <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 使用する <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> か、を実装するオブジェクトをにキャストするだけで取得 `IVsHierarchy` `IVsSccProject2` できます。 プロジェクトのソース管理下にあるファイルを取得したり、現在のソース管理の状態または場所をプロジェクトに通知したりするために使用されます。 | Project | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> | 統合モジュールは、このインターフェイスを使用して、現在のアクティブな VSPackage を設定します。 | ソース管理 VSPackage | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> | このインターフェイスは、サブスクリプションモデルに基づいています。 VSPackage は、ドキュメントイベントを受信しようとしていることを通知し、発生しようとしているイベントについてシェルで通知することができます。 これはによって実装および処理され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、さらに、を実装するイベント `IVsTrackProjectDocumentsEvents2` を VSPackage に渡します。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | このインターフェイスは、バッチ処理、同期された読み取り/書き込み操作、および高度なメソッドを提供し `OnQueryAddFiles` ます。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> | **ソリューションエクスプローラー** とプロジェクトは、新しいファイルがプロジェクトに追加されたとき、またはファイルやフォルダーの名前が変更されたり、プロジェクトから削除されたりすると、このインターフェイスを呼び出します。 ソース管理 VSPackage は、プロジェクトファイルをチェックアウトするか、操作を取り消すことができます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3> | **ソリューションエクスプローラー** およびプロジェクトは、IVstrackProjectDocuments3 インターフェイスのメソッドに対する呼び出しに応答してこのインターフェイスを呼び出します。 ソース管理 VSPackage は、バッチ処理された操作、同期された読み取り/書き込み操作を追跡し、より高度なメソッドを操作でき `OnQueryAddFiles` ます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation> | このインターフェイスは、Web プロジェクトの参加管理サポートを提供します。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip> | このインターフェイスは、プロジェクト内のソース管理ファイルのツールヒントを取得するために使用されます。 | ソース管理 VSPackage | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl> | このインターフェイスは、名前空間拡張のサポートを提供します。 | ソース管理 VSPackage | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution> | VSPackage は、このインターフェイスを使用して、名前空間の拡張機能を [ **新規**]、 **[開く**]、[ **保存** ] の各ダイアログボックスに統合します。 その結果、プロジェクトは、作成時にソース管理に自動的に追加されたり、保存操作が有効になったときにソース管理に追加されたりすることができます。 | ソース管理 VSPackage | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> | VSPackage は、このインターフェイスを使用して、 **ソリューションエクスプローラー** のノードのソース管理のグリフとして追加のグリフを定義します。 | ソース管理 VSPackage | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl> | Web プロジェクトの [ **追加** ] ダイアログボックスでは、このインターフェイスを使用します。 ソース管理の場所を参照したり、その場所にあるソース管理リポジトリに以前に追加された Web プロジェクトを開いたりするためのメソッドが用意されています。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> | このインターフェイスでは、ソース管理からのプロジェクトの非同期 (バックグラウンド) 読み込みがサポートされています。 | ソース管理 VSPackage | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents> | このインターフェイスにより、プロジェクトは、によって開始された非同期読み込みの進行状況を監視でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> ます。 | Project | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | このインターフェイスを使用すると、IDE はアクティブなソース管理 VSPackage に対してクエリを実行できます。 IDE は、アクティブなソース管理 VSPackage が登録されていない場合でも、意味のあるソース管理設定の値を照会します。 このインターフェイスは、によって実装および処理され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 | ソース管理スタブ | 必須 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> | このインターフェイスは、ソース管理 VSPackage の登録に使用されます。 | ソース管理スタブ | 必須 |
| <xref:EnvDTE.SourceControl> | このインターフェイスは、オートメーションで使用されます。 そのため、UI を表示せずに実行できる関数のみが公開されます。 | ソース管理 VSPackage | Optional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> | このインターフェイスは、ソース管理の設定をソリューション (.sln) ファイルに保存するために使用されます。 設定には、ソース管理の場所とソース管理の状態フラグが含まれます。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> | このインターフェイスは、ソース管理の設定をソリューションオプション (.suo) ファイルに保存するために使用されます。 これには、現在のユーザーの参加場所など、ユーザー固有のソース管理設定が含まれる場合があります。 | ソース管理 VSPackage | 推奨 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> | このインターフェイスは、ソリューションを閉じる前にプロジェクトファイルのチェックイン、プロジェクトを開くときにソース管理から新しいファイルを取得するなどの操作を実行するために、イベントを監視するために使用されます。 | ソース管理 VSPackage | 推奨 |

## <a name="see-also"></a>関連項目
- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
