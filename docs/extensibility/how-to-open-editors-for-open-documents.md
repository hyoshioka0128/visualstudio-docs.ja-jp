---
title: '[方法] 開いているドキュメントのエディタを開く |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d0986573ac0d53427f6490370be2bfa1c4cbe7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710921"
---
# <a name="how-to-open-editors-for-open-documents"></a>[方法] 開いているドキュメントのエディターを開く
プロジェクトがドキュメント ウィンドウを開く前に、プロジェクトは、ファイルが別のエディターのドキュメント ウィンドウで既に開いているかどうかを判断する必要があります。 ファイルは、プロジェクト固有のエディターで開くか、または に登録されている標準エディターの 1[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]つを使用できます。

## <a name="open-a-project-specific-editor"></a>プロジェクト固有のエディターを開く
 既に開いているファイルのプロジェクト固有のエディターを開くには、次の手順を使用します。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>開いているファイルのプロジェクト固有のエディターを開くには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> メソッドを呼び出します。

    この呼び出しは、ドキュメントの階層、階層アイテム、およびウィンドウ フレームへのポインタを返します (必要に応じて)。

2. ドキュメントが開いている場合、プロジェクトはドキュメント データ オブジェクトが存在するかどうか、またはドキュメント ビュー オブジェクトも存在するかどうかを確認する必要があります。

   - ドキュメント ビュー オブジェクトが存在し、このビューが別の階層または階層アイテムに対するビューである場合、プロジェクトはビューのウィンドウ フレームへのポインターを使用して、既存のウィンドウを再表示します。

   - ドキュメント ビュー オブジェクトが存在し、このビューが同じ階層項目と階層アイテムに対して存在する場合、プロジェクトは、基になるドキュメント データ オブジェクトにアタッチできる場合に、2 番目のビューを開くことができます。 それ以外の場合、プロジェクトはビューのウィンドウ フレームへのポインターを使用して、既存のウィンドウを再表示する必要があります。

   - ドキュメント データ オブジェクトのみが存在する場合、プロジェクトは、ドキュメント データ オブジェクトをそのビューに使用できるかどうかを判断する必要があります。 ドキュメント データ オブジェクトに互換性がある場合は、「[プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)」で説明されている手順を実行します。

     ドキュメント データ オブジェクトに互換性がない場合は、ファイルが現在使用中であることを示すエラーがユーザーに表示されます。 このエラーは、ユーザーがコア テキスト エディター以外のエディターを使用してファイルを開こうとすると同時にファイルをコンパイルする場合など、一時的な場合にのみ表示されます[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 コア テキスト エディターは、ドキュメント データ オブジェクトをコンパイラと共有できます。

3. ドキュメント データ オブジェクトまたはドキュメント ビュー オブジェクトがないためにドキュメントが開いていない場合は、「[プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)」の手順を実行します。

## <a name="open-a-standard-editor"></a>標準エディタを開く
 既に開いているファイルの標準エディターを開くには、次の手順を使用します。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>開いているファイルの標準エディタを開くには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> を呼び出します。

     このメソッドは、まず を呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>すことによって、ドキュメントが開かれていないことを確認します。 ドキュメントが既に開いている場合は、エディタ ウィンドウが再表示されます。

2. ドキュメントが開いていない場合は、「[方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)」の手順を実行します。

## <a name="see-also"></a>関連項目
- [プロジェクト アイテムを開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)
