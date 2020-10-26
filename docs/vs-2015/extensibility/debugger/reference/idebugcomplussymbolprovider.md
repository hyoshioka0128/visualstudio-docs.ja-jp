---
title: IDebugComPlusSymbolProvider |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider interface
ms.assetid: 5b98e908-fd15-49a6-9010-933c9b948085
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b70701aa9c4b339749554601e2a565c17697c6a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186509"
---
# <a name="idebugcomplussymbolprovider"></a>IDebugComPlusSymbolProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

マネージコードに固有のメソッドを持つ COM + シンボルプロバイダーを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugComPlusSymbolProvider : IDebugSymbolProvider  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 式エバリュエーター (EE) に役立つインターフェイスと、デバッグエンジン (DE) によって使用されるインターフェイスを分離することはできませんが、次のメソッドでは、開発者のみが対象となります。 Aresymde Sloaded、GetEntryPoint Inmodulefromposition、GetEntryPoint、GetFunctionLineOffset、GetLocalVariableLayout、IsFunctionStale、LoadSymbols、Loadsymbols Fromstream、ReplaceSymbols、UnloadSymbols、および UpdateSymbols。  
  
## <a name="methods"></a>メソッド  
 このインターフェイスは、 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[AreSymbolsLoaded](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-aresymbolsloaded.md)|アプリケーションドメイン識別子を指定して、指定したモジュールのデバッグシンボルを読み込むかどうかを決定します。|  
|[CreateTypeFromPrimitive](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-createtypefromprimitive.md)|指定したプリミティブ型から型を作成します。|  
|[GetAddressesInModuleFromPosition](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getaddressesinmodulefromposition.md)|指定したモジュール内のドキュメント位置をデバッグアドレスの配列にマップします。|  
|[GetArrayTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getarraytypefromaddress.md)|デバッグアドレスを指定して、指定した配列に関する型情報を取得します。|  
|[GetAssemblyName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getassemblyname.md)|モジュールとアプリケーションドメインを指定して、アセンブリの名前を取得します。|  
|[GetAttributedClassesForLanguage](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesforlanguage.md)|指定したプログラミング言語で実装されている、指定した属性を持つクラスを取得します。|  
|[GetAttributedClassesinModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesinmodule.md)|指定したモジュール内の指定した属性を持つクラスを取得します。|  
|[GetEntryPoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getentrypoint.md)|アプリケーションのエントリポイントを取得します。|  
|[GetFunctionLineOffset](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getfunctionlineoffset.md)|指定された行オフセットを表す関数内のアドレスを取得します。|  
|[GetLocalVariablelayout](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getlocalvariablelayout.md)|一連のメソッドのローカル変数のレイアウトを取得します。|  
|[GetNameFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getnamefromtoken.md)|指定されたメタデータオブジェクトを使用して、指定したトークンに関連付けられている名前を返します。|  
|[GetSymAttribute](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymattribute.md)|指定したモジュールの指定した親属性を持つデバッグシンボルを取得します。|  
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymunmanagedreader.md)|アンマネージコードによって使用されるシンボルリーダーを取得します。|  
|[GetTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-gettypefromaddress.md)|デバッグアドレスを指定してシンボル型を取得します。|  
|[IsFunctionDeleted](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctiondeleted.md)|指定されたデバッグアドレスにある関数が削除されるかどうかを判断します。|  
|[IsFunctionStale](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctionstale.md)|指定されたデバッグアドレスにある関数が古いものと見なされるかどうかを判断します。|  
|[IsHiddenCode](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-ishiddencode.md)|指定したデバッガーアドレスにあるコードが非表示かどうかを判断します。|  
|[LoadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbols.md)|指定されたデバッグシンボルをメモリに読み込みます。|  
|[LoadSymbolsFromStream](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbolsfromstream.md)|データストリームを指定してデバッグシンボルを読み込みます。|  
|[ReplaceSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-replacesymbols.md)|現在のデバッグシンボルを、指定したデータストリーム内のシンボルに置き換えます。|  
|[UnloadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-unloadsymbols.md)|指定したモジュールのデバッグシンボルをメモリからアンロードします。|  
|[UpdateSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-updatesymbols.md)|指定されたデータストリームを使用して、メモリ内のデバッグシンボルを更新します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: Sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
