---
title: 構造体と共用体 |Microsoft Docs
description: この記事では、Visual Studio デバッグ SDK の構造と共用体のリファレンスについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: c1f477b46083b5abd5b8e93593cc728b660b58d9
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845766"
---
# <a name="structures-and-unions"></a>構造体と共用体
次に示すのは、Visual Studio デバッグ SDK の構造と共用体です。

- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) プロセス ID を指定します。これは、システム ID または GUID のいずれかになります。

- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) ブレークポイントが起動される条件について説明します。

- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 位置、プログラム、スレッドなど、エラーのブレークポイントの解決方法について説明します。

- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) ブレークポイントの位置を示すために使用される構造体の種類を指定します。

- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md) コード内のアドレスのブレークポイントの位置を示すコンポーネントを定義します。

- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md) デバッグ対象のプログラム内のアドレスに直接バインドされているブレークポイントの位置を記述します。

- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md) コードソースファイル内の行のブレークポイントの位置を記述します。

- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) コード内の関数のブレークポイントのオフセット位置を記述します。

- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md) ユーザーが IDE から入力できる文字列に基づいてコードのブレークポイントを設定するために使用されます。

- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md) ユーザーが IDE から入力できる文字列に基づいてデータブレークポイントを設定するために使用されます。

- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md) 特定の位置にあるブレークポイントの解決方法について説明します。

- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 以前に経過した後にブレークポイントが起動される回数と条件について説明します。

- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) ブレークポイントを実装するために必要な情報が含まれています。

- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) ブレークポイントを実装するために必要な情報が含まれています ( [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造と同じですが、ベンダーの GUID、制約、およびトレースポイントの情報が含まれます)。

- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md) コードのブレークポイントの位置を記述します。

- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md) データブレークポイントのバインドの結果について説明します。

- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) コードのブレークポイントまたはデータブレークポイントのバインドされたブレークポイント情報について説明します。

- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) ブレークポイントの解決場所の構造を指定します。

- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md) 文字列の配列を記述します。

- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) メタデータから取得したフィールドの種類に関する情報を指定します。

- [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) 関数またはメソッドの呼び出しを記述します。

- [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md) デバッガーが実行されているコンピューターについて説明します。

- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md) Guid の一覧について説明します。

- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) メモリコンテキストまたはコードコンテキストを記述します。

- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) デバッグ中のプログラムのアドレスを記述します。

- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) さまざまな種類のアドレスのいずれかを表します。

- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) カスタムビューアーまたは型ビジュアライザーを識別します。

- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 名前、型、および値を持つ階層的な性質を持つオブジェクトを示すデバッグプロパティについて説明します。

- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 参照を記述します。

- [Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md) ディスプレイの IDE への逆アセンブリについて説明します。

- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) デバッグ中のプログラムによってスローされた例外または実行時エラーを記述します。

- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) ローカル変数、パラメーター、またはその他のフィールドを記述します。

- [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) スタックフレームについて説明します。

- [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md) 使用可能なデバッグエンジンの一意の識別子の配列を記述します。

- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) モジュールのジャスト Mycode 情報を設定するために使用します。

- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md) 特定のコンピューターについて説明します。

- [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) 配列内の配列要素を記述します。

- [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) クラスまたは構造体のフィールドのアドレスを記述します。

- [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) スコープ内のローカル変数のアドレス (通常は関数またはメソッド) を記述します。

- [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) クラスのメソッドのアドレスを記述します。

- [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) メソッドまたは関数のパラメーターを記述します。

- [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) メソッドまたは関数からの戻り値を記述します。

- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) メタデータから取得したフィールド型を記述します。

- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 特定のモジュール (DLL、EXE、またはアセンブリ) を記述します。

- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 検索されたシンボル検索パスに関するステータス情報を示します。

- [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) ネイティブアドレスを記述します。

- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) PDB シンボルから取得されたフィールド型について説明します。

- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md) コードの場所にバインドする準備ができているブレークポイントの状態を記述します。

- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) プロセスについて説明します。

- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md) プログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの一覧について説明します。

- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) コンピューター上で実行されているプロセスについて説明します。

- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 指定されたテキスト内の行と列の位置を記述します。

- [Threadproperties](../../../extensibility/debugger/reference/threadproperties.md) スレッドのプロパティについて説明します。

- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) フィールドの型について説明します。

- [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) 物理アドレスを記述します。

- [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) ポインターに対する相対アドレス `this` (Visual Basic) を記述し `Me` ます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg .h、sh. h、または ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
