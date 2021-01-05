---
title: 複数のドキュメントビューのサポートMicrosoft Docs
description: Visual Studio SDK でカスタムエディターに個別のドキュメントデータとドキュメントビューオブジェクトを使用して、ドキュメントの複数のビューを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c1d99f4beb000d4b48435b9215a01f31ef8e936
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97716095"
---
# <a name="supporting-multiple-document-views"></a>複数のドキュメント ビューのサポート
エディター用に個別のドキュメントデータとドキュメントビューオブジェクトを作成することにより、ドキュメントの複数のビューを提供できます。 追加のドキュメントビューが役に立つ場合は、次のような場合があります。

- 新しいウィンドウのサポート: エディターで同じ種類の複数のビューを提供するには、エディターで既にウィンドウを開いているユーザーが [**ウィンドウ**] メニューの [**新しいウィンドウ**] をクリックして新しいウィンドウを開くことができるようにします。

- フォームとコードビューのサポート: エディターがさまざまな種類のビューを提供する必要があります。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]たとえば、には、フォームビューとコードビューの両方が用意されています。

  詳細については、Visual Studio パッケージテンプレートによって作成されたカスタムエディタープロジェクトの EditorFactory.cs ファイルにある CreateEditorInstance プロシージャを参照してください。 このプロジェクトの詳細については、「 [チュートリアル: カスタムエディターを作成](../extensibility/walkthrough-creating-a-custom-editor.md)する」を参照してください。

## <a name="synchronizing-views"></a>ビューの同期
 複数のビューを実装する場合、ドキュメントデータオブジェクトは、すべてのビューがデータと同期されるようにします。 のイベント処理インターフェイスを使用して <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 、複数のビューをデータと同期することができます。

 オブジェクトを使用して <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 複数のビューを同期しない場合は、ドキュメントデータオブジェクトに加えられた変更を処理する独自のイベントシステムを実装する必要があります。 さまざまなレベルの粒度を使用して、複数のビューを最新の状態に保つことができます。 [最大の粒度] の設定では、1つのビューを入力すると、すぐに他のビューが更新されます。 最小粒度を使用すると、他のビューはアクティブ化されるまで更新されません。

## <a name="determining-whether-document-data-is-already-open"></a>ドキュメントデータが既に開いているかどうかを確認する
 次の図に示すように、統合開発環境 (IDE: integrated development environment) で実行中のドキュメントテーブル (RDT) を使用すると、ドキュメントのデータが既に開いているかどうかを追跡できます。

 ![Docdataview グラフィック](../extensibility/media/docdataview.gif "Docdataview") 複数のビュー

 既定では、各ビュー (ドキュメントビューオブジェクト) は、独自のウィンドウフレーム () に含まれてい <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> ます。 ただし、既に説明したように、ドキュメントデータは複数のビューに表示できます。 これを有効にするために、Visual Studio は RDT を調べて、問題のドキュメントが既にエディターで開かれているかどうかを確認します。 IDE でエディターを <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 作成するためにを呼び出すと、パラメーターに NULL 以外の値が返されると、 `punkDocDataExisting` ドキュメントが別のエディターで既に開かれていることが示されます。 RDT 関数の詳細については、「 [Document Table の実行](../extensibility/internals/running-document-table.md)」を参照してください。

 の実装では <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 、に返されたドキュメントデータオブジェクトを調べ `punkDocDataExisting` て、ドキュメントデータがエディターに適しているかどうかを判断します。 (たとえば、html エディターで表示できるのは HTML データだけです)。適切な場合、エディターファクトリはデータの2番目のビューを提供する必要があります。 `punkDocDataExisting`パラメーターがでない場合は `NULL` 、ドキュメントデータオブジェクトが別のエディターで開かれている可能性があります。または、ドキュメントデータが同じエディターを持つ別のビューで既に開かれている可能性があります。 ドキュメントデータがエディターファクトリでサポートされていない別のエディターで開かれている場合、Visual Studio はエディターファクトリを開くことができません。 詳細については、「 [方法: ドキュメントデータにビューをアタッチ](../extensibility/how-to-attach-views-to-document-data.md)する」を参照してください。
