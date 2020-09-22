---
title: 言語サービスフィルターの重要なコマンド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 03bb20abf32f7c320ed56f4a649a9f43453e7694
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842028"
---
# <a name="important-commands-for-language-service-filters"></a>言語サービス フィルターの重要なコマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

完全に機能する言語サービスフィルターを作成する場合は、次のコマンドを処理することを検討してください。 コマンド識別子の完全な一覧は、マネージ <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コードの列挙と、アンマネージコードの Stdidcmd ヘッダーファイルで定義されてい [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] ます。 Stdidcmd ファイルは、 *Visual STUDIO SDK のインストールパス*\VisualStudioIntegration\Common\Inc. にあります。  
  
## <a name="commands-to-handle"></a>処理するコマンド  
  
> [!NOTE]
> 次の表の各コマンドに対してフィルター処理を行うことは必須ではありません。  
  
|コマンド|説明|  
|-------------|-----------------|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが右クリックしたときに送信されます。 このコマンドは、ショートカットメニューを提供する時間を示します。 このコマンドを処理しない場合、テキストエディターには、言語固有のコマンドを使用せずに既定のショートカットメニューが表示されます。 このメニューに独自のコマンドを追加するには、コマンドを処理し、自分でショートカットメニューを表示します。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常、ユーザーが CTRL + J キーを押したときに送信されます。 でメソッドを呼び出して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ステートメント入力候補ボックスを表示します。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが文字を入力したときに送信されます。 このコマンドを監視して、トリガー文字がいつ入力されたかを確認し、ステートメント入力候補、メソッドのヒント、およびテキストマーカー (構文の色分け、かっこの一致、エラーマーカーなど) を指定します。 ステートメントの入力候補に対してメソッドを呼び出し、メソッドのヒントに対してメソッドを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> ます。 テキストマーカーをサポートするには、このコマンドを監視して、入力されている文字がマーカーを更新する必要があるかどうかを判断します。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが Enter キーを入力したときに送信されます。 このコマンドを監視して、でメソッドを呼び出して、メソッドのヒントウィンドウを閉じるタイミングを決定し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> ます。 既定では、このコマンドはテキストビューによって処理されます。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが Backspace キーを入力したときに送信されます。 でメソッドを呼び出して、メソッドのヒントウィンドウを閉じるタイミングを監視し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> ます。 既定では、このコマンドはテキストビューによって処理されます。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|メニューまたはショートカットキーから送信されます。 のメソッドを呼び出して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> パラメーター情報を使用して tip ウィンドウを更新します。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが変数に移動したとき、または変数にカーソルを置いて、[**編集**] メニューの**IntelliSense**から**クイックヒント**を選択したときに送信されます。 でメソッドを呼び出して、ヒントの変数の型を返し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。 デバッグがアクティブな場合は、ヒントにも変数の値が表示されます。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常、ユーザーが CTRL + SPACE キーを押したときに送信されます。 このコマンドは、でメソッドを呼び出すように言語サービスに指示し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。|  
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|メニューから送信されます。通常は、[**編集**] メニューの **[詳細設定**] を**選択**するか、選択**項目**をコメント解除します。 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> ユーザーが選択したテキストをコメントアウトすることを示します。 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> ユーザーが選択したテキストのコメントを解除することを示します。 これらのコマンドは、言語サービスによってのみ実装できます。|  
  
## <a name="see-also"></a>参照  
 [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
