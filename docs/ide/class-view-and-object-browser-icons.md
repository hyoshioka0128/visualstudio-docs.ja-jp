---
title: '[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン'
description: 名前空間、クラス、関数、変数などのコード エンティティを表す [クラス ビュー] およびオブジェクト ブラウザーのアイコン表示について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 9e0348c1f6c51f0a82328814be671d8f44e3d4a7
ms.sourcegitcommit: 3922edfe67063e1ede418cdbf6aa6293117c4855
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773353"
---
# <a name="class-view-and-object-browser-icons"></a>[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン

**[クラス ビュー]** および **オブジェクト ブラウザー** には、名前空間、クラス、関数、変数などのコード エンティティを表すアイコンが表示されます。 各アイコンおよびその説明を次の表に示します。

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

> [!TIP]
> このページのアイコンを最適に表示するには、Microsoft Docs テーマが **[ライト]** に設定されていることを確認してください。 この配色テーマは、次のスクリーンショットに示すように、ページの左下にあるコントロールから切り替えることができます。
>
> ![Docs のテーマ](../ide/media/toggle-docs-color-theme.png "Microsoft Docs ページの配色テーマを切り替える")

## <a name="signal-icons"></a>シグナル アイコン

次のシグナル アイコンは、上記のアイコンすべてに適用され、そのアクセシビリティを示します。

|アイコン|説明|
|----------|-----------------|
|\<No Signal Icon>|パブリック。 このコンポーネント内のどこからでも、また、それを参照するどのコンポーネントからでもアクセスできます。|
|![シグナル プロテクト シンボル](../ide/media/vxsignal_icon_key.gif)|プロテクト。 包含クラスまたは型、あるいは包含クラスまたは型から派生したクラスまたは型からアクセスできます。|
|![シグナル プライベート シンボル](../ide/media/vxsignal_icon_lock.gif)|プライベート。 包含クラスまたは型でのみアクセスできます。|
|![シグナル シール シンボル](../ide/media/vxsignal_icon_envelope.gif)|シール。|
|![シグナル フレンド&#47;内部シンボル](../ide/media/vxsignal_icon_diamond.gif)|フレンド/内部。 プロジェクトからのみアクセスできます。|
|![シグナル アイコン矢印](../ide/media/vxsignal_icon_arrow.gif)|ショートカット。 オブジェクトへのショートカットです。|

> [!NOTE]
> プロジェクトがソース管理データベースに含まれている場合は、ソース管理のステータス (チェックインまたはチェックアウトなど) を示すシグナル アイコンが追加で表示されることがあります。

> [!TIP]
> Visual Studio に表示されるアプリケーションのイメージおよびアイコンをさらに参照するには、[**Visual Studio Image Library**](https://www.microsoft.com/download/details.aspx?id=35825) を参照してください。

## <a name="see-also"></a>関連項目

- [コードの構造の表示](../ide/viewing-the-structure-of-code.md)
