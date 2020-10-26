---
title: Visual Studio Shell |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fb89fc3b82dc7f142714608d8a669e368216c729
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80703996"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]シェルは、の統合の主要なエージェントです [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 シェルには、Vspackage が共通のサービスを共有できるようにするために必要な機能が用意されています。 のアーキテクチャ目標 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は vspackage の主要機能を提供することであるため、シェルは基本的な機能を提供し、コンポーネント vspackage 間の相互通信をサポートするフレームワークです。

## <a name="shell-responsibilities"></a>シェルの役割
 シェルには、次の主要な役割があります。

- (COM インターフェイスを通じて) ユーザーインターフェイス (UI) の基本要素をサポートします。 これには、既定のメニューとツールバー、ドキュメントウィンドウフレームまたはマルチドキュメントインターフェイス (MDI) 子ウィンドウ、ツールウィンドウフレーム、およびドッキングサポートが含まれます。

- ドキュメントの永続性を調整し、1つのドキュメントを複数の方法で、または互換性のない方法で開くことを保証するために、現在開いているすべてのドキュメントの実行中のリストを実行中のドキュメントテーブル (RDT) で保持する。

- コマンドルーティングとコマンド処理インターフェイスをサポートし `IOleCommandTarget` ます。

- 適切なタイミングで Vspackage を読み込んでいます。 シェルのパフォーマンスを向上させるには、VSPackage の遅延読み込みが必要です。

- 基本的なシェル機能を提供する、などの特定の共有サービスの管理、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> および <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 基本的なウィンドウ機能を提供する。

- ソリューション (.sln) ファイルの管理。 ソリューションには、Visual C++ 6.0 のワークスペース (dsw) ファイルに似た、関連するプロジェクトのグループが含まれています。

- シェル全体の選択、コンテキスト、および通貨を追跡します。 シェルは、次の種類の項目を追跡します。

  - 現在のプロジェクト

  - 現在のプロジェクト項目、または現在のの ItemID <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - [ **プロパティ** ] ウィンドウの現在の選択項目または `SelectionContainer`

  - コマンド、メニュー、およびツールバーの表示を制御する UI コンテキスト Id または CmdUIGuids

  - アクティブウィンドウ、ドキュメント、および元に戻すマネージャーなど、現在アクティブな要素

  - ダイナミックヘルプを駆動するユーザーコンテキスト属性

  シェルは、インストールされている Vspackage と現在のサービス間の通信も仲介します。 シェルのコア機能がサポートされ、に統合されているすべての Vspackage で使用できるようになり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 これらのコア機能には、次の項目が含まれます。

- [**バージョン情報**] ダイアログボックスとスプラッシュスクリーン

- **[新しい項目の追加] ダイアログボックスと [既存項目の追加** ] ダイアログボックス

- **クラスビュー** ウィンドウと **オブジェクトブラウザー**

- [**参照**] ダイアログボックス

- **ドキュメントアウトライン** ウィンドウ

- **ダイナミックヘルプ** ウィンドウ

- **検索** と **置換**

- [**新規**] メニューの [**プロジェクトを開く**] および [**ファイルを開く**] ダイアログボックス

- [**ツール**] メニューの [**オプション**] ダイアログボックス

- **プロパティ** ウィンドウ

- **ソリューション エクスプローラー**

- **タスク一覧** ウィンドウ

- **ツールボックス**

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackages](../../extensibility/internals/vspackages.md)
