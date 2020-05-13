---
title: ビジュアルスタジオシェル |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703996"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
シェル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、 の統合の主要な[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エージェントです。 シェルは、VSPackage が共通のサービスを共有できるようにするために必要な機能を提供します。 アーキテクチャの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]目的は、VSPackages の主要な機能をベストにするため、シェルは、基本的な機能を提供し、そのコンポーネント VSPackages 間のクロスコミュニケーションをサポートするフレームワークです。

## <a name="shell-responsibilities"></a>シェルの責任
 シェルには、次の重要な役割があります。

- ユーザー インターフェイス (UI) の基本要素を (COM インターフェイスを介して) サポートします。 これには、既定のメニューとツールバー、ドキュメント ウィンドウ フレームまたはマルチドキュメント インターフェイス (MDI) 子ウィンドウ、ツール ウィンドウ フレーム、およびドッキング サポートが含まれます。

- ドキュメントの永続性を調整し、1 つのドキュメントを複数の方法で開くことができないか、または互換性のない方法で開くことができないことを保証するために、実行中のドキュメント テーブル (RDT) で現在開いているすべてのドキュメントの実行中のリストを維持します。

- コマンド ルーティングおよびコマンド処理インターフェイスをサポート`IOleCommandTarget`する 。

- 適切な時間に VS パッケージを読み込んでいます。 VSPackage の遅延読み込みは、シェルのパフォーマンスを向上させるために必要です。

- 基本的なシェル機能を提供する<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>などの特定の共有サービスの管理<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>、基本的なウィンドウ機能を提供する 、 など。

- ソリューション (.sln) ファイルを管理します。 ソリューションには、Visual C++ 6.0 のワークスペース (.dsw) ファイルと同様に、関連するプロジェクトのグループが含まれています。

- シェル全体の選択、コンテキスト、通貨を追跡します。 シェルは、次の種類の項目を追跡します。

  - 現在のプロジェクト

  - 現在のプロジェクト 項目または現在のアイテム ID<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - [プロパティ] ウィンドウまたは **[プロパティ]** ウィンドウの現在の選択`SelectionContainer`

  - コマンド、メニュー、およびツール バーの表示を制御する UI コンテキスト ID または CmdUIGuid

  - アクティブなウィンドウ、ドキュメント、および元に戻すマネージャーなどの現在アクティブな要素

  - ダイナミック ヘルプを駆動するユーザー コンテキスト属性

  シェルは、インストールされている VSPackages と現在のサービス間の通信も仲介します。 シェルのコア機能をサポートし、 に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合されたすべての VSPackages で使用できるようにします。 これらの主要な機能には、次の項目が含まれます。

- **ダイアログ**ボックスとスプラッシュ画面について

- **[新規項目の追加] ダイアログ ボックスと [既存項目の追加]** ダイアログ ボックス

- **[クラス ビュー** ] ウィンドウと**オブジェクト ブラウザ**

- **[参照設定**] ダイアログ ボックス

- **[ドキュメント アウトライン**] ウィンドウ

- **[ダイナミック ヘルプ**] ウィンドウ

- **検索**と**置換**

- [**新規作成**] メニューの **[プロジェクト**] ダイアログ ボックスと [**ファイルを開く**] ダイアログ ボックス

- **[****ツール**] メニューの [オプション] ダイアログ ボックス

- **[プロパティ]** ウィンドウ

- **ソリューション エクスプローラー**

- **[タスク一覧]** ウィンドウ

- **ツールボックス**

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackages](../../extensibility/internals/vspackages.md)
