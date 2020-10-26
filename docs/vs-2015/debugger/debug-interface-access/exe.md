---
title: Exe |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- .dll files
- Exe symbol
- .exe files
- executable files, Exe symbol
ms.assetid: a781d2cf-55fe-4373-9cf1-b732864244e0
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fe2930e0947bf0fa69408dc81c19d058d6cdd870
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164263"
---
# <a name="exe"></a>Exe
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Exe は、構文またはクラスの親を持たない唯一のシンボルであり、.exe または .dll ファイルのグローバルスコープを表します。 ファイルごとにタグを持つシンボルは1つだけです `SymTagExe` 。 [IDiaSession:: get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)メソッドは、シンボルを返します。  
  
## <a name="properties"></a>プロパティ  
 次の表は、このシンボルの種類に対して有効なプロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|`DWORD`|この実行可能ファイルの経過期間。|  
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|`GUID`|`GUID` この実行可能ファイルの。|  
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|`BOOL`|`TRUE` この実行可能ファイルに関連付けられているシンボルファイルに C 型が含まれている場合は (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|`BOOL`|`TRUE` この実行可能ファイルに関連付けられているシンボルファイルからプライベートシンボルが削除されている場合は (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|`DWORD`|ターゲット CPU ( [CV_CPU_TYPE_e 列挙](../../debugger/debug-interface-access/cv-cpu-type-e.md) 値のいずれか) を示す値。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|.Exe ファイルの名前。|  
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|`DWORD`|実行可能ファイルの署名。|  
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|`BSTR`|.Exe ファイルの .pdb ファイルまたは dbg ファイルの完全パス。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagExe`( [Symtagenum 列挙](../../debugger/debug-interface-access/symtagenum.md)値のいずれか) を返します。|  
  
## <a name="see-also"></a>参照  
 [IDiaSession:: get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)   
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
