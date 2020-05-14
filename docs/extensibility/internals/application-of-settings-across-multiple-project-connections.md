---
title: 複数のプロジェクト接続にわたる設定の適用 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bcaed0f7f2380dd36bcbffd776839025fe9efa16
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710059"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>複数のプロジェクト接続に設定を適用
ソース管理プラグイン API バージョン 1.2 を使用してビルドされたソース管理プラグインは、バッチ操作を使用して、複数のプロジェクトまたは複数の接続コンテキストで同じソース管理操作を実行できます。 バッチを使用すると、プロジェクトごとの冗長なダイアログ ボックスをユーザー エクスペリエンスから排除できます。

 ソース管理プラグイン API バージョン 1.1 を使用してビルドされたソース管理プラグインで複数の接続に属する複数の項目を選択し (たとえば、異なるファイル共有マシン上の 2 つの Web プロジェクト)、それらをチェックアウトすると、ユーザーは同じダイアログ ボックスを繰り返し表示します。 このシナリオは、IDE が各接続コンテキストの状態をリセットするため、ユーザーがダイアログ ボックスの **[すべてに適用**] チェック ボックスをクリックした場合でも発生します。

## <a name="new-capability-flag"></a>新しい機能フラグ
 この`SccBeginBatch`関数は、`SCC_CAP_BATCH`バッチ操作が進行中であることを示すフラグを設定します。

## <a name="new-functions"></a>新しい関数
次の新機能は、バッチ操作をサポートします。

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

この`SCCBeginBatch`関数は、ソース管理操作のグループを開始します。 この`SccEndBatch`関数はグループを閉じます。 グループはネストできません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
