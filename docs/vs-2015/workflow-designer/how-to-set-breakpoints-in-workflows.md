---
title: '方法: ワークフローにブレークポイントを設定するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: e41b21c9-c061-4358-8e2f-eb5e412864a8
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2d1bbb18a9015b52b3d65cb8f8fd02674693abc0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659135"
---
# <a name="how-to-set-breakpoints-in-workflows"></a>方法 : ワークフロー内のブレークポイントを設定する
[!INCLUDE[wfd1](../includes/wfd1-md.md)]を使用すると、Visual Basic コードまたは C# コードを使用する場合と同じように、グラフィカル ワークフローにブレークポイントを設定できます。 設定したそれぞれのブレークポイントで、ワークフローの実行が停止します。

 ブレークポイントには、 *保留中*、 *バインド*済み、 *エラー*という3つの状態があります。 ブレークポイントは、設定時には "保留" になり、穴のない赤いアイコンで表示されます。 特定の種類のワークフローがランタイムによって読み込まれると、ブレークポイントの状態は "バインド" になります。 不適切な形式のブレークポイントを指定した場合 (アクティビティ名が無効など) は、エラー ウィンドウが表示されます。 ブレークポイントはブレークポイント ウィンドウに追加されますが、小さな x 印が付きます。

> [!NOTE]
> 呼び出されるワークフローに対してブレークポイントを設定することはできません。
>
> [!WARNING]
> デバッグする前に、[**ツール**]、[**オプション**]、[**デバッグ**] メニューの [**マイコードのみを有効にする (マネージのみ)** ] オプションが選択されていることを確認します。 2つのシーケンスが別のシーケンス内に入れ子になっていて、最初の内部シーケンスにブレークポイントを設定した場合、[<strong>マイコードのみを有効にする (マネージのみ)</strong>] オプションが選択されていない場合、 **F11**キーを押しても2番目の内部シーケンスにはデバッグされません。
>
> [!WARNING]
> XAML ファイルのプロパティへの完全パスが正確でない場合、ワークフロー内のブレークポイントにヒットしません。XAML ファイルへの完全パスは、プロジェクトやソリューションを別のフォルダーや別のコンピューターへ移動すると正確ではなくなります。Ctrl キーを押しながら S キーを押すと、完全パスのプロパティが保存および更新されます。

### <a name="to-set-a-breakpoint-on-an-activity-in-the-design-view"></a>デザイン ビューでアクティビティにブレークポイントを設定するには

1. デバッガーを中断する位置にあるアクティビティを選択します。

2. [ **デバッグ** ] メニューの [ **ブレークポイント**の設定/解除] をクリックします。 アクティビティの左上端に赤色のアイコンが表示されます。

     または、アクティビティを選択した後にショートカット **F9** キーを押すか、アクティビティを右クリックして、コンテキストメニューから [ **ブレークポイント** ]、[ブレークポイントの **挿入** ] の順に選択することもできます。

## <a name="see-also"></a>参照
 [方法:](../workflow-designer/how-to-invoke-the-workflow-debugger.md) [ワークフローデザイナーを使用してワークフローデバッガーデバッグワークフロー](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)を呼び出す方法 [: ワークフローデザイナーを使用して XAML をデバッグする](../workflow-designer/how-to-debug-xaml-with-the-workflow-designer.md)