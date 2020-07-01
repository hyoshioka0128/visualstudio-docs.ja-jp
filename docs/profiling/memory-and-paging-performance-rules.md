---
title: メモリとページングのパフォーマンス規則 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f37972b2-efe4-4a1c-a5d1-a246ccd76817
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 716bc771310b73c8a0b11a97080184d9868fe91b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535136"
---
# <a name="memory-and-paging-performance-rules"></a>メモリとページングのパフォーマンス規則
メモリとページングのカテゴリのパフォーマンス規則は、アプリケーションのパフォーマンスと応答性に影響を与える可能性があるページング アクティビティをプロファイル実行で特定します。

|ルール|説明|
|-|-|
|[DA0014: ディスクへのアクティブなメモリのページングが非常に高率で発生しています](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md)|ディスクへのアクティブなメモリのページングがプロファイリング実行全体において非常に高率で発生しています。 通常、このレベルのページング率は、アプリケーションのパフォーマンスと応答性に影響します。 アルゴリズムを修正してメモリの割り当てを減らすことを検討してください。 また、アプリケーションのメモリ要件も検討した方がよいでしょう。 より多くのメモリを備えたコンピューターでプロファイリングを再度実行してみてください。 この規則は、ページング アクティビティの量が規則 D0017 の上限のしきい値を超えた場合に適用されます。|
|[DA0017: ディスクへのアクティブなメモリのページングが高率で発生しています](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md)|ディスクへのアクティブなメモリのページングがプロファイリング実行全体において比較的高率で発生しています。 通常、このレベルのページング率は、アプリケーションのパフォーマンスと応答性に影響します。 アルゴリズムを修正してメモリの割り当てを減らすことを検討してください。 また、アプリケーションのメモリ要件も検討した方がよいでしょう。 より多くのメモリを備えたコンピューターでプロファイリングを再度実行してみてください。|
