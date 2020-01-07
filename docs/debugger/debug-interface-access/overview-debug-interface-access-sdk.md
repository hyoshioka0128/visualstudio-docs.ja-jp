---
title: 概要 (Debug Interface Access SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- user-defined types
- .dbg files
- modules
- interfaces [DIA SDK]
- DBG files
- procedures [DIA SDK]
- executable files
- COM objects, in DIA SDK
- compilands
- executable images
ms.assetid: 720b4479-a8bc-4fec-860e-80c1a0780405
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e4269c620247f256d2cfae2e84b76ff60fcf9ba
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738607"
---
# <a name="overview-debug-interface-access-sdk"></a>概要 (Debug Interface Access SDK)
Microsoft デバッグ情報にアクセスするには、DIA SDK を使用します。 DIA SDK には、Microsoft がデバッグ情報の形式を変更するたびにコードを書き直す必要がなくなり、COM ベースの API セットが用意されています。 DIA SDK では、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] バージョン5.0 以降で生成される .pdb ファイルと dbg ファイルにある、以前のバージョンのデバッグ情報のセットから読み取ることもできます。

 DIA SDK 内の各インターフェイスは、特に指定されていない場合を除き、異なる COM オブジェクトを表します。 追加のインターフェイス (つまり、追加のオブジェクト) は、既存のインターフェイスポインターで `QueryInterface` を呼び出すことなく、 [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)や[IDiaSession:: findchildren](../../debugger/debug-interface-access/idiasession-findchildren.md)などの明示的なクエリによって作成されます。

## <a name="see-also"></a>関連項目
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
