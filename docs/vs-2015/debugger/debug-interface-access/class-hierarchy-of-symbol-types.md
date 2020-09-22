---
title: シンボル型のクラス階層 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], class hierarchies
ms.assetid: 0ccd6990-4654-44cd-a6f3-bdd82fe90f6c
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3a7b3edb0262e3e2b4f0cde51b499e25b04aba51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842184"
---
# <a name="class-hierarchy-of-symbol-types"></a>シンボル型のクラス階層
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次の表では、クラス階層のシンボル型について説明します。  
  
## <a name="symbol-types"></a>シンボルの種類  
  
|シンボルの種類|Description|  
|-----------------|-----------------|  
|[UDT](../../debugger/debug-interface-access/udt.md)|各クラス、構造体、および共用体を表すために使用される記号。|  
|[Enum (Debug Interface Access SDK)](../../debugger/debug-interface-access/enum-debug-interface-access-sdk.md)|列挙型のシンボル。|  
|[PointerType](../../debugger/debug-interface-access/pointertype.md)|ポインター型のシンボル。|  
|[ArrayType](../../debugger/debug-interface-access/arraytype.md)|配列型のシンボル。|  
|[BaseType](../../debugger/debug-interface-access/basetype.md)|基本型のシンボル|  
|[Typedef (Debug Interface Access SDK)](../../debugger/debug-interface-access/typedef-debug-interface-access-sdk.md)|他の型の名前を導入するシンボル。|  
|[BaseClass](../../debugger/debug-interface-access/baseclass.md)|ユーザー定義型 (UDT) の各基底クラスに使用されるシンボル。|  
|[フレンド (Debug Interface Access SDK)](../../debugger/debug-interface-access/friend-debug-interface-access-sdk.md)|フレンドクラスおよびフレンド関数のシンボル。|  
|[FunctionType](../../debugger/debug-interface-access/functiontype.md)|一意の関数シグネチャごとにシンボル。|  
|[FunctionArgType](../../debugger/debug-interface-access/functionargtype.md)|関数に対する各パラメーターのシンボル。|  
|[VTableShape](../../debugger/debug-interface-access/vtableshape.md)|仮想テーブルのサイズのシンボル。|  
|[VTable](../../debugger/debug-interface-access/vtable.md)|仮想テーブルのシンボル。|  
|[CustomType](../../debugger/debug-interface-access/customtype.md)|ベンダー定義型のシンボル。|  
|[ManagedType](../../debugger/debug-interface-access/managedtype.md)|メタデータで定義されている型のシンボル。|  
|[ディメンション](../../debugger/debug-interface-access/dimension.md)|配列の次元のシンボル。|  
  
> [!NOTE]
> 各シンボルには、シンボルに関する情報を保持するプロパティや、その他のシンボルへの参照を含めることができます。 これらのプロパティは、個々のシンボルのトピックに一覧表示されます。  
  
## <a name="see-also"></a>参照  
 [CV_access_e 列挙型](../../debugger/debug-interface-access/cv-access-e.md)   
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
