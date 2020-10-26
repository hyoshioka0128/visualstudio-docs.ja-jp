---
title: IDiaSymbol |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol interface
ms.assetid: 01ad328a-736c-4933-a9f8-c2ded19ddd8c
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7c9b267893bacef8c9126b1a17b4eb444af6a1dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65692886"
---
# <a name="idiasymbol"></a>IDiaSymbol
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルインスタンスのプロパティについて説明します。  
  
## <a name="syntax"></a>構文  
  
```  
IDiaSymbol : IUnknown  
```  
  
## <a name="methods-in-alphabetical-order"></a>アルファベット順のメソッド  
 次の表に、のメソッドを示し `IDiaSymbol` ます。  
  
> [!NOTE]
> シンボルは、シンボルの種類に応じて、これらのメソッドの一部に対してのみ意味のあるデータを返します。 メソッドからが返さ `S_OK` れた場合、そのメソッドは意味のあるデータを返しました。  
  
|Method|説明|  
|------------|-----------------|  
|[IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)|記号のすべての子を取得します。|  
|[IDiaSymbol::findChildrenEx](../../debugger/debug-interface-access/idiasymbol-findchildrenex.md)|記号の子を取得します。 このメソッドは、 [IDiaSymbol:: findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)の拡張バージョンです。|  
|[IDiaSymbol::findChildrenExByAddr](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyaddr.md)|指定されたアドレスで有効なシンボルの子を取得します。|  
|[IDiaSymbol::findChildrenExByRVA](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyrva.md)|指定した相対仮想アドレス (RVA) で有効なシンボルの子を取得します。|  
|[IDiaSymbol::findChildrenExByVA](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyva.md)|指定した仮想アドレスで有効なシンボルの子を取得します。|  
|[IDiaSymbol::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyaddr.md)|指定されたアドレスのすべてのインラインフレームをクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSymbol::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyrva.md)|指定した相対仮想アドレス (RVA) のすべてのインラインフレームをクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSymbol::findInlineFramesByVA](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyva.md)|指定された仮想アドレス (VA) 上のすべてのインラインフレームをクライアントが反復処理できるようにする列挙を取得します。|  
|[IDiaSymbol::findInlineeLines](../../debugger/debug-interface-access/idiasymbol-findinlineelines.md)|このシンボルで直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSymbol::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyaddr.md)|クライアントが、指定されたアドレス範囲内のこのシンボルに直接または間接的にインライン化されているすべての関数の行番号情報を反復処理できるようにする列挙体を取得します。|  
|[IDiaSymbol::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyrva.md)|クライアントが、指定された相対仮想アドレス (RVA) 内のこのシンボルに直接または間接的にインライン化されているすべての関数の行番号情報を反復処理できるようにする列挙体を取得します。|  
|[IDiaSymbol::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyva.md)|指定した仮想アドレス (VA) 内のこのシンボルに直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙体を取得します。|  
|[IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasymbol-findsymbolsbyrvaforacceleratorpointertag.md)|対応するタグ値が指定されている場合、このメソッドは、指定された相対仮想アドレスで、このスタブ関数に含まれるシンボルの列挙体を返します。|  
|[IDiaSymbol::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasymbol-findsymbolsforacceleratorpointertag.md)|C++ AMP スタブ関数内のアクセラレータポインタータグの数を返します。|  
|[IDiaSymbol::get_acceleratorPointerTags](../../debugger/debug-interface-access/idiasymbol-get-acceleratorpointertags.md)|C++ AMP accelerator スタブ関数に対応するすべてのアクセラレータポインタータグ値を返します。|  
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|クラスメンバーのアクセス修飾子を取得します。|  
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|アドレスの場所のオフセット部分を取得します。|  
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|アドレスの場所のセクション部分を取得します。|  
|[IDiaSymbol::get_addressTaken](../../debugger/debug-interface-access/idiasymbol-get-addresstaken.md)|別のシンボルがこのアドレスを参照しているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|プログラムデータベースの age 値を取得します。|  
|[IDiaSymbol::get_arrayIndexType](../../debugger/debug-interface-access/idiasymbol-get-arrayindextype.md)|配列インデックス型のシンボル識別子を取得します。|  
|[IDiaSymbol::get_arrayIndexTypeId](../../debugger/debug-interface-access/idiasymbol-get-arrayindextypeid.md)|シンボルの配列インデックスの型識別子を取得します。|  
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|バックエンドメジャーバージョン番号を取得します。|  
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|バックエンドのマイナーバージョン番号を取得します。|  
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|バックエンドのビルド番号を取得します。|  
|[IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)|基本データオフセットを取得します。|  
|[IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)|基本データスロットを取得します。|  
|[IDiaSymbol::get_baseSymbol](../../debugger/debug-interface-access/idiasymbol-get-basesymbol.md)|ポインターの基になる記号を取得します。|  
|[IDiaSymbol::get_baseSymbolId](../../debugger/debug-interface-access/idiasymbol-get-basesymbolid.md)|ポインターの基になるシンボル ID を取得します。|  
|[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)|単純型の型タグを取得します。|  
|[IDiaSymbol::get_bitPosition](../../debugger/debug-interface-access/idiasymbol-get-bitposition.md)|位置のビット位置を取得します。|  
|[IDiaSymbol::get_builtInKind](../../debugger/debug-interface-access/idiasymbol-get-builtinkind.md)|HLSL 型の組み込みの種類を取得します。|  
|[IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)|メソッドの呼び出し規約を示すインジケーターを返します。|  
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|シンボルの親クラスへの参照を取得します。|  
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|シンボルのクラス親識別子を取得します。|  
|[IDiaSymbol::get_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|シンボルがコードアドレスを参照しているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_compilerGenerated](../../debugger/debug-interface-access/idiasymbol-get-compilergenerated.md)|シンボルがコンパイラによって生成されたかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|[コンパイル単位](../../debugger/debug-interface-access/compiland.md)の作成に使用されるコンパイラの名前を取得します。|  
|[IDiaSymbol::get_constructor](../../debugger/debug-interface-access/idiasymbol-get-constructor.md)|ユーザー定義データ型にコンストラクターがあるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_container](../../debugger/debug-interface-access/idiasymbol-get-container.md)|この記号の格納記号を取得します。|  
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|ユーザー定義データ型が定数であるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_count](../../debugger/debug-interface-access/idiasymbol-get-count.md)|リストまたは配列内の項目の数を取得します。|  
|[IDiaSymbol::get_countLiveRanges](../../debugger/debug-interface-access/idiasymbol-get-countliveranges.md)|ローカルシンボルに関連付けられている有効なアドレス範囲の数を取得します。|  
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|関数がカスタム呼び出し規約を使用するかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_dataBytes](../../debugger/debug-interface-access/idiasymbol-get-databytes.md)|OEM シンボルのデータバイトを取得します。|  
|[IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)|データシンボルの変数分類を取得します。|  
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|コンパイルされたプログラムまたは単位のエディットコンティニュ機能を記述するフラグを取得します。|  
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|関数が遠くの戻り値を使用するかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|フロントエンドメジャーバージョン番号を取得します。|  
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|フロントエンドのマイナーバージョン番号を取得します。|  
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|フロントエンドのビルド番号を取得します。|  
|[IDiaSymbol::get_function](../../debugger/debug-interface-access/idiasymbol-get-function.md)|パブリックシンボルが関数を参照しているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|シンボルの GUID を取得します。|  
|[IDiaSymbol::get_hasAlloca](../../debugger/debug-interface-access/idiasymbol-get-hasalloca.md)|関数にの呼び出しが含まれているかどうかを示すフラグを取得 `alloca` します。|  
|[IDiaSymbol::get_hasAssignmentOperator](../../debugger/debug-interface-access/idiasymbol-get-hasassignmentoperator.md)|ユーザー定義データ型に代入演算子が定義されているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasCastOperator](../../debugger/debug-interface-access/idiasymbol-get-hascastoperator.md)|ユーザー定義データ型にキャスト演算子が定義されているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|コンパイル単位にデバッグ情報が含まれているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasEH](../../debugger/debug-interface-access/idiasymbol-get-haseh.md)|関数に C++ スタイルの例外ハンドラーがあるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasEHa](../../debugger/debug-interface-access/idiasymbol-get-haseha.md)|関数に非同期例外ハンドラーがあるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasInlAsm](../../debugger/debug-interface-access/idiasymbol-get-hasinlasm.md)|関数にインラインアセンブリがあるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)|関数に longjmp コマンド (C スタイルの例外処理の一部) が含まれているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|モジュールにマネージコードが含まれているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasNestedTypes](../../debugger/debug-interface-access/idiasymbol-get-hasnestedtypes.md)|ユーザー定義データ型に入れ子になった型定義があるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|関数またはコンパイル単位が ( [/gs (Buffer Security Check)](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e) コンパイラスイッチを使用して) でコンパイルされたセキュリティチェックを持っているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasSEH](../../debugger/debug-interface-access/idiasymbol-get-hasseh.md)|関数に Win32 スタイルの構造化例外処理があるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)|関数に setjmp コマンドが含まれているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_indirectVirtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-indirectvirtualbaseclass.md)|ユーザー定義データ型が間接仮想基底クラスであるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_InlSpec](../../debugger/debug-interface-access/idiasymbol-get-inlspec.md)|関数がインライン属性でマークされているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|関数に割り込み命令からの戻り値があるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|関数が基底クラスの仮想関数であるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isAcceleratorGroupSharedLocal](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorgroupsharedlocal.md)|シンボルが C++ AMP Accelerator 用にコンパイルされたコード内のグループ共有ローカル変数に対応するかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isAcceleratorPointerTagLiveRange](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorpointertagliverange.md)|シンボルが C++ AMP Accelerator 用にコンパイルされたコード内のポインター変数のタグコンポーネントの *定義範囲シンボル* に対応するかどうかを示すフラグを取得します。 定義範囲シンボルは、アドレスの範囲の変数の場所です。|  
|[IDiaSymbol::get_isAcceleratorStubFunction](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorstubfunction.md)|呼び出しに対応するアクセラレータ用にコンパイルされたシェーダーの、シンボルがトップレベルの関数シンボルに対応するかどうかを示し `parallel_for_each` ます。|  
|[IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)|データが多数の記号の集計の一部であるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|シンボルファイルに C 型が含まれているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|モジュールが共通中間言語 (CIL) からネイティブコードに変換されたかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|ユーザー定義データ型の要素が特定の境界に合わせてアラインされているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isHLSLData](../../debugger/debug-interface-access/idiasymbol-get-ishlsldata.md)|このシンボルが、High Level Shader Language (HLSL) データを表すかどうかを指定します。|  
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|モジュールが [/hotpatch (Create Hotpatchable Image)](https://msdn.microsoft.com/library/aad539b6-c053-4c78-8682-853d98327798) コンパイラスイッチを使用してコンパイルされたかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|マネージコンパイル単位がリンカーの LTCG にリンクされているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isMatrixRowMajor](../../debugger/debug-interface-access/idiasymbol-get-ismatrixrowmajor.md)|マトリックスが行メジャーであるかどうかを指定します。|  
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|マネージコンパイル単位が .netmodule (メタデータのみを含む) かどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isMultipleInheritance](../../debugger/debug-interface-access/idiasymbol-get-ismultipleinheritance.md)|`this`複数の継承を持つデータメンバーをポインターが指しているかどうかを指定します。|  
|[IDiaSymbol::get_isNaked](../../debugger/debug-interface-access/idiasymbol-get-isnaked.md)|関数に [生](https://msdn.microsoft.com/library/69723241-05e1-439b-868e-20a83a16ab6d) の属性があるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isOptimizedAway](../../debugger/debug-interface-access/idiasymbol-get-isoptimizedaway.md)|変数を最適化するかどうかを指定します。|  
|[IDiaSymbol::get_isPointerBasedOnSymbolValue](../../debugger/debug-interface-access/idiasymbol-get-ispointerbasedonsymbolvalue.md)|`this`ポインターがシンボル値に基づいているかどうかを指定します。|  
|[IDiaSymbol::get_isPointerToDataMember](../../debugger/debug-interface-access/idiasymbol-get-ispointertodatamember.md)|このシンボルがデータメンバーへのポインターであるかどうかを指定します。|  
|[IDiaSymbol::get_isPointerToMemberFunction](../../debugger/debug-interface-access/idiasymbol-get-ispointertomemberfunction.md)|このシンボルがメンバー関数へのポインターであるかどうかを指定します。|  
|[IDiaSymbol::get_isReturnValue](../../debugger/debug-interface-access/idiasymbol-get-isreturnvalue.md)|変数が戻り値を格納するかどうかを指定します。|  
|[IDiaSymbol::get_isSdl](../../debugger/debug-interface-access/idiasymbol-get-issdl.md)|/SDL オプションを使用してモジュールをコンパイルするかどうかを指定します。|  
|[IDiaSymbol::get_isSingleInheritance](../../debugger/debug-interface-access/idiasymbol-get-issingleinheritance.md)|`this`ポインターが1つの継承を持つデータメンバーを指しているかどうかを指定します。|  
|[IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)|データが個別のシンボルの集計に分割されているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|関数またはサンクレイヤーが静的かどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|プライベートシンボルがシンボルファイルから削除されているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_isVirtualInheritance](../../debugger/debug-interface-access/idiasymbol-get-isvirtualinheritance.md)|`this`ポインターが仮想継承を持つデータメンバーを指しているかどうかを指定します。|  
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|ソースの言語を取得します。|  
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|このシンボルによって表されるオブジェクトによって使用されるメモリのバイト数を取得します。|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|記号の構文上の親への参照を取得します。|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|記号の字句親識別子を取得します。|  
|[IDiaSymbol::get_libraryName](../../debugger/debug-interface-access/idiasymbol-get-libraryname.md)|オブジェクトが読み込まれたライブラリまたはオブジェクトファイルのファイル名を取得します。|  
|[IDiaSymbol::get_liveRangeLength](../../debugger/debug-interface-access/idiasymbol-get-liverangelength.md)|ローカルシンボルが有効なアドレス範囲の長さを返します。|  
|[IDiaSymbol::get_liveRangeStartAddressSection](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddresssection.md)|ローカルシンボルが有効な開始アドレス範囲のセクション部分を返します。|  
|[IDiaSymbol::get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md)|ローカルシンボルが有効な開始アドレス範囲のオフセット部分を返します。|  
|[IDiaSymbol::get_liveRangeStartRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-liverangestartrelativevirtualaddress.md)|ローカルシンボルが有効なアドレス範囲の先頭を返します。|  
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|データシンボルの場所の種類を取得します。|  
|[IDiaSymbol::get_lowerBound](../../debugger/debug-interface-access/idiasymbol-get-lowerbound.md)|FORTRAN 配列次元の下限を取得します。|  
|[IDiaSymbol::get_lowerBoundId](../../debugger/debug-interface-access/idiasymbol-get-lowerboundid.md)|FORTRAN 配列次元の下限のシンボル識別子を取得します。|  
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|ターゲット CPU の種類を取得します。|  
|[IDiaSymbol::get_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|シンボルがマネージコードを参照するかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_memorySpaceKind](../../debugger/debug-interface-access/idiasymbol-get-memoryspacekind.md)|メモリ領域の種類を取得します。|  
|[IDiaSymbol::get_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|シンボルが Microsoft 中間言語 (MSIL) コードを参照しているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|記号の名前を取得します。|  
|[IDiaSymbol::get_nested](../../debugger/debug-interface-access/idiasymbol-get-nested.md)|ユーザー定義データ型が入れ子になっているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|関数が [noinline](https://msdn.microsoft.com/library/f259d55b-dec7-4bde-8cf9-14521e4fdc42) 属性でマークされているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|[Noreturn](https://msdn.microsoft.com/library/9c6517e5-22d7-4051-9974-3d2200ae4d1d)属性を使用して関数が宣言されているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_noStackOrdering](../../debugger/debug-interface-access/idiasymbol-get-nostackordering.md)|スタックバッファーチェックの一部としてスタックの順序付けを実行できなかったかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|関数またはラベルに到達していないかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_numberOfAcceleratorPointerTags](../../debugger/debug-interface-access/idiasymbol-get-numberofacceleratorpointertags.md)|C++ AMP スタブ関数内のアクセラレータポインタータグの数を返します。|  
|[IDiaSymbol::get_numberOfModifiers](../../debugger/debug-interface-access/idiasymbol-get-numberofmodifiers.md)|元の型に適用される修飾子の数を取得します。|  
|[IDiaSymbol::get_numberOfRegisterIndices](../../debugger/debug-interface-access/idiasymbol-get-numberofregisterindices.md)|レジスタインデックスの数を取得します。|  
|[IDiaSymbol::get_numberOfRows](../../debugger/debug-interface-access/idiasymbol-get-numberofrows.md)|行列内の行の数を取得します。|  
|[IDiaSymbol::get_numberOfColumns](../../debugger/debug-interface-access/idiasymbol-get-numberofcolumns.md)|行列内の列の数を取得します。|  
|[IDiaSymbol::get_objectFileName](../../debugger/debug-interface-access/idiasymbol-get-objectfilename.md)|オブジェクトファイル名を取得します。|  
|[IDiaSymbol::get_objectPointerType](../../debugger/debug-interface-access/idiasymbol-get-objectpointertype.md)|クラスメソッドのオブジェクトポインターの型を取得します。|  
|[IDiaSymbol::get_oemId](../../debugger/debug-interface-access/idiasymbol-get-oemid.md)|シンボルの値を取得 `oemId` します。|  
|[IDiaSymbol::get_oemSymbolId](../../debugger/debug-interface-access/idiasymbol-get-oemsymbolid.md)|シンボルの値を取得 `oemSymbolId` します。|  
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|シンボルの場所のオフセットを取得します。|  
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|関数またはラベルに最適化されたコードとデバッグ情報が含まれているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_overloadedOperator](../../debugger/debug-interface-access/idiasymbol-get-overloadedoperator.md)|ユーザー定義データ型にオーバーロードされた演算子があるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_packed](../../debugger/debug-interface-access/idiasymbol-get-packed.md)|ユーザー定義データ型がパックされているかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|プログラムまたはコンパイル単位がコンパイルされたプラットフォームの種類を取得します。|  
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|関数が純粋仮想であるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_rank](../../debugger/debug-interface-access/idiasymbol-get-rank.md)|FORTRAN 多次元配列のランクを取得します。|  
|[IDiaSymbol::get_reference](../../debugger/debug-interface-access/idiasymbol-get-reference.md)|ポインター型が参照であるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_registerId](../../debugger/debug-interface-access/idiasymbol-get-registerid.md)|場所のレジスタ指定子を取得します。|  
|[IDiaSymbol::get_registerType](../../debugger/debug-interface-access/idiasymbol-get-registertype.md)|レジスタの種類を取得します。|  
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|場所の相対仮想アドレス (RVA) を取得します。|  
|[IDiaSymbol::get_restrictedType](../../debugger/debug-interface-access/idiasymbol-get-restrictedtype.md)|ポインターに制限付きのフラグを設定するかどうかを指定し `this` ます。|  
|[IDiaSymbol::get_samplerSlot](../../debugger/debug-interface-access/idiasymbol-get-samplerslot.md)|サンプラースロットを取得します。|  
|[IDiaSymbol::get_scoped](../../debugger/debug-interface-access/idiasymbol-get-scoped.md)|非グローバル構文のスコープにユーザー定義データ型が表示されるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|シンボルの署名値を取得します。|  
|[IDiaSymbol::get_sizeInUdt](../../debugger/debug-interface-access/idiasymbol-get-sizeinudt.md)|ユーザー定義型のメンバーのサイズを取得します。|  
|[IDiaSymbol::get_slot](../../debugger/debug-interface-access/idiasymbol-get-slot.md)|位置のスロット番号を取得します。|  
|[IDiaSymbol::get_sourceFileName](../../debugger/debug-interface-access/idiasymbol-get-sourcefilename.md)|ソースファイルのファイル名を取得します。|  
|[IDiaSymbol::getSrcLineOnTypeDefn](../../debugger/debug-interface-access/idiasymbol-getsrclineontypedefn.md)|指定されたユーザー定義型が定義されている場所を示すソースファイルと行番号を取得します。|  
|[IDiaSymbol::get_stride](../../debugger/debug-interface-access/idiasymbol-get-stride.md)|行列またはストライプ配列のストライドを取得します。|  
|[IDiaSymbol::get_subType](../../debugger/debug-interface-access/idiasymbol-get-subtype.md)|サブタイプを取得します。|  
|[IDiaSymbol::get_subTypeId](../../debugger/debug-interface-access/idiasymbol-get-subtypeid.md)|サブタイプ ID を取得します。|  
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|シンボルが読み込まれたファイルの名前を取得します。|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|一意のシンボル識別子を取得します。|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|シンボルの種類の分類子を取得します。|  
|[IDiaSymbol::get_targetOffset](../../debugger/debug-interface-access/idiasymbol-get-targetoffset.md)|サンクターゲットのオフセットセクションを取得します。|  
|[IDiaSymbol::get_targetRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetrelativevirtualaddress.md)|サンクターゲットの相対仮想アドレス (RVA) を取得します。|  
|[IDiaSymbol::get_targetSection](../../debugger/debug-interface-access/idiasymbol-get-targetsection.md)|サンクターゲットのアドレスセクションを取得します。|  
|[IDiaSymbol::get_targetVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetvirtualaddress.md)|サンクターゲットの仮想アドレス (VA) を取得します。|  
|[IDiaSymbol::get_textureSlot](../../debugger/debug-interface-access/idiasymbol-get-textureslot.md)|テクスチャスロットを取得します。|  
|[IDiaSymbol::get_thisAdjust](../../debugger/debug-interface-access/idiasymbol-get-thisadjust.md)|メソッドの論理 adjustor を取得し `this` ます。|  
|[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)|関数のサンク型を取得します。|  
|[IDiaSymbol::get_timeStamp](../../debugger/debug-interface-access/idiasymbol-get-timestamp.md)|基になる実行可能ファイルのタイムスタンプを取得します。|  
|[IDiaSymbol::get_token](../../debugger/debug-interface-access/idiasymbol-get-token.md)|マネージ関数または変数のメタデータトークンを取得します。|  
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|関数シグネチャへの参照を取得します。|  
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|シンボルの型識別子を取得します。|  
|[IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)|このシンボルのコンパイラ固有の型値の配列を取得します。|  
|[IDiaSymbol::get_typeIds](../../debugger/debug-interface-access/idiasymbol-get-typeids.md)|このシンボルのコンパイラ固有の型識別子の値の配列を取得します。|  
|[IDiaSymbol::get_uavSlot](../../debugger/debug-interface-access/idiasymbol-get-uavslot.md)|Uav スロットを取得します。|  
|[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)|さまざまなユーザー定義型 (UDT) を取得します。|  
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|ユーザー定義データ型が整列されていないかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|C++ の修飾名 (リンケージ) の装飾されていない名前を取得します。|  
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`get_undecoratedName`拡張フィールドの値に基づいて装飾されていない名前を取得するメソッドの拡張。|  
|[IDiaSymbol::get_unmodifiedTypeId](../../debugger/debug-interface-access/idiasymbol-get-unmodifiedtypeid.md)|元の (変更されていない) 型の ID を取得します。|  
|[IDiaSymbol::get_upperBound](../../debugger/debug-interface-access/idiasymbol-get-upperbound.md)|FORTRAN 配列次元の上限を取得します。|  
|[IDiaSymbol::get_upperBoundId](../../debugger/debug-interface-access/idiasymbol-get-upperboundid.md)|FORTRAN 配列次元の上限のシンボル識別子を取得します。|  
|[IDiaSymbol::get_value](../../debugger/debug-interface-access/idiasymbol-get-value.md)|定数の値を取得します。|  
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|関数が仮想であるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|場所の仮想アドレス (VA) を取得します。|  
|[IDiaSymbol::get_virtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseclass.md)|ユーザー定義データ型が仮想基底クラスであるかどうかを示すフラグを取得します。|  
|[IDiaSymbol::get_virtualBaseDispIndex](../../debugger/debug-interface-access/idiasymbol-get-virtualbasedispindex.md)|仮想ベースのディスプレイスメントテーブルへのインデックスを取得します。|  
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|仮想関数の仮想関数テーブル内のオフセットを取得します。|  
|[IDiaSymbol::get_virtualBasePointerOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbasepointeroffset.md)|仮想基本ポインターのオフセットを取得します。|  
|[IDiaSymbol::get_virtualBaseTableType](../../debugger/debug-interface-access/idiasymbol-get-virtualbasetabletype.md)|仮想ベーステーブルポインターの型を取得します。|  
|[IDiaSymbol::get_virtualTableShape](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshape.md)|ユーザー定義型の仮想テーブルの型のシンボルインターフェイスを取得します。|  
|[IDiaSymbol::get_virtualTableShapeId](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshapeid.md)|シンボルの仮想テーブル図形の識別子を取得します。|  
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|ユーザー定義データ型が volatile であるかどうかを示すフラグを取得します。|  
  
## <a name="remarks"></a>解説  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスを取得するには、次のいずれかのメソッドを呼び出します。  
  
- [IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)  
  
- [IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)  
  
- [IDiaEnumSymbolsByAddr::Next](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-next.md)  
  
- [IDiaEnumSymbolsByAddr::Prev](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-prev.md)  
  
- [IDiaEnumSymbolsByAddr::symbolByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyaddr.md)  
  
- [IDiaEnumSymbolsByAddr::symbolByRVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyrva.md)  
  
- [IDiaEnumSymbolsByAddr::symbolByVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyva.md)  
  
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)  
  
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)  
  
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)  
  
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)  
  
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)  
  
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)  
  
- [IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)  
  
- [IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)  
  
- [IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)  
  
## <a name="example"></a>例  
 この例では、特定の相対仮想アドレスで関数のローカル変数を表示する方法を示します。 また、異なる型のシンボルが相互にどのように関連付けられているかも示します。  
  
> [!NOTE]
> `CDiaBSTR` は、をラップし、 `BSTR` インスタンス化がスコープ外になったときに文字列の解放を自動的に処理するクラスです。  
  
```cpp#  
void DumpLocalVars( DWORD rva, IDiaSession *pSession )  
{  
    CComPtr< IDiaSymbol > pBlock;  
    if ( FAILED( psession->findSymbolByRVA( rva, SymTagBlock, &pBlock ) ) )  
    {  
        Fatal( "Failed to find symbols by RVA" );  
    }  
    CComPtr< IDiaSymbol > pscope;  
    for ( ; pBlock != NULL; )  
    {  
        CComPtr< IDiaEnumSymbols > pEnum;  
        // local data search  
        if ( FAILED( pBlock->findChildren( SymTagNull, NULL, nsNone, &pEnum ) ) )  
        {  
            Fatal( "Local scope findChildren failed" );  
        }  
        CComPtr< IDiaSymbol > pSymbol;  
        DWORD tag;  
        DWORD celt;  
        while ( pEnum != NULL &&  
                SUCCEEDED( pEnum->Next( 1, &pSymbol, &celt ) ) &&  
                celt == 1)  
        {  
            pSymbol->get_symTag( &tag );  
            if ( tag == SymTagData )  
            {  
                CDiaBSTR name;  
                DWORD    kind;  
                pSymbol->get_name( &name );  
                pSymbol->get_dataKind( &kind );  
                if ( name != NULL )  
                    wprintf_s( L"\t%s (%s)\n", name, szDataKinds[ kind ] );  
            }  
            else if ( tag == SymTagAnnotation )  
            {  
                CComPtr< IDiaEnumSymbols > pValues;  
                // local data search  
                wprintf_s( L"\tAnnotation:\n" );  
                if ( FAILED( pSymbol->findChildren( SymTagNull, NULL, nsNone, &pValues ) ) )  
                    Fatal( "Annotation findChildren failed" );  
                pSymbol = NULL;  
                while ( pValues != NULL &&  
                        SUCCEEDED( pValues->Next( 1, &pSymbol, &celt ) ) &&  
                        celt == 1 )  
                {  
                    CComVariant value;  
                    if ( pSymbol->get_value( &value ) != S_OK )  
                        Fatal( "No value for annotation data." );  
                    wprintf_s( L"\t\t%ws\n", value.bstrVal );  
                    pSymbol = NULL;  
                }  
            }  
            pSymbol = NULL;  
        }  
        pBlock->get_symTag( &tag );   
        if ( tag == SymTagFunction )    // stop when at function scope  
            break;  
        // move to lexical parent  
        CComPtr< IDiaSymbol > pParent;  
        if ( SUCCEEDED( pBlock->get_lexicalParent( &pParent ) )  
            && pParent != NULL ) {  
            pBlock = pParent;  
        }  
        else  
        {  
            Fatal( "Finding lexical parent failed." );  
        }  
    };  
}  
```  
  
## <a name="requirements"></a>必要条件  
 `Header:` Dia2  
  
 ライブラリ: diaguids  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>参照  
 [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)   
 [シンボルとシンボルタグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)   
 [コンパイル単位](../../debugger/debug-interface-access/compiland.md)
