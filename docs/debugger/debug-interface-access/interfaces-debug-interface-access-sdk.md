---
title: インターフェイス (Debug Interface Access SDK) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- interfaces [DIA SDK]
- DIA SDK, interfaces
ms.assetid: 62aee7c3-d314-4272-a32b-b2818f32fab8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a0aa48ae0d3c3b6b05ea469baea1a1e1aa106667
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738695"
---
# <a name="interfaces-debug-interface-access-sdk"></a>インターフェイス (Debug Interface Access SDK)
メソッドは、目次の各インターフェイスの下にアルファベット順に一覧表示され、Vtable の順序でインターフェイスページに表示されます。

## <a name="in-this-section"></a>このセクションの内容

[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)

DIA SDK がデバッグオブジェクトの仮想および相対仮想アドレスを計算する方法を制御します。

[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)

デバッグシンボルのソースへのアクセスを開始します。

[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)

デバッグデータストリーム内のレコードへのアクセスを提供します。

[IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)

データソースに格納されているさまざまなデバッグストリームを列挙します。

[IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

データソースに格納されているさまざまなフレームデータ要素を列挙します。

[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

データソースに格納されている、挿入されたさまざまなソースを列挙します。

[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

データソースに格納されているさまざまな行番号を列挙します。

[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

データソースに格納されているさまざまなセクションの投稿を列挙します。

[IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

データソースに格納されているさまざまなセグメントを列挙します。

[IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

データソースに格納されているさまざまなソースファイルを列挙します。

[IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)

使用可能なさまざまなスタックフレームを列挙します。

[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

データソースに格納されているさまざまなシンボルを列挙します。

[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)

データソースに格納されているさまざまなシンボルをアドレスで列挙します。

[IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)

データソースに格納されているさまざまなテーブルを列挙します。

[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)

スタックフレームの詳細を公開します。

[IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)

モジュールまたはイメージのベースの位置とメモリオフセットの詳細を公開します。

[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

DIA データソースに格納されているプログラムのソースコードにアクセスします。

[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)

イメージテキストのバイトブロックからソースファイルの行番号へのマッピングプロセスを説明する情報にアクセスします。

[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)

DIA シンボル検索プロシージャからコールバックを受信します。これにより、ユーザーインターフェイスは、場所の試行の進行状況についてレポートすることができます。

[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)

DIA シンボル検索プロシージャからコールバックを受信し、特定のプロセスに制限を適用できるようにします。

[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

DIA プロパティセットの永続的なプロパティを読み取ることができます。

[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)

クライアントアプリケーションが、ファイルの位置によって指定された実行可能ファイルのバイトを提供できるようにします。

[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)

クライアントアプリケーションが、相対仮想アドレスによって指定された実行可能ファイルのバイトを提供できるようにします。

[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)

セクションの貢献度、つまりコンパイル単位によってイメージに対して提供される連続するメモリブロックを記述するデータを取得します。

[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)

セクション番号のデータをアドレス空間のセグメントにマップします。

[IDiaSession](../../debugger/debug-interface-access/idiasession.md)

デバッグシンボルのクエリコンテキストを提供します。

[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)

ソースファイルを表します。

[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)

スタックフレームのプロパティを公開します。

[IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)

PDB ファイルを使用してスタックウォークを実行するメソッドを提供します。

[IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)

[IDiaFrameData:: execute](../../debugger/debug-interface-access/idiaframedata-execute.md)メソッドの呼び出し間でスタックコンテキストを保持します。

[IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)

プログラムデバッグデータベース (PDB) ファイルを使用して、スタックのウォークを容易にします。

[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

シンボルインスタンスのプロパティについて説明します。

[IDiaTable](../../debugger/debug-interface-access/idiatable.md)

DIA データソーステーブルを列挙します。

## <a name="related-sections"></a>関連項目
[列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)

DIA SDK のさまざまなインターフェイスによって使用される列挙体と構造体について説明します。

[定数 (Debug Interface Access SDK)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)

DIA SDK で使用できる定数について説明します。

## <a name="see-also"></a>関連項目

- [参照](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)