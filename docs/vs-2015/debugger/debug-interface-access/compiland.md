---
title: コンパイル単位 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- compiland symbol
- compilands, compiland symbol
ms.assetid: c798eb2b-664a-41ec-ae90-5e9d292507ca
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 579ac6a70b379364870425e78cee41ac0840a214
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164006"
---
# <a name="compiland"></a>コンパイル単位
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

`SymTagCompiland`.Exe ファイルにリンクされているコンパイル単位ごとに1つのシンボルがあります。 コンパイル単位情報は `SymTagCompiland` 、追加のコンパイル単位シンボルを読み込まずに取得できるタグ、および `SymTagCompilandDetails` 追加のシンボルの読み込みを必要とする可能性のあるタグを持つシンボル間で分割されます。  
  
## <a name="properties"></a>プロパティ  
 次の表は、このシンボルの種類に対して有効なプロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` コンパイル時にエディットコンティニュが有効にされた場合は。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|.Exe ファイルのシンボル。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文の親シンボルの ID。|  
|[IDiaSymbol::get_libraryName](../../debugger/debug-interface-access/idiasymbol-get-libraryname.md)|`BSTR`|オブジェクトが読み込まれたライブラリまたはオブジェクトファイルの名前。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|コンパイル単位のオブジェクトファイルのファイル名。|  
|[IDiaSymbol::get_sourceFileName](../../debugger/debug-interface-access/idiasymbol-get-sourcefilename.md)|`BSTR`|ソースファイルの名前。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagCompiland`( [Symtagenum 列挙](../../debugger/debug-interface-access/symtagenum.md)値のいずれか) を返します。|  
  
## <a name="see-also"></a>参照  
 [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)   
 [CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)   
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
