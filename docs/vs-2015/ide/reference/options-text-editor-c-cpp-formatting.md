---
title: '[オプション]、[テキスト エディター]、[C/C++]、[書式設定] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.C%2fC%2b%2b.Formatting.General
dev_langs:
- C++
helpviewer_keywords:
- Text Editor Options dialog box, formatting
ms.assetid: cb6f1cbb-5305-48da-a8e8-33fd70775d46
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5ad06dfb32c301985eb4976f6c89c7be1e0e68da
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662341"
---
# <a name="options-text-editor-cc-formatting"></a>[オプション]、[テキスト エディター]、[C/C++]、[書式設定]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このページでは、C または C++ でプログラムを記述する際のコード エディターの既定の動作を変更できます。

 このページを表示するには、左ペインの **[オプション]** ダイアログ ボックスで、 **[テキスト エディター]** フォルダー、 **[C/C++]** を順に展開して、 **[書式設定]** をクリックします。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="cc-options"></a>[C/C++ オプション]
 **自動クイックヒントツールヒントを有効にする**クイックヒント IntelliSense 機能を有効または無効にします。

## <a name="inactive-code"></a>[アクティブでないコード]
 **アクティブでないコードブロックの表示**@No__t_1 宣言によって非アクティブになっているコードは、識別しやすいように異なる方法で色分けされています。

 **アクティブでないコードの不透明度を無効にする**非アクティブコードは、透明度ではなく色を使用して識別できます。

 **非アクティブコードの不透明度 (%)** アクティブでないコードブロックの不透明度はカスタマイズできます。

## <a name="indentation"></a>[インデント幅]
 **かっこをインデント**するコードブロックの開始後に enter キーを押すと (関数や `for` ループなど)、中かっこをどのように揃えるかを構成できます。 中かっこは、コード ブロックの最初の文字位置に合わせて、またはインデント位置に合わせて配置されます。

 **タブの自動インデント**TAB キーを押すと、現在のコード行で何が起こるかを構成できます。 行がインデントされるか、またはタブが挿入されます。

## <a name="miscellaneous"></a>その他
 [**タスク一覧] ウィンドウのコメントを列挙する**エディターでは、コメント内の事前設定された単語を含むオープンソースファイルをスキャンできます。 見つかったキーワードのエントリが **[タスク一覧]** ウィンドウに作成されます。

 **一致するトークンの強調表示**カーソルが中かっこの横にある場合、エディターは対応する中かっこを強調表示して、含まれているコードをより簡単に確認できるようにします。

## <a name="outlining"></a>アウトライン
 **ファイルを開くときにアウトラインモードに入る**ファイルをテキストエディターに取り込むと、アウトライン機能を有効にすることができます。 詳細については、「[アウトライン](../../ide/outlining.md)」を参照してください。 このチェック ボックスをオンにすると、ファイルを開いたときにアウトライン表示機能が有効になります。

 **#Pragma 領域ブロックの自動アウトライン**このオプションを選択すると、[プラグマディレクティブ](https://msdn.microsoft.com/library/9867b438-ac64-4e10-973f-c3955209873f)の自動アウトラインが有効になります。 これにより、アウトライン モードでプラグマ領域ブロックの展開と折りたたみを行うことができます。

 **ステートメントブロックの自動的なアウトライン**このオプションを選択すると、次のステートメント構造で自動アウトラインが有効になります。

- [if-else](https://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2)

- [switch ステートメント (C++)](https://msdn.microsoft.com/library/6c3f3ed3-5593-463c-8f4b-b33742b455c6)

- [while ステートメント (C++)](https://msdn.microsoft.com/library/358dbe76-5e5e-4af5-b575-c2293c636899)

## <a name="see-also"></a>関連項目
 [[全般] ([オプション] ダイアログボックス](../../ide/reference/general-environment-options-dialog-box.md)- [IntelliSense を使用](../../ide/using-intellisense.md))
