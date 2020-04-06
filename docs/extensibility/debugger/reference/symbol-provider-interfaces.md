---
title: シンボル プロバイダー インターフェイス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- interfaces, symbol handler
- symbol handler, interfaces
- symbol handler, evaluating variables
ms.assetid: 4201f10e-c9f7-4b38-bb45-40fe0082d5bf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7929ba36c76f0db1cabab087afe3590de509efff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715850"
---
# <a name="symbol-provider-interfaces"></a>シンボル プロバイダーのインターフェイス
以下は、 のシンボル処理インターフェイスです[!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)]。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、中断モード中にコール スタック内の変数を評価するために使用されます。 これらは、共通言語ランタイムシンボルプロバイダー (SP) に対してのみ実装されます。

|インターフェイス|によって実装される|説明|
|---------------|--------------------|-----------------|
|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)|SP|アイテムのアドレスを表します。|
|[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)|SP|プロセス ID へのアクセスを提供する項目のアドレスを表します。|
|[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)|SP|配列のシンボルまたは配列の型を表します。|
|[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)|SP|クラス シンボルまたはクラス型を表します。|
|[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)|SP|マネージ コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表します。|
|[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)|SP|マネージ コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表し **、IDebugComPlus シンボル プロバイダー**を拡張します。|
|[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)|SP|他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。|
|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)|SP|シンボルにアタッチできるカスタム属性を表します。|
|[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)|SP|メソッドまたは型のカスタム属性のクエリを表します。|
|[IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)|SP|シンボルのカスタム属性へのアクセスを提供します。|
|[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)|SP|実行時に決定できる任意の型の基本インターフェイス。|
|[IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)|SP|オブジェクトの動的フィールド[を](../../../extensibility/debugger/reference/idebugbinder.md)表します。|
|[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)|SP|列挙型を表します。|
|[IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)|Sp|マネージ コード ジェネリックをサポートするために、使用可能なフィールドの型を拡張します。|
|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)|SP|すべてのフィールドの基本クラス。は、シンボルまたは型の説明を表します。|
|[IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)|SP|マネージ コードジェネリック型のフィールドの定義を表します。|
|[IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)|SP|マネージ コードジェネリック型のフィールドのインスタンスを表します。|
|[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)|SP|マネージ コードのジェネリック型のパラメーターを表します。|
|[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)|SP|メソッドを表します。|
|[IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)|SP|デバッグオプション修飾子を表します。|
|[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)|SP|ポインターを表します。|
|[IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)|SP|[インターフェイスから](../../../extensibility/debugger/reference/idebugfield.md)プリミティブ型列挙値を表します。|
|[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)|SP|取得または設定できるマネージ コード クラスのプロパティを表します。|
|[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)|SP|シンボルと型を提供するシンボル プロバイダーを表します。|
|[IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)|SP|メタデータとコア シンボル インターフェイスに直接アクセスできるシンボル プロバイダーを表します。|
|[IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)|SP|型を表すフィールドを作成する機能を表します。|
|[IDebugTypeFieldBuilder2](../../../extensibility/debugger/reference/idebugtypefieldbuilder2.md)|SP|配列型を作成できるように**IDebugTypeFieldBuilder**を拡張します。|
|[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)|SP|オブジェクトのコレクション[を](../../../extensibility/debugger/reference/idebugaddress.md)表します。|
|[IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)|SP|オブジェクトのコレクション[を](../../../extensibility/debugger/reference/idebugcustomattribute.md)表します。|
|[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)|SP|[オブジェクトの](../../../extensibility/debugger/reference/idebugfield.md)コレクションを表します。|

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
