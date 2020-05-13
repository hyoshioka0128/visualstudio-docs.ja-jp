---
title: SymTagEnum |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 806fe878468baa06b52a15879ceaff1b376461e9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738510"
---
# <a name="symtagenum"></a>SymTagEnum
シンボルの種類を指定します。

## <a name="syntax"></a>構文

```C++
enum SymTagEnum {
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

## <a name="elements"></a>Elements
`SymTagNull` は、シンボルに型がないことを示します。

`SymTagExe` は、シンボルが .exe ファイルであることを示します。 シンボルストアごとに `SymTagExe` シンボルが1つだけあります。 グローバルスコープとして機能し、構文の親を持ちません。

シンボルストアの各コンパイル単位コンポーネントのコンパイル単位シンボルを示す `SymTagCompiland` です。 ネイティブアプリケーションの場合、`SymTagCompiland` シンボルは、イメージにリンクされたオブジェクトファイルに対応します。 一部の種類の Microsoft 中間言語 (MSIL) イメージには、クラスごとに1つのコンパイル単位があります。

`SymTagCompilandDetails` は、コンパイル単位の拡張属性がシンボルに含まれていることを示します。 これらのプロパティを取得するには、コンパイル単位シンボルの読み込みが必要になることがあります。

`SymTagCompilandEnv` は、シンボルがコンパイル単位に対して定義された環境文字列であることを示します。

`SymTagFunction` は、シンボルが関数であることを示します。

`SymTagBlock` は、シンボルが入れ子になったブロックであることを示します。

`SymTagData` は、記号がデータであることを示します。

`SymTagAnnotation` は、シンボルがコード注釈用であることを示します。 この記号の子は、定数のデータ文字列 (`SymTagData`、`LocIsConstant`、`DataIsConstant`) です。 ほとんどのクライアントはこのシンボルを無視します。

`SymTagLabel` は、記号がラベルであることを示します。

`SymTagPublicSymbol` は、シンボルがパブリックシンボルであることを示します。 ネイティブアプリケーションの場合、このシンボルは、イメージのリンク中に検出された COFF 外部シンボルです。

`SymTagUDT` は、シンボルがユーザー定義型 (構造体、クラス、または共用体) であることを示します。

`SymTagEnum` は、シンボルが列挙体であることを示します。

`SymTagFunctionType` は、シンボルが関数シグネチャ型であることを示します。

`SymTagPointerType` は、シンボルがポインター型であることを示します。

`SymTagArrayType` は、シンボルが配列型であることを示します。

`SymTagBaseType` は、シンボルが基本データ型であることを示します。

`SymTagTypedef` は、シンボルが `typedef`、つまり別の型の別名であることを示します。

`SymTagBaseClass` は、シンボルがユーザー定義型の基本クラスであることを示します。

`SymTagFriend` は、シンボルがユーザー定義型のフレンドであることを示します。

`SymTagFunctionArgType` は、シンボルが関数の引数であることを示します。

`SymTagFuncDebugStart` は、シンボルが関数のプロローグコードの終了位置であることを示します。

`SymTagFuncDebugEnd` は、シンボルが関数のエピローグコードの開始位置であることを示します。

`SymTagUsingNamespace` は、シンボルが現在のスコープでアクティブになっている名前空間の名前であることを示します。

`SymTagVTableShape` は、シンボルが仮想テーブルの説明であることを示します。

`SymTagVTable` は、シンボルが仮想テーブルポインターであることを示します。

`SymTagCustom` は、シンボルがカスタムシンボルであり、DIA によって解釈されないことを示します。

`SymTagThunk` は、16ビットコードと32ビットコードの間でデータを共有するために使用されるサンクであることを示します。

`SymTagCustomType` は、シンボルがカスタムコンパイラシンボルであることを示します。

`SymTagManagedType` は、シンボルがメタデータ内にあることを示します。

`SymTagDimension` は、その記号が FORTRAN 多次元配列であることを示します。

`SymTagCallSite` は、シンボルが呼び出しサイトを表すことを示します。

`SymTagInlineSite` は、シンボルがインラインサイトを表すことを示します。

`SymTagBaseInterface` は、シンボルが基本インターフェイスであることを示します。

`SymTagVectorType` は、シンボルがベクター型であることを示します。

`SymTagMatrixType` は、記号がマトリックス型であることを示します。

`SymTagHLSLType` は、シンボルが高レベルのシェーダー言語の種類であることを示します。

## <a name="remarks"></a>Remarks
デバッグファイル内のすべてのシンボルには、シンボルの型を指定する識別タグがあります。

この列挙体の値は、 [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)メソッドの呼び出しによって返されます。

この列挙体の値は、検索の範囲を特定のシンボルの種類に制限するために、次のメソッドに渡されます。

- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)

- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)

- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)

- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)

- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)

- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>［要件］
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
