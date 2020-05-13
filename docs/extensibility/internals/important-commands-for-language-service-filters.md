---
title: 言語サービス フィルタの重要なコマンド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb29ee5b5a5359d6cfe34911656dfe9be015262e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707612"
---
# <a name="important-commands-for-language-service-filters"></a>言語サービス フィルターの重要なコマンド
完全な機能を備えた言語サービス フィルタを作成する場合は、次のコマンドの処理を検討してください。 コマンド識別子の完全な一覧は、マネージ<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>コードの列挙体とアンマネージ[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]コードの Stdidcmd.h ヘッダー ファイルで定義されます。 ファイルは *、Visual Studio SDK*のインストール パス \VisualStudioIntegration\Common\Inc. で見つけることができます。

## <a name="commands-to-handle"></a>処理するコマンド

> [!NOTE]
> 次の表のすべてのコマンドをフィルター処理する必要はありません。

|command|説明|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが右クリックすると送信されます。 このコマンドは、ショートカット メニューを提供する時間であることを示します。 このコマンドを処理しない場合、テキスト エディターには、言語固有のコマンドを使用しない既定のショートカット メニューが表示されます。 このメニューに独自のコマンドを含めるには、コマンドを処理して、ショートカット メニューを表示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常、ユーザーが Ctrl + J キーを押したときに送信されます。 のメソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>を呼び<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>出して、ステートメント入力候補ボックスを表示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが文字を入力したときに送信されます。 このコマンドを監視して、トリガー文字の入力時期を判別し、構文の色付け、ブレースの一致、エラー・マーカーなどのステートメント入力候補、メソッド・ヒント、テキスト・マーカーを提供します。 for<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>ステートメントの完了時にメソッドを呼<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>び出し<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow>、for メソッドヒントのメソッドを呼び出します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> テキスト マーカーをサポートするには、このコマンドを監視して、入力する文字にマーカーの更新が必要かどうかを判断します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが Enter キーを入力したときに送信されます。 このコマンドを監視して、 のメソッドを呼び出してメソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>ヒント<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>ウィンドウを閉じるタイミングを決定します。 既定では、テキスト ビューはこのコマンドを処理します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザが Backspace キーを入力したときに送信されます。 でメソッドを呼び出して、メソッド ヒント ウィンドウ<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>を閉じる<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>タイミングを判断するモニター。 既定では、テキスト ビューはこのコマンドを処理します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|メニューまたはショートカット キーから送信されます。 パラメーター情報<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>を使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>してヒント ウィンドウを更新するメソッドを呼び出します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが変数の上にカーソルを置くか、変数にカーソルを合わせ、[**編集]** メニューの**IntelliSense**から**クイック ヒント**を選択したときに送信されます。 のメソッドを呼び出すことによって、ヒント内の変数<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A>の型を<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>返します。 デバッグがアクティブな場合、ヒントには変数の値も表示されます。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常は、ユーザーが Ctrl + Space キーを押したときに送信されます。 このコマンドは、言語サービスに対して<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>、 の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>メソッドを呼び出すように指示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|メニューから送信される (通常は[**編集**]メニューの **[選択範囲をコメント**]または[**編集]メニューの[詳細設定**から**選択項目をコメント解除**])。 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>選択したテキストをコメント アウトすることを示します。<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>は、選択したテキストのコメントを解除することを示します。 これらのコマンドは、言語サービスによってのみ実装できます。|

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
