---
title: シンボルとシンボルタグ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK]
ms.assetid: 2ee3a262-cda6-48bf-b799-a37edde6c8b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5d2281a82926dabfde88b8d4bb9096f0e9624211
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738531"
---
# <a name="symbols-and-symbol-tags"></a>シンボルとシンボル タグ
コンパイルされたプログラムに関するデバッグ情報は、Debug Interface Access (DIA) SDK Api を使用してアクセスできるシンボルとしてプログラムデータベース (.pdb) ファイルに格納されます。 すべてのシンボルには、 [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)プロパティと[IDiaSymbol:: get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)プロパティがあります。 @No__t_0 プロパティは、 [Symtagenum](../../debugger/debug-interface-access/symtagenum.md)列挙列挙によって定義されるシンボルの種類を示します。 @No__t_0 プロパティは、シンボルのすべてのインスタンスの一意の識別子を含む `DWORD` 値です。

 シンボルには、シンボルに関する追加情報と他のシンボルへの参照 (多くの場合、 [IDiaSymbol:: get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)または[IDiaSymbol:: get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)) を指定できるプロパティもあります。 参照が含まれているプロパティに対してクエリを実行すると、参照が[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)オブジェクトとして返されます。 このようなプロパティは、常に同じ名前の別のプロパティとペアになりますが、"Id" がサフィックスとして付けられます (たとえば、 [IDiaSymbol:: get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)および[IDiaSymbol:: get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md))。 シンボルの[場所](../../debugger/debug-interface-access/symbol-locations.md)のテーブル、[シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)、および[シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)は、さまざまな種類のシンボルのプロパティの概要を示します。 これらのプロパティには、または他のシンボルに関する関連情報が含まれている場合があります。 @No__t_0 のプロパティは、関連するプロパティの単なる数値の序数識別子であるため、それ以上の議論から省略されます。 これらは、パラメーターを明確にするために必要な場合にのみ参照されます。

 プロパティにアクセスしようとすると、エラーが発生せず、symbol プロパティに値が割り当てられている場合、プロパティの "get" メソッドは `S_OK` を返します。 @No__t_0 の戻り値は、現在のシンボルに対してプロパティが無効であることを示します。

## <a name="in-this-section"></a>このセクションの内容

[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)

シンボルが持つことができるさまざまな種類の場所について説明します。

[シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)

ファイル、モジュール、関数など、字句階層を形成するシンボル型について説明します。

[シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)

クラス、配列、および関数の戻り値の型など、さまざまな言語要素に対応するシンボル型について説明します。

## <a name="see-also"></a>関連項目

- [Debug Interface Access SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)