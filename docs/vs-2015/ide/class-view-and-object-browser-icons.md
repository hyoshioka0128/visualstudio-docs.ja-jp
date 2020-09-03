---
title: '[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- icons, in Object Browser
- signal icons
- Class View tool, symbols
- graphic symbols
- IntelliSense, icons
- icons, IntelliSense
- symbols, Object Browser icons
- Object Browser, icons in Class View
ms.assetid: 58cc3f44-c296-4a88-a008-09d28598d9c0
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e67763234ff7b3778cccabaed45fbbc0bc04d30
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72620483"
---
# <a name="class-view-and-object-browser-icons"></a>[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

クラスビュー * * と **オブジェクトブラウザー** には、名前空間、クラス、関数、変数などのコードエンティティを表すアイコンが表示されます。 各アイコンおよびその説明を次の表に示します。

|アイコン|説明|アイコン|説明|
|----------|-----------------|----------|-----------------|
|![名前空間シンボル](../ide/media/vxnamespace-icon.gif "vxNamespace_Icon")|名前空間|![宣言シンボル](../ide/media/vxmethod-icon.gif "vxMethod_Icon")|メソッドまたは関数|
|![クラス アイコン](../ide/media/vxclass-icon.gif "vxClass_Icon")|クラス|![演算子シンボル](../ide/media/vxoperator-icon.gif "vxOperator_Icon")|演算子|
|![ロリポップ インターフェイス シンボル](../ide/media/vxinterface-icon.gif "vxInterface_Icon")|Interface|![プロパティ シンボル](../ide/media/vxproperty-icon.gif "vxProperty_Icon")|プロパティ|
|![構造体シンボル](../ide/media/vxstruct-icon.gif "vxStruct_Icon")|構造体|![フィールド アイコン](../ide/media/vxfield-icon.gif "vxField_Icon")|フィールドまたは変数|
|![共用体シンボル](../ide/media/vxunion-icon.gif "vxUnion_Icon")|和集合|![イベント シンボル](../ide/media/vxevent-icon.gif "vxEvent_Icon")|event|
|![一覧表示シンボル](../ide/media/vxenum-icon.gif "vxEnum_Icon")|Enum|![定数アイコン](../ide/media/vxconstant-icon.gif "vxConstant_Icon")|定数|
|![型定義シンボル](../ide/media/vxtypedef-icon.gif "vxTypeDef_Icon")|TypeDef|![項目の一覧表示シンボル](../ide/media/vxenumitem-icon.gif "vxEnumItem_Icon")|列挙型項目|
|![Visual Studio モジュール シンボル](../ide/media/vxmodule-icon.gif "vxModule_Icon")|Module|![マップ項目シンボル](../ide/media/vxmapitem-icon.gif "vxMapItem_Icon")|マップ項目|
|![拡張メソッド シンボル](../ide/media/extensionmethod.gif "ExtensionMethod")|拡張メソッド|![宣言シンボル](../ide/media/vxmethod-icon.gif "vxMethod_Icon")|外部宣言|
|![デリゲート シンボル](../ide/media/vxdelegate-icon.gif "vxDelegate_Icon")|Delegate|![クラス ビューおよびオブジェクト ブラウザーのエラー アイコン](../ide/media/erroricon.gif "ErrorIcon")|Error|
|![例外シンボル](../ide/media/vxexception-icon.gif "vxException_Icon")|例外|![テンプレート シンボル](../ide/media/vxtemplate-icon.gif "vxTemplate_Icon")|テンプレート|
|![マップ シンボル](../ide/media/vxmap-icon.gif "vxMap_Icon")|マップ|![エラー感嘆符シンボル](../ide/media/vxerror-icon.gif "vxError_Icon")|不明|
|![型転送シンボル](../ide/media/ob-type-forward.gif "ob_type_forward")|型の転送|||

## <a name="signal-icons"></a>シグナル アイコン
 次のシグナル アイコンは、上記のアイコンすべてに適用され、そのアクセシビリティを示します。

> [!NOTE]
> プロジェクトがソース管理データベースに含まれている場合は、ソース管理のステータス (チェックインまたはチェックアウトなど) を示すシグナル アイコンが追加で表示されることがあります。

|アイコン|説明|
|----------|-----------------|
|\<No Signal Icon>|パブリック。 このコンポーネント内のどこからでも、また、それを参照するどのコンポーネントからでもアクセスできます。|
|![シグナル プロテクト シンボル](../ide/media/vxsignal-icon-key.gif "vxSignal_Icon_Key")|プロテクト。 包含クラスまたは型、あるいは包含クラスまたは型から派生したクラスまたは型からアクセスできます。|
|![シグナル プライベート シンボル](../ide/media/vxsignal-icon-lock.gif "vxSignal_Icon_Lock")|プライベート。 包含クラスまたは型でのみアクセスできます。|
|![シグナル シール シンボル](../ide/media/vxsignal-icon-envelope.gif "vxSignal_Icon_Envelope")|シール。|
|![シグナルフレンド&#47;内部シンボル](../ide/media/vxsignal-icon-diamond.gif "vxSignal_Icon_Diamond")|フレンド/内部。 プロジェクトからのみアクセスできます。|
|![シグナル アイコン矢印](../ide/media/vxsignal-icon-arrow.gif "vxSignal_Icon_Arrow")|ショートカット。 オブジェクトへのショートカットです。|

## <a name="see-also"></a>参照
 [コードの構造の表示](../ide/viewing-the-structure-of-code.md)
