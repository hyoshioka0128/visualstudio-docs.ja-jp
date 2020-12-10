---
title: '方法: 標準エディターを開く |Microsoft Docs'
description: 標準エディターを使用して OpenItem メソッドを実装する方法について説明します。 IDE では、指定されたファイルの種類の標準エディターが決定されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff03ed508fc11377861556bc27bdc33aaa1ec069
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993771"
---
# <a name="how-to-open-standard-editors"></a>方法: 標準エディターを開く
標準エディターを開くと、ファイルのプロジェクト固有のエディターを指定するのではなく、指定したファイルの種類の標準エディターが IDE によって決定されます。

 メソッドを実装するには、次の手順を実行し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> ます。 これにより、標準エディターでプロジェクトファイルが開きます。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>標準エディターを使用して OpenItem メソッドを実装するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> `RDT_EditLock` ドキュメントデータオブジェクトファイルが既に開いているかどうかを判断するには、() を呼び出します。

2. ファイルが既に開いている場合は、パラメーターに値を指定して、メソッドを呼び出してファイルを resurface し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> `IDO_ActivateIfOpen` `grfIDO` ます。

     ファイルが開いていて、ドキュメントが呼び出し元のプロジェクトとは異なるプロジェクトによって所有されている場合、プロジェクトは、開いているエディターが別のプロジェクトのものであることを示す警告を受け取ります。 次に、ファイルウィンドウが表示されます。

3. ドキュメントが開いていない場合、または実行中のドキュメントテーブルにない場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッド () を呼び出して、 `OSE_ChooseBestStdEditor` ファイルの標準エディターを開きます。

     メソッドを呼び出すと、IDE は次のタスクを実行します。

    1. IDE は、レジストリの Editor/{guidEditorType}/Extensions サブキーをスキャンして、ファイルを開くことができるエディターを特定し、この実行に最も高い優先順位を与えます。

    2. IDE によってファイルを開くことができるエディターが特定されると、IDE はを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ます。 エディターがこのメソッドを実装すると、IDE が新しく開いたドキュメントを呼び出すために必要な情報が返され <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> ます。

    3. 最後に、IDE は通常の永続化インターフェイス (など) を使用してドキュメントを読み込み <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> ます。

    4. IDE で、階層または階層項目が使用可能であると判断された場合、IDE はプロジェクトのメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> メソッド呼び出しで再び渡すプロジェクトレベルのコンテキストポインターを取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> ます。

4. <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> エディターがプロジェクトからコンテキストを取得できるようにする場合は、ide がプロジェクトでを呼び出すと、ide へのポインターが返されます。

     この手順を実行すると、プロジェクトはエディターに追加のサービスを提供できます。

     ドキュメントビューまたはドキュメントビューオブジェクトがウィンドウフレームに正常に配置されている場合は、を呼び出すことによって、オブジェクトがそのデータで初期化され <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A> ます。

## <a name="see-also"></a>こちらもご覧ください
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)
- [方法: 開いているドキュメントのエディターを開く](../extensibility/how-to-open-editors-for-open-documents.md)
- [[ファイルを開く] コマンドを使用してファイルを表示する](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
