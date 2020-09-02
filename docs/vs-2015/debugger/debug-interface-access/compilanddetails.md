---
title: CompilandDetails |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CompilandDetails symbol
ms.assetid: ddc7d794-c622-4c63-b2a6-72f8b2d0022a
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 34349bf096d8bb98ae4b3de7c7a922b8d28bc4f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702998"
---
# <a name="compilanddetails"></a>CompilandDetails
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コンパイル単位情報は、 `SymTagCompiland` タグ (low detail) と `SymTagCompilandDetails` タグ (high detail) を持つシンボル間で分割されます。 `SymTagCompilandDetails` 追加のシンボルを読み込む必要があります。 ただし、シンボルでは使用できないコンパイル単位に関する豊富な情報を提供し `SymTagCompiland` ます。  
  
## <a name="properties"></a>Properties  
 次の表は、このシンボルの種類に対して有効なプロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|コンパイラのバックエンドビルド番号。|  
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|コンパイラのバックエンドメジャーバージョン番号。|  
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|コンパイラのバックエンドマイナーバージョン番号。|  
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|このコンパイル単位を生成したコンパイラの名前 (DIA SDK v2.0 以降でのみ)。|  
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` コンパイル時にエディットコンティニュが有効にされた場合は。|  
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|コンパイラのフロントエンドビルド番号。|  
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|コンパイラのフロントエンドメジャーバージョン番号。|  
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|コンパイラのフロントエンドマイナーバージョン番号。|  
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|`TRUE` このコンパイル単位にデバッグ情報が含まれている場合は (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|`TRUE` このコンパイル単位にマネージコードが含まれている場合は (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` コンパイル単位が [/gs (バッファーセキュリティチェック)](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e) コンパイラスイッチを使用してコンパイルされた場合 (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|`TRUE` コンパイル単位が共通中間言語 (CIL) コードからネイティブコードに変換された場合。|  
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|`TRUE` ユーザー定義型 (UDT) が指定したメモリ境界に固定されている場合は (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|`TRUE` コンパイル単位が [/hotpatch (Create Hotpatchable Image)](https://msdn.microsoft.com/library/aad539b6-c053-4c78-8682-853d98327798) コンパイラスイッチを使用してコンパイルされた場合 (DIA SDK v2.0 以降でのみ)。|  
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|`TRUE` コンパイル単位が [/ltcg (リンク時のコード生成)](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2) コンパイラスイッチを使用してコンパイルされた場合 (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|コンパイル単位が Microsoft 中間言語 (MSIL) モジュールの場合は TRUE、(DIA SDK v2.0 以降でのみ)。|  
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|ソース コード言語。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|コンパイル単位のシンボル。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文の親シンボルの ID。|  
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|コンパイル単位がコンパイルされたプラットフォーム ( [CV_CPU_TYPE_e 列挙](../../debugger/debug-interface-access/cv-cpu-type-e.md) 値のいずれか)。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagCompilandDetails`( [Symtagenum 列挙](../../debugger/debug-interface-access/symtagenum.md)値のいずれか) を返します。|  
  
## <a name="remarks"></a>解説  
 多くの場合、コンパイラは2パスコンパイラと呼ばれる形式です。コンパイラのバージョンによっては、各パスが個別のプログラムによって処理される場合があります。 これらはそれぞれフロントエンドとバックエンドのコンパイラと呼ばれます。そのため、バックエンドとフロントエンドのバージョン番号のシンボルプロパティを使用します。  
  
## <a name="see-also"></a>参照  
 [コンパイル単位](../../debugger/debug-interface-access/compiland.md)   
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
