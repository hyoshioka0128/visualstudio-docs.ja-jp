---
title: '[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- icons, in Object Browser
- signal icons
- Class View tool, symbols
- graphic symbols
- IntelliSense, icons
- icons, IntelliSense
- symbols, Object Browser icons
- Object Browser, icons in Class View
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6589d40d8f897eb8df7f108f53973af268d1edc9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588396"
---
# <a name="class-view-and-object-browser-icons"></a>[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン

**[クラス ビュー]** および**オブジェクト ブラウザー**には、名前空間、クラス、関数、変数などのコード エンティティを表すアイコンが表示されます。 各アイコンおよびその説明を次の表に示します。

|アイコン|説明|アイコン|説明|
|----------|-----------------|----------|-----------------|
|![名前空間シンボル](../ide/media/vxnamespace_icon.gif)|名前空間|![宣言シンボル](../ide/media/vxmethod_icon.gif)|メソッドまたは関数|
|![クラス アイコン](../ide/media/vxclass_icon.gif)|クラス|![演算子シンボル](../ide/media/vxoperator_icon.gif)|演算子|
|![ロリポップ インターフェイス シンボル](../ide/media/vxinterface_icon.gif)|Interface|![プロパティ シンボル](../ide/media/vxproperty_icon.gif)|プロパティ|
|![構造体シンボル](../ide/media/vxstruct_icon.gif)|構造体|![フィールド アイコン](../ide/media/vxfield_icon.gif)|フィールドまたは変数|
|![共用体シンボル](../ide/media/vxunion_icon.gif)|和集合|![イベント シンボル](../ide/media/vxevent_icon.gif)|event|
|![一覧表示シンボル](../ide/media/vxenum_icon.gif)|Enum|![定数アイコン](../ide/media/vxconstant_icon.gif)|定数|
|![型定義シンボル](../ide/media/vxtypedef_icon.gif)|TypeDef|![項目の一覧表示シンボル](../ide/media/vxenumitem_icon.gif)|列挙型項目|
|![Visual Studio モジュール シンボル](../ide/media/vxmodule_icon.gif)|Module|![マップ項目シンボル](../ide/media/vxmapitem_icon.gif)|マップ項目|
|![拡張メソッド シンボル](../ide/media/extensionmethod.gif)|拡張メソッド|![宣言シンボル](../ide/media/vxmethod_icon.gif)|外部宣言|
|![デリゲート シンボル](../ide/media/vxdelegate_icon.gif)|Delegate|![クラス ビューおよびオブジェクト ブラウザーのエラー アイコン](../ide/media/erroricon.gif)|Error|
|![例外シンボル](../ide/media/vxexception_icon.gif)|例外|![テンプレート シンボル](../ide/media/vxtemplate_icon.gif)|テンプレート|
|![マップ シンボル](../ide/media/vxmap_icon.gif)|マップ|![エラー感嘆符シンボル](../ide/media/vxerror_icon.gif)|不明|
|![型転送シンボル](../ide/media/ob_type_forward.gif)|型の転送|||

## <a name="signal-icons"></a>シグナル アイコン

次のシグナル アイコンは、上記のアイコンすべてに適用され、そのアクセシビリティを示します。

|アイコン|説明|
|----------|-----------------|
|\<シグナル アイコンなし>|パブリック。 このコンポーネント内のどこからでも、また、それを参照するどのコンポーネントからでもアクセスできます。|
|![シグナル プロテクト シンボル](../ide/media/vxsignal_icon_key.gif)|プロテクト。 包含クラスまたは型、あるいは包含クラスまたは型から派生したクラスまたは型からアクセスできます。|
|![シグナル プライベート シンボル](../ide/media/vxsignal_icon_lock.gif)|プライベート。 包含クラスまたは型でのみアクセスできます。|
|![シグナル シール シンボル](../ide/media/vxsignal_icon_envelope.gif)|シール。|
|![シグナル フレンド&#47;内部シンボル](../ide/media/vxsignal_icon_diamond.gif)|フレンド/内部。 プロジェクトからのみアクセスできます。|
|![シグナル アイコン矢印](../ide/media/vxsignal_icon_arrow.gif)|ショートカット。 オブジェクトへのショートカットです。|

> [!NOTE]
> プロジェクトがソース管理データベースに含まれている場合は、ソース管理のステータス (チェックインまたはチェックアウトなど) を示すシグナル アイコンが追加で表示されることがあります。

## <a name="see-also"></a>関連項目

- [コードの構造の表示](../ide/viewing-the-structure-of-code.md)
