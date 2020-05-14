---
title: ソース管理プラグインの実装に関するベスト プラクティス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 68491f22d63ae3ebb664b7c22188a661dccbf39a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740055"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装するためのベスト プラクティス
次の技術的な詳細は、ソース管理プラグインを確実に実装するのに役立[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ちます。

## <a name="memory-management-issues"></a>メモリ管理の問題
 ほとんどの場合、呼び出し元である統合開発環境 (IDE) は、メモリを解放して割り当てます。 ソース管理プラグインは、文字列とその他の項目を呼び出し元が割り当てたバッファーに返します。 例外は、発生する特定の関数の説明に記載されています。

## <a name="arrays-of-file-names"></a>ファイル名の配列
 ファイルの配列が渡されるとき、ファイル名の連続した配列として渡されません。 ファイル名へのポインタの配列として渡されます。 たとえば、 [SccGet](../extensibility/sccget-function.md)では、ファイル名は`lpFileNames`パラメーター`lpFileNames`によって渡されます。 `char **` `lpFileNames`[0] は最初の名前へのポインタであり`lpFileNames`、[1] は 2 番目の名前へのポインタであり、以下に続く。

## <a name="large-model"></a>大型モデル
 16 ビットオペレーティング・システム上であっても、すべてのポインターは 32 ビットです。

## <a name="fully-qualified-paths"></a>完全修飾パス
 ファイル名またはディレクトリを引数として指定する場合、末尾の円記号を使用せずに、完全修飾パスまたは UNC パスを指定する必要があります。 ソース管理プラグインは、基になるソース管理システムの要件である場合、相対パスに変換する必要があります。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>登録された DLL の完全修飾パスを指定します。
 IDE は相対パスから DLL を読み込みなくなりました (たとえば *、.\NewProvider.dll)。* DLL の完全なパスを指定する必要があります (*たとえば、C:\プロバイダー\NewProvider.dll)。* この要件は、権限のないソース管理 DLL または偽装されたソース管理 DLL の読み込みを防止することによって、IDE のセキュリティを強化します。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>ソース管理プラグインをインストールするときに既存の VSSCI プラグインを確認する
 ソース管理プラグインをインストールする予定のユーザーは、既にコンピューターに既存のソース管理プラグインがインストールされている可能性があります。 作成するプラグインのインストール (セットアップ) プログラムは、関連するレジストリ キーの既存の値があるかどうかを判断する必要があります。 これらのキーが既に設定されている場合、インストール プログラムは、プラグインを既定のソース管理プラグインとして登録するかどうかをユーザーに確認し、インストール済みのプラグインを置き換える必要があります。

## <a name="error-result-codes-and-reporting"></a>エラー結果コードとレポート
 ソース`SCC_OK`管理関数の戻りコードは、すべてのファイルに対して操作が成功したことを示します。 操作が失敗した場合は、最後に発生したエラー コードを返す必要があります。

 レポートのルールは、IDE でエラーが発生した場合、IDE がそのエラーを報告する責任を負うということです。 ソース管理システムでエラーが発生した場合、ソース管理プラグインがエラーの報告を行います。 たとえば、**選択されているファイルは**IDE によって報告されませんが、**このファイルは既にチェックアウト**されていますが、プラグインによって報告されます。

## <a name="the-context-structure"></a>コンテキスト構造
 [SccInitialize](../extensibility/sccinitialize-function.md)の呼び出し中に、呼び`ppvContext`出し元は、初期化されていないハンドルであるパラメーターを void に渡します。 ソース管理プラグインは、このパラメーターを無視するか、任意の種類の構造体を割り当てて、渡されたポインターにその構造体へのポインターを配置できます。 IDE はこの構造を理解していませんが、プラグイン内の他のすべての呼び出しにこの構造体へのポインターを渡します。 これにより、プラグインに対して、グローバル変数を使用せずに関数呼び出しを通じて保持されるグローバル状態情報を維持するために使用できる、貴重なコンテキスト キャッシュ情報が提供されます。 プラグインは、 [SccUninitialize](../extensibility/sccuninitialize-function.md)の呼び出しで構造体を解放する役割を担います。

 プラグインが[SccInitialize](../extensibility/sccinitialize-function.md) `lpSccCaps` `SCC_CAP_REENTRANT`でビットを設定する場合 (具体的には、パラメーター)、開いているすべてのプロジェクトを追跡するために複数のコンテキスト構造が使用されます。

## <a name="bitflags-and-other-command-options"></a>ビットフラグおよびその他のコマンドオプション
 [SccGet](../extensibility/sccget-function.md)などの各コマンドでは、コマンドの動作を変更する多くのオプションを指定できます。

 この API では、パラメーターを使用して IDE`fOptions`による特定のオプションの設定がサポートされています。 これらのオプションについては、[特定のコマンドで使用される Bitflags](../extensibility/bitflags-used-by-specific-commands.md)と、そのコマンドが影響を受けるコマンドで説明されています。 一般に、これらはユーザーに対してプロンプトが表示されないオプションです。

 ユーザーが設定できる設定オプションのほとんどは、ソース管理プラグインによって大きく異なるため、この方法では定義されていません。したがって、推奨されるメカニズムは **[詳細設定]** ボタンです。 たとえば、[**取得**] ダイアログ ボックスには、IDE に認識できる情報だけが表示されますが、プラグインにこのコマンドのオプションがある場合は **[詳細設定**] ボタンも表示されます。 ユーザーが **[詳細設定**] ボタンをクリックすると、IDE[は SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)を呼び出して、ソース管理プラグインを有効にして、ビットフラグや日付/時刻などの情報をユーザーに求めます。 プラグインは、コマンド中に戻される構造体の中でこの情報を`SccGet`返します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインを作成する](../extensibility/internals/creating-a-source-control-plug-in.md)
