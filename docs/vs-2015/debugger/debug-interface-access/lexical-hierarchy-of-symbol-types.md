---
title: シンボル型の構文階層 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], type hierarchies
ms.assetid: 912da653-ddfe-45a4-84aa-64281283739a
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e70b83046c41b13cb51324eb63e81b26a118a81f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841948"
---
# <a name="lexical-hierarchy-of-symbol-types"></a>シンボル型の構文階層
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次の表は、字句階層内のシンボルの種類を示しています。  
  
## <a name="symbol-types"></a>シンボルの種類  
  
|シンボルの種類|Description|  
|-----------------|-----------------|  
|[注釈](../../debugger/debug-interface-access/annotation.md)|プログラムコード内の注釈付きの場所を指定します。|  
|[ブロック](../../debugger/debug-interface-access/block.md)|関数で入れ子になったスコープを指定します。|  
|`Compiland`|.Exe ファイルにリンクされたを指定します `compiland` 。|  
|[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)|追加のコンパイル単位 details の読み込みを必要とする可能性のあるコンパイル単位データを指定します。これにより、取得する実行時のオーバーヘッドが発生します。|  
|[CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)|コンパイル単位のコンパイルにとって重要な追加の環境変数を指定します。|  
|[カスタム (Debug Interface Access SDK)](../../debugger/debug-interface-access/custom-debug-interface-access-sdk.md)|ユーザー定義のシンボルを指定します。|  
|[データ (Debug Interface Access SDK)](../../debugger/debug-interface-access/data-debug-interface-access-sdk.md)|このような変数をパラメーター、ローカル変数、グローバル変数、およびクラスメンバーとして指定します。|  
|[Exe](../../debugger/debug-interface-access/exe.md)|データのグローバルスコープを指定します。.exe ファイルまたは .dll ファイル全体に対応します。|  
|[FuncDebugEnd](../../debugger/debug-interface-access/funcdebugend.md)|デバッグの終了位置を定義した点を持つ関数を指定します。|  
|[FuncDebugStart](../../debugger/debug-interface-access/funcdebugstart.md)|デバッグを開始するポイントが定義されている関数を指定します。|  
|[関数 (Debug Interface Access SDK)](../../debugger/debug-interface-access/function-debug-interface-access-sdk.md)|関数を指定します。|  
|[ラベル (Debug Interface Access SDK)](../../debugger/debug-interface-access/label-debug-interface-access-sdk.md)|プログラムコード内の場所を指定します。|  
|[PublicSymbol](../../debugger/debug-interface-access/publicsymbol.md)|実行可能プログラムをビルドするときに表示される外部シンボルを指定します。|  
|[サンク](../../debugger/debug-interface-access/thunk.md)|を指定し `thunk` ます。|  
|[UsingNameSpace](../../debugger/debug-interface-access/usingnamespace.md)|識別子を指定し `namespace` ます。|  
  
> [!NOTE]
> シンボルの種類によっては、追加のシンボルプロパティを使用できる場合があります。 これらのプロパティは、個々のシンボルのトピックに一覧表示されます。  
  
## <a name="see-also"></a>参照  
 [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)   
 [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)   
 [シンボルとシンボルタグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)   
 [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
