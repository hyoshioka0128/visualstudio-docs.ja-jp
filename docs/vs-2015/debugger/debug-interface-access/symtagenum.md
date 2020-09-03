---
title: SymTagEnum |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1578d88265769414f68964e28d3426ffcc62f9e8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193512"
---
# <a name="symtagenum"></a>SymTagEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルの種類を指定します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
enum SymTagEnum {   
   SymTagNull,  
   SymTagExe,  
   SymTagCompiland,  
   SymTagCompilandDetails,  
   SymTagCompilandEnv,  
   SymTagFunction,  
   SymTagBlock,  
   SymTagData,  
   SymTagAnnotation,  
   SymTagLabel,  
   SymTagPublicSymbol,  
   SymTagUDT,  
   SymTagEnum,  
   SymTagFunctionType,  
   SymTagPointerType,  
   SymTagArrayType,   
   SymTagBaseType,   
   SymTagTypedef,   
   SymTagBaseClass,  
   SymTagFriend,  
   SymTagFunctionArgType,   
   SymTagFuncDebugStart,   
   SymTagFuncDebugEnd,  
   SymTagUsingNamespace,   
   SymTagVTableShape,  
   SymTagVTable,  
   SymTagCustom,  
   SymTagThunk,  
   SymTagCustomType,  
   SymTagManagedType,  
   SymTagDimension,  
   SymTagCallSite,  
   SymTagInlineSite,  
   SymTagBaseInterface,  
   SymTagVectorType,  
   SymTagMatrixType,  
   SymTagHLSLType  
};  
```  
  
## <a name="elements"></a>要素  
 `SymTagNull`  
 記号に型がないことを示します。  
  
 `SymTagExe`  
 シンボルが .exe ファイルであることを示します。 シンボルストアごとにシンボルが1つだけ存在 `SymTagExe` します。 グローバルスコープとして機能し、構文の親を持ちません。  
  
 `SymTagCompiland`  
 シンボルストアの各コンパイル単位コンポーネントのコンパイル単位シンボルを示します。 ネイティブアプリケーションの場合、シンボルは、 `SymTagCompiland` イメージにリンクされたオブジェクトファイルに対応します。 一部の種類の Microsoft 中間言語 (MSIL) イメージには、クラスごとに1つのコンパイル単位があります。  
  
 `SymTagCompilandDetails`  
 シンボルにコンパイル単位の拡張属性が含まれていることを示します。 これらのプロパティを取得するには、コンパイル単位シンボルの読み込みが必要になることがあります。  
  
 `SymTagCompilandEnv`  
 シンボルが、コンパイル単位に対して定義された環境文字列であることを示します。  
  
 `SymTagFunction`  
 シンボルが関数であることを示します。  
  
 `SymTagBlock`  
 シンボルが入れ子になったブロックであることを示します。  
  
 `SymTagData`  
 記号がデータであることを示します。  
  
 `SymTagAnnotation`  
 シンボルがコード注釈用であることを示します。 この記号の子は、定数のデータ文字列 ( `SymTagData` 、 `LocIsConstant` 、 `DataIsConstant` ) です。 ほとんどのクライアントはこのシンボルを無視します。  
  
 `SymTagLabel`  
 記号がラベルであることを示します。  
  
 `SymTagPublicSymbol`  
 シンボルがパブリックシンボルであることを示します。 ネイティブアプリケーションの場合、このシンボルは、イメージのリンク中に検出された COFF 外部シンボルです。  
  
 `SymTagUDT`  
 シンボルがユーザー定義型 (構造体、クラス、または共用体) であることを示します。  
  
 `SymTagEnum`  
 シンボルが列挙体であることを示します。  
  
 `SymTagFunctionType`  
 シンボルが関数シグネチャ型であることを示します。  
  
 `SymTagPointerType`  
 シンボルがポインター型であることを示します。  
  
 `SymTagArrayType`  
 記号が配列型であることを示します。  
  
 `SymTagBaseType`  
 記号が基本型であることを示します。  
  
 `SymTagTypedef`  
 記号がであるか、 `typedef` 別の型のエイリアスであることを示します。  
  
 `SymTagBaseClass`  
 シンボルがユーザー定義型の基本クラスであることを示します。  
  
 `SymTagFriend`  
 シンボルがユーザー定義型のフレンドであることを示します。  
  
 `SymTagFunctionArgType`  
 シンボルが関数の引数であることを示します。  
  
 `SymTagFuncDebugStart`  
 シンボルが関数のプロローグコードの終了位置であることを示します。  
  
 `SymTagFuncDebugEnd`  
 シンボルが関数のエピローグコードの開始位置であることを示します。  
  
 `SymTagUsingNamespace`  
 シンボルが現在のスコープ内でアクティブな名前空間の名前であることを示します。  
  
 `SymTagVTableShape`  
 シンボルが仮想テーブルの説明であることを示します。  
  
 `SymTagVTable`  
 シンボルが仮想テーブルポインターであることを示します。  
  
 `SymTagCustom`  
 シンボルがカスタムシンボルであり、DIA によって解釈されないことを示します。  
  
 `SymTagThunk`  
 記号が16ビットコードと32ビットコードの間でデータを共有するために使用されるサンクであることを示します。  
  
 `SymTagCustomType`  
 シンボルがカスタムコンパイラシンボルであることを示します。  
  
 `SymTagManagedType`  
 シンボルがメタデータ内にあることを示します。  
  
 `SymTagDimension`  
 記号が FORTRAN 多次元配列であることを示します。  
  
 `SymTagCallSite`  
 シンボルが呼び出しサイトを表すことを示します。  
  
 `SymTagInlineSite`  
 記号がインラインサイトを表すことを示します。  
  
 `SymTagBaseInterface`  
 シンボルが基本インターフェイスであることを示します。  
  
 `SymTagVectorType`  
 記号がベクター型であることを示します。  
  
 `SymTagMatrixType`  
 記号がマトリックス型であることを示します。  
  
 `SymTagHLSLType`  
 シンボルがハイレベルシェーダー言語型であることを示します。  
  
## <a name="remarks"></a>注釈  
 デバッグファイル内のすべてのシンボルには、シンボルの型を指定する識別タグがあります。  
  
 この列挙体の値は、 [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) メソッドへの呼び出しによって返されます。  
  
 この列挙体の値は、検索の範囲を特定のシンボルの種類に制限するために、次のメソッドに渡されます。  
  
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)  
  
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)  
  
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)  
  
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)  
  
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)  
  
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)  
  
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)  
  
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst. h  
  
## <a name="see-also"></a>参照  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [IDiaSession:: Findシンボル Byaddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)   
 [IDiaSession:: Findシンボル Byrva](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)   
 [IDiaSession:: findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)   
 [IDiaSession:: Findシンボル Bytoken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)   
 [IDiaSession:: Findシンボル Byva](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)   
 [IDiaSession:: findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)   
 [IDiaSession:: findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
