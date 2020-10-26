---
title: '[その他] ([オプション] ダイアログボックス-[テキストエディター]-[XML])Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: fd3fff31-cddc-422d-a2f0-a5a1ef492afd
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d30564c11951d6ffec420c6a2ea95c41695de3dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656235"
---
# <a name="miscellaneous-xml-text-editor-options-dialog-box"></a>[その他] ([オプション] ダイアログ ボックス - [テキスト エディター] - [XML])
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このダイアログ ボックスでは、XML エディターのオートコンプリートとスキーマの設定を変更することができます。 **[ツール]** メニューから **[オプション]** ダイアログ ボックスにアクセスできます。

> [!NOTE]
> これらの設定は、[**テキストエディター** ] フォルダー、[ **XML** ] フォルダー、および [**オプション**] ダイアログボックスの [**その他**] オプションを選択すると使用できます。

## <a name="auto-insert"></a>自動挿入
 **終了タグ** オートコンプリートの設定がオンになっている場合、タグがまだ閉じられていない場合は、右山かっこ (>) を入力して開始タグを閉じると、終了タグが自動的に追加されます。 これは既定の動作です。

 空の要素の完了は、オートコンプリート設定に依存するわけではありません。 バックスラッシュ (/) を入力することで、いつでも空の要素をオートコンプリートできます。

 **属性の引用符** XML 属性を作成すると、エディターによって文字が挿入され、 `=" "` 二重引用符内にカレット (^) が配置されます。

 既定で選択されています。

 **名前空間の宣言** 必要に応じて、エディターによって名前空間の宣言が自動的に挿入されます。

 既定で選択されています。

 **その他のマークアップ (コメント、CDATA)** コメント、CDATA、DOCTYPE、処理命令、およびその他のマークアップがオート完了します。

 既定で選択されています。

## <a name="network"></a>ネットワーク
 **Dtd とスキーマを自動的にダウンロード** するスキーマとドキュメント型定義 (Dtd) は、HTTP ロケーションから自動的にダウンロードされます。 この機能は、プロキシ サーバーの自動検出を有効にした System.Net を使用します。

 既定で選択されています。

## <a name="outlining"></a>アウトライン
 **ファイルを開くときにアウトラインモードに入る** ファイルを開いたときにアウトライン機能をオンにします。

 既定で選択されています。

## <a name="caching"></a>キャッシュ
 **スキーマ** スキーマキャッシュの場所を指定します。 参照ボタン ([.**..**]) をクリックすると、現在のスキーマキャッシュの場所で [ **ディレクトリの参照** ] ダイアログボックスが開きます。 別のディレクトリを選択するか、ダイアログでフォルダーを選択して右クリックし、[ **開く** ] を選択してディレクトリ内の内容を確認することができます。

## <a name="see-also"></a>参照
 [Xml ドキュメントのプロパティ、[プロパティ] ウィンドウの](../xml-tools/xml-document-properties-properties-window.md) [Xml エディターのコンポーネント](../xml-tools/xml-editor-components.md)
