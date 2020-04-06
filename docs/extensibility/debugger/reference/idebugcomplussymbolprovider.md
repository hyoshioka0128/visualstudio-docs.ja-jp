---
title: を提供する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider interface
ms.assetid: 5b98e908-fd15-49a6-9010-933c9b948085
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 482ea1b2fb2eb7ddad46bd99694e4599e9fd9bbe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733479"
---
# <a name="idebugcomplussymbolprovider"></a>IDebugComPlusSymbolProvider
マネージ コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表します。

## <a name="syntax"></a>構文

```
IDebugComPlusSymbolProvider : IDebugSymbolProvider
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーター (EE) に役立つインターフェイスとデバッグ エンジン (DE) で使用されるインターフェイスとの間には分離はありませんが、次のメソッドはおそらく DE 開発者にのみ関心を持つでしょう。

## <a name="methods"></a>メソッド
 [インターフェイスの](../../../extensibility/debugger/reference/idebugsymbolprovider.md)メソッドに加えて、このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[AreSymbolsLoaded](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-aresymbolsloaded.md)|アプリケーション ドメイン識別子を指定して、指定したモジュールのデバッグ シンボルが読み込まれるかどうかを判断します。|
|[CreateTypeFromPrimitive](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-createtypefromprimitive.md)|指定したプリミティブ型から型を作成します。|
|[GetAddressesInModuleFromPosition](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getaddressesinmodulefromposition.md)|指定したモジュール内のドキュメントの位置をデバッグ アドレスの配列に割り当てします。|
|[GetArrayTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getarraytypefromaddress.md)|指定した配列のデバッグ アドレスに関する型情報を取得します。|
|[GetAssemblyName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getassemblyname.md)|モジュールとアプリケーション ドメインを指定したアセンブリの名前を取得します。|
|[GetAttributedClassesForLanguage](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesforlanguage.md)|指定したプログラミング言語で実装されている指定された属性を持つクラスを取得します。|
|[GetAttributedClassesinModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesinmodule.md)|指定したモジュール内の指定された属性を持つクラスを取得します。|
|[GetEntryPoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getentrypoint.md)|アプリケーションのエントリ ポイントを取得します。|
|[GetFunctionLineOffset](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getfunctionlineoffset.md)|指定された行オフセットを表す関数内のアドレスを取得します。|
|[GetLocalVariablelayout](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getlocalvariablelayout.md)|メソッドのセットのローカル変数のレイアウトを取得します。|
|[GetNameFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getnamefromtoken.md)|指定されたトークンに関連付けられた名前を返します。|
|[GetSymAttribute](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymattribute.md)|指定したモジュールの指定された親属性を持つデバッグ シンボルを取得します。|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymunmanagedreader.md)|アンマネージ コードで使用されるシンボル リーダーを取得します。|
|[GetTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-gettypefromaddress.md)|デバッグ アドレスを指定して、シンボルの型を取得します。|
|[IsFunctionDeleted](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctiondeleted.md)|指定したデバッグ アドレスの関数が削除されているかどうかを判断します。|
|[IsFunctionStale](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctionstale.md)|指定したデバッグ アドレスの関数が古いと見なされるかどうかを判断します。|
|[IsHiddenCode](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-ishiddencode.md)|指定したデバッガー アドレスのコードが非表示かどうかを判断します。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbols.md)|指定したデバッグ シンボルをメモリに読み込みます。|
|[LoadSymbolsFromStream](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbolsfromstream.md)|データ ストリームに指定されたデバッグ シンボルを読み込みます。|
|[ReplaceSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-replacesymbols.md)|現在のデバッグ シンボルを、指定したデータ ストリーム内のシンボルに置き換えます。|
|[UnloadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-unloadsymbols.md)|指定したモジュールのデバッグ シンボルをメモリからアンロードします。|
|[UpdateSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-updatesymbols.md)|メモリ内のデバッグ シンボルを、指定されたデータ ストリームで更新します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: を使用します。

 アセンブリ:
