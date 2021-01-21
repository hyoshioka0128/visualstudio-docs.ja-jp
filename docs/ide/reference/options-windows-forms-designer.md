---
title: '[オプション]、[Windows フォームデザイナー]、全般'
description: '[全般] ページを使用して、Visual Studio の Windows フォーム デザイナーのグリッドとその他の機能に対するユーザー設定を設定する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 08/09/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.WindowsFormsDesigner.General
helpviewer_keywords:
- Windows Forms Designer options
- Options dialog box, Windows Forms Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: d7172ca12344ab046c9bf65e7df280a9fa6dd0aa
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040083"
---
# <a name="options-dialog-box-windows-forms-designer"></a>[オプション] ダイアログ ボックス:Windows フォーム デザイナー

Windows フォーム デザイナーのオプション ページでは、Visual Studio の Windows フォーム デザイナーのグリッドとその他の機能に対するユーザー設定を設定できます。 **[ツール]** メニューから **[オプション]** ダイアログ ボックスを開きます。

## <a name="code-generation-settings"></a>コード生成の設定

**最適化されたコード生成**\
最適化されたコード生成を有効にします。 一部のコントロールは、このモードと互換性がない場合があります。 この変更を有効にするには、Visual Studio を閉じてからもう一度開く必要があります。

## <a name="high-dpi-support"></a>高 DPI サポート

**DPI スケーリングに関する通知**\
Visual Studio を 100% のスケーリングで再起動できるメッセージを、Windows フォーム デザイナーに表示します。 詳しくは、「[Visual Studioで DPI の認識を無効にする](/dotnet/framework/winforms/disable-dpi-awareness-visual-studio)」をご覧ください。

## <a name="layout-settings"></a>レイアウト設定

**既定のグリッド セル サイズ**\
デザイナーの水平グリッド線と垂直グリッド線の間隔をピクセル単位で設定します。 既定のサイズは 8 と 8 です。 最大サイズは 200 と 200 です。

**レイアウト モード**\
レイアウトに使用する配置システムを指定します。 SnapToGrid またはスナップ線のいずれかを選択できます。

**グリッドの表示**\
デザイナーでサイズ設定グリッドを表示するかどうかを指定します。 既定では、グリッドは有効になっています。

**グリッドに合わせる**\
デザイナーでオブジェクトとコントロールをグリッドにスナップするかどうかを決定します。 つまり、この機能が有効になっている場合、デザイナーでの要素のサイズ変更と移動は、GridSize のインクリメントに制限されます。 SnapToGrid を有効にすると、ユーザー インターフェイスのさまざまな部分を正確に整列しやすくなりますが、コントロールを配置するユーザーの自由度は制限されます。 既定では、SnapToGrid は有効になっています。

## <a name="object-bound-smart-tag-settings"></a>オブジェクト バインド スマート タグ設定

**自動的にスマート タグを開く**\
コントロールとコンポーネントでスマート タグを表示するかどうかを決定します。 スマート タグがサポートされていないコントロールやコンポーネントもあります。

## <a name="refactoring"></a>リファクタリング

**名前変更時のリファクタリングの有効化**\
`true` に設定すると、[プロパティ] ウィンドウまたは [ドキュメント アウトライン] ウィンドウでコンポーネントの名前を変更すると、名前の変更リファクタリング操作が実行されます。

## <a name="toolbox"></a>ツールボックス

**ツールボックスを自動取得する**\
プロジェクトによってビルドされたコンポーネントとコントロールを [ツールボックス] ウィンドウに自動的に設定するかどうかを決定します。
