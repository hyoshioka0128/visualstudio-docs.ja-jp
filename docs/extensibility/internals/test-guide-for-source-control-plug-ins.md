---
title: ソース管理プラグインのテスト ガイド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: e6b3f8e76e977472a3459697a650b32dae657c22
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704374"
---
# <a name="test-guide-for-source-control-plug-ins"></a>ソース管理プラグイン向けのテスト ガイド
このセクションでは、 を使用してソース管理プラグインをテスト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]するためのガイダンスを提供します。 最も一般的なテスト領域の広範な概要と、問題のあるより複雑な領域が提供されています。 この概要は、テスト ケースの完全なリストではありません。

> [!NOTE]
> 最新[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の IDE に対するバグ修正と改良により、以前のバージョンの を使用している間に以前には発生しなかった既存のソース管理[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プラグインの問題が明らかになる場合があります。 以前のバージョン以降にプラグインに変更が加えていなくても、このセクションで列挙した領域に対して既存の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理プラグインをテストすることを強くお勧めします。

## <a name="common-preparation"></a>共通の準備
 インストールされているターゲット[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理プラグインを持つコンピューターが必要です。 同様に構成された 2 台目のコンピューターは、一部のソース管理から開くテストに使用できます。

## <a name="definition-of-terms"></a>用語の定義
 このテスト ガイドの目的で、次の用語定義を使用します。

 クライアント プロジェクト ソース管理の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合をサポートするで使用可能な任意の[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]プロジェクト[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]の種類[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]( 、 、 など ) 。

 Web プロジェクト Web プロジェクトには、ファイル システム、ローカル IIS、リモート サイト、FTP の 4 種類があります。

- ファイル システム プロジェクトはローカル パス上に作成されますが、UNC パスを介して内部でアクセスされるため、インターネット インフォメーション サービス (IIS) をインストールする必要はありません。

- ローカル IIS プロジェクトは、同じコンピュータにインストールされている IIS と連携し、ローカル コンピュータを指す URL を使用してアクセスします。

- リモート サイト プロジェクトも IIS サービスの下に作成されますが[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、IIS サーバー コンピュータのソース管理下に配置され、IDE 内からは作成されません。

- FTP プロジェクトはリモート FTP サーバーを介してアクセスされますが、ソース管理下に置くことはできません。

  参加 ソース管理下のソリューションまたはプロジェクトの別の用語。

  バージョン ストア ソース管理プラグイン API を介してアクセスされているソース管理データベース。

## <a name="test-areas-covered-in-this-section"></a>このセクションで扱うテストエリア

- [テスト領域 1: ソース管理から追加/開く](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - ケース 1a: ソース管理へのソリューションの追加

  - ケース 1b: ソース管理からソリューションを開く

  - ケース 1c: ソース管理からソリューションを追加する

- [テスト領域 2: ソース管理からの取得](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [テスト領域 3: チェックアウト/チェックアウトの取り消し](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - ケース 3: チェックアウト/チェックアウトの取り消し

  - ケース 3a: チェックアウト

  - ケース 3b: 切断されたチェックアウト

  - ケース 3c: クエリ編集/クエリ保存 (QEQS)

  - ケース 3d: サイレントチェックアウト

  - ケース 3e: チェックアウトを取り消す

- [テスト領域 4: チェックイン](../../extensibility/internals/test-area-4-check-in.md)

  - ケース 4a: 変更されたアイテム

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

  - ケース 8b: ソリューションベースの変更

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
