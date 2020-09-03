---
title: 概要 (Debug Interface Access SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
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
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7374b03da42e34e8ac3be8c7cc570769d9cfd1ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179209"
---
# <a name="overview-debug-interface-access-sdk"></a>概要 (Debug Interface Access SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Microsoft デバッグ情報にアクセスするには、DIA SDK を使用します。 DIA SDK には、Microsoft がデバッグ情報の形式を変更するたびにコードを書き直す必要がなくなり、COM ベースの API セットが用意されています。 DIA SDK では、バージョン5.0 以降で生成される .pdb ファイルと dbg ファイルにある、以前のバージョンのデバッグ情報のセットから読み取ることもでき [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] ます。  
  
 DIA SDK 内の各インターフェイスは、特に指定されていない場合を除き、異なる COM オブジェクトを表します。 追加のインターフェイス (つまり、追加のオブジェクト) は、既存のインターフェイスポインターでを呼び出すのではなく、明示的なクエリ ( [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) や [IDiaSession:: findchildren](../../debugger/debug-interface-access/idiasession-findchildren.md)など) によって作成され `QueryInterface` ます。  
  
## <a name="see-also"></a>参照  
 [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)   
 [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
