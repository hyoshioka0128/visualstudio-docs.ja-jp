---
title: 複数のプロジェクト接続に設定を適用する
description: ソース管理プラグインを使用してバッチ操作を実行することで、複数のプロジェクト接続で設定を適用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 14b466112e3939756142a43568ddc3107e55d659
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906089"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>複数のプロジェクト接続での設定の適用
ソース管理プラグイン API バージョン1.2 を使用して構築されたソース管理プラグインは、バッチ操作を使用して、複数のプロジェクトまたは複数の接続コンテキストで同じソース管理操作を実行できます。 バッチを使用すると、ユーザーエクスペリエンスから、プロジェクトごとの冗長なダイアログボックスを削除できます。

 ソース管理プラグイン API バージョン 1.1 (異なるファイル共有マシン上の2つの web プロジェクトなど) を使用してビルドされたソース管理プラグイン内の複数の接続に属する複数の項目をユーザーが選択した場合、ユーザーは同じダイアログボックスを繰り返し表示します。 このシナリオは、ユーザーがダイアログボックスの [ **すべてに適用** ] チェックボックスをクリックした場合にも発生します。これは、IDE によって各接続コンテキストの状態がリセットされるためです。

## <a name="new-capability-flag"></a>新しい機能フラグ
 関数は、 `SccBeginBatch` `SCC_CAP_BATCH` バッチ操作が進行中であることを示すフラグを設定します。

## <a name="new-functions"></a>新しい関数
次の新しい関数では、バッチ操作をサポートしています。

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

関数は、 `SCCBeginBatch` ソース管理操作のグループを開始します。 関数は、 `SccEndBatch` グループを閉じます。 グループを入れ子にすることはできません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
