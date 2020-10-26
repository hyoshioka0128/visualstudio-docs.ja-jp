---
title: '方法: カスタムデバッグエンジンをデバッグする |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a65e69655c4e8699bd267f1835ec0c49603014d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903307"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>方法: カスタムデバッグエンジンをデバッグする
プロジェクトの種類は、メソッドからデバッグエンジン (DE) を起動し <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> ます。 これは、プロジェクトの種類を制御するインスタンスの制御下で DE が起動されることを意味 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 ただし、のインスタンスでは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、DE をデバッグできません。 カスタム DE をデバッグするための手順を次に示します。

> [!NOTE]
> : "カスタムデバッグエンジンのデバッグ" 手順では、このプロシージャにアタッチする前に、DE が開始されるまで待機する必要があります。 De の開始時に表示される DE の先頭付近にメッセージボックスを配置すると、その時点でアタッチして、メッセージボックスをクリアして続行することができます。 これにより、すべての DE イベントをキャッチできます。

> [!WARNING]
> 次の手順を実行する前に、リモートデバッグがインストールされている必要があります。 詳細については、「 [リモートデバッグ](../../debugger/remote-debugging.md) 」を参照してください。

## <a name="debug-a-custom-debug-engine"></a>カスタムデバッグエンジンのデバッグ

1. リモートデバッグモニターの *msvsmon.exe*を開始します。

2. *msvsmon.exe*の [**ツール**] メニューの [**オプション**] をクリックして、[**オプション**] ダイアログボックスを開きます。

3. [認証なし] オプションを選択し、[ **OK]** をクリックします。

4. のインスタンスを起動 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] し、カスタムの DE プロジェクトを開きます。

5. の2番目のインスタンスを起動 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] し、DE を起動するカスタムプロジェクトを開きます (開発の場合、これは通常、VSIP をインストールするときに設定される実験用のレジストリハイブにあります)。

6. の2番目のインスタンスで [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、カスタムプロジェクトからソースファイルを読み込み、デバッグするプログラムを開始します。 しばらく待ってから、DE の読み込みを許可するか、ブレークポイントにヒットするまで待機します。

7. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)](DE プロジェクトを含む) の最初のインスタンスで、[**デバッグ**] メニューの [**プロセスにアタッチ**] を選択します。

8. [ **プロセスにアタッチ** ] ダイアログボックスで、[ **トランスポート** ] を [ **リモート (認証なしのネイティブのみ)**] に変更します。

9. **修飾子**をコンピューターの名前に変更します (メモ: エントリの履歴があるため、この名前は1回だけ入力する必要があります)。

10. [選択 **可能なプロセス** ] ボックスの一覧で、実行している DE のインスタンスを選択し、[ **アタッチ** ] ボタンをクリックします。

11. シンボルを DE に読み込んだら、DE コードにブレークポイントを配置します。

12. デバッグプロセスを停止してから再起動するたびに、手順 6. ~ 10. を繰り返します。

## <a name="debug-a-custom-project-type"></a>カスタムプロジェクトの種類をデバッグする

1. 通常のレジストリハイブから開始し、プロジェクトの種類のプロジェクト (プロジェクトの種類のインスタンス化ではなく、プロジェクトの種類 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のソース) を読み込みます。

2. プロジェクトのプロパティを開き、[ **デバッグ** ] ページにアクセスします。 **コマンド**の場合は、IDE へのパスを入力し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます (既定では、 *[ドライブ 8\Common7\IDE\devenv.exe] は [ドライブ]* になり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます)。

3. コマンドの **引数**には、 `/rootsuffix exp` 実験的なレジストリハイブ (VSIP のインストール時に作成されたもの) を入力します。

4. [ **OK** ] をクリックして変更内容を確定します。

5. **F5**キーを押して、プロジェクトの種類を開始します。 これにより、の2番目のインスタンスが起動 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

6. この時点で、プロジェクトの種類のソースコードにブレークポイントを配置できます。

7. の2番目のインスタンスで [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、プロジェクトの種類の新しいインスタンスを読み込むか作成します。 読み込み中または作成中に、ブレークポイントにヒットすることがあります。

8. プロジェクトの種類をデバッグします。

9. DE を起動するプロセスをデバッグする場合は、「カスタムデバッグエンジンのデバッグ」の手順を実行して、起動後に DE にアタッチすることができます。 これにより、2つのインスタンスが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 実行されます。1つはプロジェクトの種類のソース、もう1つはインスタンス化されたプロジェクトの種類、もう1つは DE にアタッチされます。

## <a name="see-also"></a>関連項目
- [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
