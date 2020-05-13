---
title: '[ファイルを開く] コマンドを使用してファイルを表示する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4051793077e613981e1dd5b44f1736878f5853e9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708579"
---
# <a name="display-files-by-using-the-open-with-command"></a>[ファイルから開く] コマンドを使用してファイルを表示する
プロジェクトは IDE に対して[**ファイルを開く**] ダイアログ ボックスを表示するように要求できます。 この要求は、標準エディターの選択を持つファイルを開くユーザーを求めます。 このプロセスは、次の手順で説明します。

1. プロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>を呼び出し`OSE_UseOpenWithDialog`、パラメーター`OSEOpenDocEditor`の値を指定します。

2. ドキュメントのファイル名拡張子に基づいて、指定したドキュメントを開くことができるエディタが IDE によって決定され、[**ファイルを開くアプリケーションの選択**] ダイアログ ボックスに表示されます。

    > [!NOTE]
    > [**ファイルを開く**] ダイアログ ボックスに含める必要がある組み込みエディターを持つプロジェクトは、そのようなエディターごとにエディター ファクトリを登録する必要があります。 組み込みエディターは、メソッドの実装で適用される特定の種類のプロジェクトとのみ機能します<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>。 IDE には、コアテキストエディタとバイナリエディタ用の組み込みエディタファクトリがあります。 IDE は、登録されている各 Windows ファイルの関連付けに代わって、エディター ファクトリのインスタンスも作成します。 このようなファイルの例としては、Word があります。

3. ユーザーが [**ファイルを開くアプリケーションの選択**] ダイアログ ボックスから項目を選択すると、その後<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>、メソッドを呼び出してドキュメントが開きます。 詳細については、「[方法 : 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)
- [[ファイルを開く] コマンドを使用してファイルを表示する](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)
