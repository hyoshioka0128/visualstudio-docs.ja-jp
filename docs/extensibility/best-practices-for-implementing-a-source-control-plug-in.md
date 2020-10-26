---
title: ソース管理プラグインの実装に関するベストプラクティス
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 399afaff75b2456e668aaa9862fb7aa5439cc39f
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90038453"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装するためのベストプラクティス
次の技術的な詳細は、でソース管理プラグインを確実に実装するのに役立ち [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

## <a name="memory-management-issues"></a>メモリ管理の問題
 ほとんどの場合、呼び出し元である統合開発環境 (IDE) は、メモリを解放して割り当てます。 ソース管理プラグインは、呼び出し元が割り当てたバッファー内の文字列とその他の項目を返します。 例外については、発生した特定の関数の説明に記載されています。

## <a name="arrays-of-file-names"></a>ファイル名の配列
 ファイルの配列が渡されると、ファイル名の連続する配列として渡されません。 ファイル名へのポインターの配列として渡されます。 たとえば、 [Sccget](../extensibility/sccget-function.md)では、パラメーターによってファイル名が渡され `lpFileNames` ます。ここで、 `lpFileNames` は実際にへのポインターです `char **` 。 `lpFileNames`[0] は、最初の名前へのポインターです `lpFileNames` 。 [1] は2番目の名前へのポインターです。

## <a name="large-model"></a>大規模なモデル
 すべてのポインターは、16ビットオペレーティングシステムであっても、32ビットです。

## <a name="fully-qualified-paths"></a>完全修飾パス
 ファイル名またはディレクトリを引数として指定する場合は、末尾に円記号を付けずに、完全修飾パスまたは UNC パスを指定する必要があります。 基になるソース管理システムの要件である場合は、ソース管理プラグインを相対パスに変換する必要があります。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>登録された DLL の完全修飾パスを指定します
 IDE では、相対パス ( *.\NewProvider.dll*など) から dll が読み込まれなくなりました。 DLL の完全パスを指定する必要があります (たとえば、 *C:\Providers\NewProvider.dll*)。 この要件により、未承認または偽装されたソース管理 Dll の読み込みを防ぐことができ、IDE のセキュリティが強化されます。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>ソース管理プラグインをインストールするときに既存の VSSCI プラグインがあるかどうかを確認する
 ソース管理プラグインをインストールする予定のユーザーには、既存のソース管理プラグインが既にコンピューターにインストールされている場合があります。 作成するプラグインのインストール (セットアップ) プログラムでは、関連するレジストリキーに既存の値があるかどうかを判断する必要があります。 これらのキーが既に設定されている場合、インストールプログラムは、プラグインを既定のソース管理プラグインとして登録するかどうかをユーザーに確認し、既にインストールされているプラグインを置き換える必要があります。

## <a name="error-result-codes-and-reporting"></a>エラー結果コードとレポート
 `SCC_OK`ソース管理関数のリターンコードは、すべてのファイルに対して操作が成功したことを示します。 操作が失敗した場合、最後に検出されたエラーコードが返されます。

 レポートのルールは、ide でエラーが発生した場合に、IDE がそれを報告する役割を果たしていることを示します。 ソース管理システムでエラーが発生した場合は、ソース管理プラグインによってレポートが作成されます。 たとえば、 **現在選択** されているファイルが IDE によって報告されないのに対し、 **このファイルは既にチェックアウト** されているため、プラグインによって報告されます。

## <a name="the-context-structure"></a>コンテキスト構造
 [Sccinitialize](../extensibility/sccinitialize-function.md)の呼び出し中に、呼び出し元は、 `ppvContext` void への初期化されていないハンドルであるパラメーターを渡します。 ソース管理プラグインは、このパラメーターを無視することも、任意の種類の構造体を割り当て、その構造体へのポインターを渡されたポインターに格納することもできます。 IDE はこの構造を理解していませんが、この構造体へのポインターをプラグイン内の他のすべての呼び出しに渡します。 これにより、グローバル変数を使用せずに関数呼び出し間で保持されるグローバル状態情報を維持するために使用できる、有益なコンテキストキャッシュ情報がプラグインに提供されます。 プラグインは、 [Sccuninitialize](../extensibility/sccuninitialize-function.md)解除の呼び出しで構造体を解放する役割を担います。

 プラグインが `SCC_CAP_REENTRANT` [Sccinitialize](../extensibility/sccinitialize-function.md) のビットを設定している場合 (具体的には `lpSccCaps` パラメーター)、開いているすべてのプロジェクトを追跡するために複数のコンテキスト構造が使用されます。

## <a name="bitflags-and-other-command-options"></a>Bitflags とその他のコマンドオプション
 [Sccget](../extensibility/sccget-function.md)などの各コマンドに対して、IDE はコマンドの動作を変更する多くのオプションを指定できます。

 API は、パラメーターを使用した IDE による特定のオプションの設定をサポートしてい `fOptions` ます。 これらのオプションについ [ては、特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md) と、それによって影響を受けるコマンドを組み合わせて説明します。 一般に、これらのオプションはユーザーにプロンプトを表示しません。

 ユーザーが構成できるほとんどの設定オプションは、ソース管理プラグインによって大きく異なるため、この方法で定義されていません。このため、推奨されるメカニズムは **[詳細設定** ] ボタンです。 たとえば、[ **取得** ] ダイアログボックスでは、IDE には認識している情報のみが表示されますが、プラグインにこのコマンドのオプションがある場合は **[詳細設定** ] ボタンも表示されます。 ユーザーが **[詳細設定** ] ボタンをクリックすると、IDE は [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) を呼び出して、ソース管理プラグインによって、ビットフラグや日付/時刻などの情報の入力をユーザーに求めることができるようにします。 このプラグインは、コマンドの実行中に返される構造体にこの情報を返し `SccGet` ます。

## <a name="see-also"></a>参照
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインを作成する](../extensibility/internals/creating-a-source-control-plug-in.md)
