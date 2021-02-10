---
title: ソース管理プラグイン向けのテスト ガイド | Microsoft Docs
description: Visual Studio を使用したソース管理プラグインのテストについて説明します。 この概要には、一般的なテスト領域が含まれています。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 951b83f425f1e7171c519fced3fa3a4644279621
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934143"
---
# <a name="test-guide-for-source-control-plug-ins"></a>ソース管理プラグイン向けのテスト ガイド
このセクションでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を使用したソース管理プラグインのテストに関するガイダンスを提供します。 特に一般的なテスト領域の大まかな概要と、問題が発生しやすい複雑な領域の一部を紹介します。 この概要は、テスト ケースの完全な一覧ではありません。

> [!NOTE]
> 最新の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE のバグ修正プログラムと機能強化によって、以前のバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の使用中には発生しなかった、既存のソース管理プラグインに関する問題が明らかになることがあります。 以前のバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] からプラグインに変更が加えられていない場合でも、このセクションで列挙されている領域については、既存のソース管理プラグインをテストすることを強くお勧めします。

## <a name="common-preparation"></a>一般的な準備
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] とターゲット ソース管理プラグインがインストールされているマシンが必要です。 2 つ目のマシンを同じように構成して、[ソース管理から開く] テストの一部で使用することができます。

## <a name="definition-of-terms"></a>用語の定義
 このテスト ガイドでは、次の用語定義を使用します。

 クライアント プロジェクト ソース管理の統合がサポートされる [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で使用できるプロジェクト タイプ ([!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] など)。

 Web プロジェクト 次の 4 種類の Web プロジェクトがあります: ファイル システム、ローカル IIS、リモート サイト、FTP。

- ファイル システム プロジェクトはローカル パスに作成されますが、UNC パスを使用して内部でアクセスされるため、インターネット インフォメーション サービス (IIS) をインストールする必要はありません。また、クライアント プロジェクトと同様に、IDE 内からソース管理下に配置することもできます。

- ローカル IIS プロジェクトは、同じマシンにインストールされ、ローカル コンピューターをポイントする URL でアクセスされる IIS で動作します。

- リモート サイト プロジェクトは IIS サービスの下にも作成されますが、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 内からではなく、IIS サーバー マシンのソース管理下に配置されます。

- FTP プロジェクトはリモート FTP サーバーを介してアクセスされますが、ソース管理下に配置することはできません。

  参加リスト ソース管理下にあるソリューションまたはプロジェクトに対するもう 1 つの用語。

  バージョン ストア ソース管理プラグイン API を使用してアクセスされているソース管理データベース。

## <a name="test-areas-covered-in-this-section"></a>このセクションで説明するテスト領域

- [テスト領域 1: ソース管理への追加とオープン](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - ケース 1a: ソース管理へのソリューションの追加

  - ケース 1b: ソース管理からソリューションを開く

  - ケース 1c: ソース管理からのソリューションの追加

- [テスト領域 2: ソース管理から取得](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [テスト領域 3: チェックアウトとチェックアウトの取り消し](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - ケース 3: チェックアウトとチェックアウトの取り消し

  - ケース 3a: チェックアウト

  - ケース 3b: 切断されたチェックアウト

  - ケース 3c: クエリの編集/クエリの保存 (QEQS)

  - ケース 3d: サイレント チェックアウト

  - ケース 3e: チェックアウトの取り消し

- [テスト領域 4: チェックイン](../../extensibility/internals/test-area-4-check-in.md)

  - ケース 4a: 変更された項目

  - ケース 4b: ファイルの追加

  - ケース 4c: プロジェクトの追加

- [テスト領域 5: ソース管理の変更](../../extensibility/internals/test-area-5-change-source-control.md)

  - ケース 5a: Bind

  - ケース 5b: バインドの解除

  - ケース 5c: 再バインド

- [テスト領域 6: 削除](../../extensibility/internals/test-area-6-delete.md)

- [テスト領域 7: 共有](../../extensibility/internals/test-area-7-share.md)

- [テスト領域 8: プラグインの切り替え](../../extensibility/internals/test-area-8-plug-in-switching.md)

  - ケース 8a: 自動変更

  - ケース 8b: ソリューションベースの変更

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
