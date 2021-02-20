---
title: Windows シンボル情報を参照する | Microsoft Docs
description: Visual Studio プロファイル ツールでシンボル (.pdb) ファイルを使用して、プログラム バイナリの関数名などのシンボル名を解決する方法について学習します。
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- performance tools, symbol servers
- servers, symbol servers
- profiling tools, symbol servers
- symbol servers
ms.assetid: b7c67318-6be2-4b1e-a161-077b1f4a7c30
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c788be648b77a36b8da7027c89a7d9cb047b57d5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907098"
---
# <a name="how-to-reference-windows-symbol-information"></a>方法: Windows シンボル情報を参照する
Visual Studio プロファイリング ツールは、シンボル (.*pdb*) ファイルを使用して、プログラム バイナリの関数名などのシンボル名を解決します。 次の手順を使って、ローカル コンピューター上の Windows のバージョンに適切な .*pdb* ファイルを自動的にダウンロードし、更新することができます。

> [!NOTE]
> この設定は、既存のレポートには影響しません。 シンボル サーバーを指定した後に作成されたレポートだけにシンボル情報が含まれます。

 詳細については、[シンボル (.*pdb*) ファイルとソース ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)の指定に関する記事をご覧ください。

### <a name="to-use-the-microsoft-symbol-server"></a>Microsoft シンボル サーバーを使用するには

1. シンボル ファイルの情報を格納するフォルダーを作成します (例: C:\SymbolCache)。

2. **[ツール]** メニューの **[オプション]** をクリックします。

     **[オプション]** ダイアログ ボックスが表示されます。

3. **[デバッグ]** ツリーを展開し、 **[シンボル]** をクリックします。

4. **[シンボル ファイル (.pdb) の場所]** で、 **[Microsoft シンボル サーバー]** を選択します。

5. **[シンボル サーバーからシンボルをキャッシュするディレクトリ]** ボックスに、次に示すように、手順 1. で作成したフォルダーのパスを入力します。

     **C:\SymbolCache**

     あるいは省略記号ボタン ( **...** ) をクリックして、 **[フォルダの参照]** ダイアログ ボックスでディレクトリを選択することもできます。

## <a name="see-also"></a>関連項目
- [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
- [方法: シンボル情報をシリアル化する](../profiling/how-to-serialize-symbol-information.md)
