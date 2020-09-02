---
title: シンボルとシンボルタグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK]
ms.assetid: 2ee3a262-cda6-48bf-b799-a37edde6c8b8
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 625752125d3c68e9f03afd41cd549995fbc3272e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193537"
---
# <a name="symbols-and-symbol-tags"></a>シンボルとシンボル タグ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コンパイルされたプログラムに関するデバッグ情報は、Debug Interface Access (DIA) SDK Api を使用してアクセスできるシンボルとしてプログラムデータベース (.pdb) ファイルに格納されます。 すべてのシンボルには、 [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) と [IDiaSymbol:: get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md) プロパティがあります。 プロパティは、 `symTag` [Symtagenum](../../debugger/debug-interface-access/symtagenum.md) 列挙型によって定義されるシンボルの種類を示します。 `symIndexId`プロパティは、 `DWORD` シンボルのすべてのインスタンスの一意の識別子を含む値です。  
  
 シンボルには、シンボルに関する追加情報と他のシンボルへの参照 (多くの場合、 [IDiaSymbol:: get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md) または [IDiaSymbol:: get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)) を指定できるプロパティもあります。 参照が含まれているプロパティに対してクエリを実行すると、参照が [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトとして返されます。 このようなプロパティは、常に同じ名前の別のプロパティとペアになりますが、"Id" がサフィックスとして付けられます (たとえば、 [IDiaSymbol:: get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md) と [IDiaSymbol:: get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md))。 シンボルの [場所](../../debugger/debug-interface-access/symbol-locations.md)のテーブル、 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)、および [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md) は、さまざまな種類のシンボルのプロパティの概要を示します。 これらのプロパティには、または他のシンボルに関する関連情報が含まれている場合があります。 プロパティは、 `*Id` 関連するプロパティの単なる数値の序数識別子であるため、それ以上の議論から省略されます。 これらは、パラメーターを明確にするために必要な場合にのみ参照されます。  
  
 プロパティにアクセスしようとすると、エラーが発生せず、symbol プロパティに値が割り当てられている場合、プロパティの "get" メソッドはを返し `S_OK` ます。 戻り値がの場合は、 `S_FALSE` プロパティが現在のシンボルに対して無効であることを示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)  
 シンボルが持つことができるさまざまな種類の場所について説明します。  
  
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)  
 ファイル、モジュール、関数など、字句階層を形成するシンボル型について説明します。  
  
 [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)  
 クラス、配列、および関数の戻り値の型など、さまざまな言語要素に対応するシンボル型について説明します。  
  
## <a name="see-also"></a>参照  
 [Debug Interface Access SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)
