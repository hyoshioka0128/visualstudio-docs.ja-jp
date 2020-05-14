---
title: 構造と共用体 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- structures [Visual Studio SDK]
ms.assetid: 9ff0a8f8-1ee6-4fdd-8b80-206436ff589b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 19d8f547d98488edffc6049be7619e5b5e921d93
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713495"
---
# <a name="structures-and-unions"></a>構造体と共用体
Visual Studio デバッグ SDK の構造体と共用体を次に示します。

- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)プロセス ID を指定します。

- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)ブレークポイントが発生する条件を記述します。

- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)場所、プログラム、スレッドなど、エラー ブレークポイントの解決方法について説明します。

- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)ブレークポイントの場所を記述するために使用する構造体の種類を指定します。

- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)コード内のアドレスでのブレークポイントの位置を記述するコンポーネントを定義します。

- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)デバッグ中のプログラム内のアドレスに直接バインドされているブレークポイントの場所を記述します。

- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)コード ソース ファイルの行にブレークポイントの位置を記述します。

- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)コード内の関数でのブレークポイントのオフセット位置を記述します。

- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)ユーザーが IDE から入力できる文字列に基づいてコード ブレークポイントを設定するために使用します。

- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)ユーザーが IDE から入力できる文字列に基づくデータ ブレークポイントを設定するために使用します。

- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)特定の場所でのブレークポイントの解決方法を説明します。

- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)以前に渡された後にブレークポイントが発生する回数と条件を記述します。

- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)ブレークポイントの実装に必要な情報を格納します。

- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)ブレークポイントの実装に必要な情報[(BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)構造と同じですが、ベンダの GUID、制約、トレース ポイントの情報が含まれます) が含まれます。

- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)コード ブレークポイントの場所を記述します。

- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)データ ブレークポイントをバインドした結果について説明します。

- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)コード ブレークポイントまたはデータ ブレークポイントのバインドされたブレークポイント情報について説明します。

- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)ブレークポイントの解像度の場所の構造を指定します。

- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)文字列の配列を表します。

- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)メタデータから取得したフィールド型に関する情報を指定します。

- [CODE_PATH](../../../extensibility/debugger/reference/code-path.md)関数またはメソッドの呼び出しを記述します。

- [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md)デバッガーが実行されているコンピューターについて説明します。

- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)GUID の一覧について説明します。

- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)メモリ コンテキストまたはコード コンテキストについて説明します。

- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)デバッグ中のプログラムのアドレスを記述します。

- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)さまざまな種類のアドレスの 1 つを表します。

- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)カスタム ビューアーまたは型ビジュアライザーを識別します。

- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)名前、型、および値を持つ階層型のオブジェクトを記述するデバッグ プロパティについて説明します。

- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)参照について説明します。

- [デスタアセンブリデータ](../../../extensibility/debugger/reference/disassemblydata.md)表示用の IDE への逆アセンブリについて説明します。

- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)デバッグ中のプログラムによってスローされる例外または実行時エラーについて説明します。

- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)ローカル変数、パラメーター、またはその他のフィールドを記述します。

- [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md)スタック フレームを表します。

- [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md)使用可能なデバッグ エンジンの一意の識別子の配列について説明します。

- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)モジュールの JustMyCode 情報を設定するために使用します。

- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)特定のコンピュータについて説明します。

- [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)配列内の配列要素を表します。

- [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)クラスまたは構造体のフィールドのアドレスを記述します。

- [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)スコープ内のローカル変数のアドレス (通常は関数またはメソッド) を記述します。

- [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)クラスのメソッドのアドレスを記述します。

- [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)メソッドまたは関数のパラメーターを記述します。

- [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)メソッドまたは関数からの戻り値を表します。

- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)メタデータから取得されるフィールド型を表します。

- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)特定のモジュール (DLL、EXE、またはアセンブリ) について説明します。

- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)検索されたシンボル検索パスに関する状態情報を示します。

- [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)ネイティブ アドレスを表します。

- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)PDB シンボルから取得されるフィールド型を表します。

- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)コードの場所にバインドする準備ができたブレークポイントの状態を記述します。

- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)プロセスについて説明します。

- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)プログラム ノードを表す[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトの一覧について説明します。

- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)コンピュータ上で実行されているプロセスについて説明します。

- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)指定されたテキストの行と列の位置を記述します。

- [スレッドプロパティ](../../../extensibility/debugger/reference/threadproperties.md)スレッドのプロパティを記述します。

- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)フィールドの型を表します。

- [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)物理アドレスを記述します。

- [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)`this`ポインターに対する相対アドレスを記述します (`Me` Visual Basic で) 。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h、sh.h、または ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
