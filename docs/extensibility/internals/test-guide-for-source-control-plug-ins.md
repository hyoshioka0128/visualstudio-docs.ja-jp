---
title: ソース管理プラグインのテストガイド |Microsoft Docs
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- plug-ins, source control
- source control [Visual Studio SDK], testing plug-ins
- tests, source control plug-ins
- testing, source control plug-ins
- source control plug-ins, test guide
ms.assetid: 13b74765-0b7c-418e-8cd9-5f2e8db51ae5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 321d61175068f135aae87bff73f13ac800f4793c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905159"
---
# <a name="test-guide-for-source-control-plug-ins"></a>ソース管理プラグイン向けのテスト ガイド
このセクションでは、を使用したソース管理プラグインのテストに関するガイダンスを提供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 最も一般的なテスト領域の概要と、問題がある可能性がある複雑な領域の一部を紹介します。 この概要は、テストケースの完全な一覧ではありません。

> [!NOTE]
> 以前 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンのを使用しているときに以前に検出されなかった既存のソース管理プラグインに関する問題は、最新の IDE のバグ修正および機能強化によって発見される可能性があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 以前のバージョンの以降、プラグインに変更が加えられていない場合でも、このセクションで列挙されている領域については、既存のソース管理プラグインをテストすることを強くお勧めし [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="common-preparation"></a>一般的な準備
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]とターゲットソース管理プラグインがインストールされているコンピューターが必要です。 同様に構成された2つ目のコンピューターは、オープンソース管理テストの一部で使用できます。

## <a name="definition-of-terms"></a>用語の定義
 このテストガイドでは、次の用語定義を使用します。

 クライアントプロジェクトソース管理の統合をサポートするで使用できるプロジェクトの種類 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ( [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 、、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] またはなど [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] )。

 Web プロジェクトには、ファイルシステム、ローカル IIS、リモートサイト、FTP の4種類の Web プロジェクトがあります。

- ファイルシステムプロジェクトはローカルパスに作成されますが、UNC パスを使用して内部でアクセスされるため、インターネットインフォメーションサービス (IIS) をインストールする必要はありません。また、クライアントプロジェクトと同様に、IDE 内からソース管理下に配置することもできます。

- ローカル IIS プロジェクトは、同じコンピューターにインストールされ、ローカルコンピューターを指す URL を使用してアクセスされる IIS で動作します。

- リモートサイトプロジェクトは IIS サービスでも作成されますが、IDE 内からではなく、IIS サーバーコンピューターのソース管理下に配置され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- FTP プロジェクトはリモート FTP サーバーを介してアクセスされますが、ソース管理下に配置することはできません。

  ソース管理下にあるソリューションまたはプロジェクトに対するもう1つの用語。

  バージョンストアソース管理プラグイン API を使用してアクセスされているソース管理データベース。

## <a name="test-areas-covered-in-this-section"></a>このセクションで説明されているテスト領域

- [テスト領域 1: ソース管理に追加/オープンする](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - ケース 1a: ソース管理にソリューションを追加する

  - ケース 1b: ソース管理からソリューションを開く

  - ケース 1c: ソース管理からソリューションを追加する

- [テスト領域 2: ソース管理からの取得](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [テスト領域 3: チェックアウト/チェックアウトの取り消し](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - ケース 3: チェックアウト/チェックアウトの取り消し

  - ケース 3a: チェックアウト

  - ケース 3b: 切断されたチェックアウト

  - ケース 3c: クエリの編集/クエリの保存 (QEQS)

  - ケース 3d: サイレントチェックアウト

  - ケース 3e: チェックアウトを元に戻す

- [テスト領域 4: チェックイン](../../extensibility/internals/test-area-4-check-in.md)

  - ケース 4a: 変更された項目

  - ケース 4b: ファイルの追加

  - ケース 4c: プロジェクトの追加

- [テスト領域 5: ソース管理の変更](../../extensibility/internals/test-area-5-change-source-control.md)

  - ケース 5a: バインド

  - ケース 5b: バインド解除

  - ケース 5c: 再バインド

- [テスト領域 6: 削除](../../extensibility/internals/test-area-6-delete.md)

- [テスト領域 7: 共有](../../extensibility/internals/test-area-7-share.md)

- [テスト領域 8: プラグインの切り替え](../../extensibility/internals/test-area-8-plug-in-switching.md)

  - ケース 8a: 自動変更

  - Case 8b: ソリューションベースの変更

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
