---
title: 複数のプロジェクト接続での設定の適用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bca17fdc440fc373d0d4811ed57cd5d27a6c201a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203849"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>複数のプロジェクト接続全体への設定の適用
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理プラグイン API 1.2 を使用して構築されたソース管理プラグインは、バッチ操作を使用して、複数のプロジェクトまたは複数の接続コンテキストで同じソース管理操作を実行できます。 バッチを使用すると、ユーザーエクスペリエンスから、プロジェクトごとの冗長なダイアログボックスを削除できます。  
  
 ソース管理プラグイン API 1.1 を使用して構築されたソース管理プラグイン内の複数の接続に属する複数の項目をユーザーが選択した場合 (たとえば、異なるファイル共有マシン上の2つの Web プロジェクトがある場合)、ユーザーは同じダイアログボックスを繰り返し表示します。 これは、ユーザーがダイアログボックスの [ **すべてに適用** ] チェックボックスをクリックした場合にも発生します。これは、IDE によって各接続コンテキストの状態がリセットされるためです。  
  
## <a name="new-capability-flag"></a>新しい機能フラグ  
 `SccBeginBatch` 関数は、 `SCC_CAP_BATCH` バッチ操作が進行中であることを示すフラグを設定します。  
  
## <a name="new-functions"></a>新しい関数  
 次の新しい関数では、バッチ操作をサポートしています。  
  
- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)  
  
- [SccEndBatch](../../extensibility/sccendbatch-function.md)  
  
  関数は、 `SCCBeginBatch` ソース管理操作のグループを開始します。 `SccEndBatch` グループを閉じます。 グループを入れ子にすることはできません。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
