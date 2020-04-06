---
title: '方法 : カスタム デバッグ エンジンをデバッグする |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c79790bfc9c9cd3767a453258b8c2d340f64d029
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738576"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>方法: カスタム デバッグ エンジンをデバッグする
プロジェクトの種類は、メソッドからデバッグ エンジン (DE) を起動します<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A>。 つまり、DE はプロジェクトの種類を制御するインスタンスの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]制御の下で起動されます。 ただし、そのインスタンスは[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]DE をデバッグできません。 次に示す手順を使用すると、カスタム DE をデバッグできます。

> [!NOTE]
> : "カスタム デバッグ エンジンのデバッグ" の手順では、デが起動するまで待ってからアタッチする必要があります。 DE の開始時に表示される DE の先頭近くにメッセージ ボックスを配置した場合は、そのポイントにアタッチし、メッセージ ボックスをクリアして続行できます。 そうすれば、すべての DE イベントをキャッチできます。

> [!WARNING]
> 次の手順を実行する前に、リモート デバッグをインストールしておく必要があります。 詳細については[、「リモート デバッグ](../../debugger/remote-debugging.md)」を参照してください。

## <a name="debug-a-custom-debug-engine"></a>カスタム デバッグ エンジンをデバッグする

1. *msvsmon.exe*を起動し、リモート デバッグ モニターを起動します。

2. *msvsmon.exe*の [**ツール**] メニューの **[オプション]** をクリックして、[**オプション]** ダイアログ ボックスを開きます。

3. [認証なし] オプションを選択し **、[OK]** をクリックします。

4. のインスタンスを起動[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]し、カスタム DE プロジェクトを開きます。

5. DE を起動する[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]カスタム プロジェクトを 2 つ目のインスタンスで起動し、開きます (開発用に、これは通常、VSIP のインストール時にセットアップされる実験用レジストリ ハイブにあります)。

6. のこの 2[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]番目のインスタンスでは、カスタム プロジェクトからソース ファイルを読み込み、デバッグするプログラムを起動します。 DE が読み込まれるまでしばらく待つか、ブレークポイントがヒットするまで待ちます。

7. (DE プロジェクトを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用して) の最初のインスタンスで、[**デバッグ**] メニューから [**プロセスにアタッチ]** を選択します。

8. [**プロセスにアタッチ]** ダイアログ ボックスで、[**トランスポート**を**リモート (認証なしでネイティブのみ)]** に変更します。

9. **修飾子**をマシンの名前に変更します (注: エントリの履歴があるので、この名前を 1 回だけ入力する必要があります)。

10. [**使用可能なプロセス]** リストで、実行中の DE のインスタンスを選択し、[**アタッチ**] ボタンをクリックします。

11. シンボルが DE に読み込まれた後、DE コードにブレークポイントを配置します。

12. デバッグプロセスを停止してから再開するたびに、手順 6 ~ 10 を繰り返します。

## <a name="debug-a-custom-project-type"></a>カスタム プロジェクトの種類をデバッグする

1. 通常[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のレジストリ ハイブで起動し、プロジェクトの種類のプロジェクトを読み込みます (これは、プロジェクトの種類のインスタンス化ではなく、プロジェクトの種類のソースです)。

2. プロジェクトのプロパティを開き、[**デバッグ**] ページに移動します。 **コマンド**に IDE へのパスを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]入力します (既定では、[*ドライブ]* \プログラム ファイル\マイクロソフト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]8\Common7\IDE\devenv.exe)。

3. [**コマンド引数]** に`/rootsuffix exp`、実験用レジストリ ハイブ (VSIP のインストール時に作成) を入力します。

4. [ **OK** ] をクリックして変更内容を確定します。

5. **F5**キーを押してプロジェクトの種類を開始します。 これにより、 の 2[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]番目のインスタンスが起動します。

6. この時点で、プロジェクトの種類のソース コードにブレークポイントを配置できます。

7. の 2 番目[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のインスタンスで、プロジェクトの種類のインスタンスを読み込むか、新しく作成します。 読み込みまたは作成中に、ブレークポイントがヒットする可能性があります。

8. プロジェクトの種類をデバッグします。

9. DE を起動するプロセスをデバッグする場合は、起動後に、デにアタッチする「カスタム デバッグ エンジンのデバッグ」手順の手順を実行できます。 これにより、プロジェクトの種類のソース[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]用、インスタンス化されたプロジェクトの種類用の 1 つ、および DE にアタッチされた 3 つ目の 3 つの実行インスタンスが提供されます。

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
