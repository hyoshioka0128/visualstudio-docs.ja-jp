---
title: サンク |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- thunk properties [DIA SDK]
- thunk symbol
ms.assetid: 01abb95f-d89a-465c-a4eb-8e8509598c95
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68e5542f3257ead72c13d454affbd0713325a7b4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62576370"
---
# <a name="thunk"></a>サンク
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

各 `thunk` はタグによって識別され `SymTagThunk` ます。  
  
## <a name="properties"></a>プロパティ  
 次の表は、このシンボルの種類に対して有効なプロパティを示しています。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|`DWORD`|[CV_access_e 列挙](../../debugger/debug-interface-access/cv-access-e.md)値の1つであるアクセス修飾子属性 (DIA SDK v2.0 以降の場合のみ)。|  
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|位置のオフセット部分です。詳細については、 [LocationType 列挙体](../../debugger/debug-interface-access/locationtype.md)を参照してください。|  
|[IDiaSegment::get_addressSection](../../debugger/debug-interface-access/idiasegment-get-addresssection.md)|`DWORD`|セクションの位置の部分。詳細については、 [LocationType 列挙体](../../debugger/debug-interface-access/locationtype.md)を参照してください。|  
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|`IDiaSymbol*`|存在する場合は、外側のクラスの親。 (DIA SDK v2.0 以降のバージョンのみ)。|  
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|`DWORD`|外側のクラスの親シンボルの ID (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|サンクが定数としてマークされている場合は TRUE (DIA SDK Version 8.0 以降でのみ)。|  
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|`BOOL`|サンクが仮想関数の概要 (DIA SDK v2.0 以降でのみ) の場合は TRUE|  
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|サンクが静的と見なされる場合は TRUE (DIA SDK v2.0 以降でのみ)。|  
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|サンク内のコードのバイト数。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|外側のコンパイル単位、block、または function のシンボル。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文の親シンボルの ID。|  
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|エンドポイントには静的な場所があります。詳細については、「 [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md) の列挙」を参照してください。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|サンクの名前。|  
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|`BOOL`|サンクが純粋仮想 (DIA SDK v2.0 以降でのみ) の場合は TRUE。|  
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|モジュール内でのこのサンクの相対位置。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagThunk`( [Symtagenum 列挙](../../debugger/debug-interface-access/symtagenum.md)値のいずれか) を返します。|  
|[IDiaSymbol::get_targetOffset](../../debugger/debug-interface-access/idiasymbol-get-targetoffset.md)|`DWORD`|サンクターゲットの位置のオフセット部分。|  
|[IDiaSymbol::get_targetRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetrelativevirtualaddress.md)|`DWORD`|外側のブロック内のサンクターゲットの相対仮想アドレス。|  
|[IDiaSymbol::get_targetSection](../../debugger/debug-interface-access/idiasymbol-get-targetsection.md)|`DWORD`|サンクターゲットのセクション部分。|  
|[IDiaSymbol::get_targetVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetvirtualaddress.md)|`ULONGLONG`|実行可能イメージ内のサンクターゲットの位置。|  
|[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)|`DWORD`|[THUNK_ORDINAL 列挙体](../../debugger/debug-interface-access/thunk-ordinal.md)で定義されているサンク型。|  
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|このサンクの型 (DIA SDK Version 8.0 以降でのみ)。|  
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|型シンボルの ID (DIA SDK v2.0 以降の場合のみ)。|  
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` サンクがアラインされていない場合 (DIA SDK v2.0 以降でのみ)、|  
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|`BOOL`|`TRUE` サンクが virtual (DIA SDK v2.0 以降でのみ) の場合。|  
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|実行可能イメージ内のこのサンクの位置。|  
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|`DWORD`|このサンクへの仮想テーブル内のオフセット (DIA SDK v2.0 以降のみ)。|  
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` サンクが volatile としてマークされている場合は (DIA SDK v2.0 以降のみ)。|  
  
## <a name="see-also"></a>参照  
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)   
 [THUNK_ORDINAL 列挙型](../../debugger/debug-interface-access/thunk-ordinal.md)
