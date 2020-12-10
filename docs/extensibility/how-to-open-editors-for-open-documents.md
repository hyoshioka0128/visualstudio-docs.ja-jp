---
title: '方法: 開いているドキュメントのエディターを開く |Microsoft Docs'
description: 標準またはプロジェクト固有のエディターでファイルを開く方法について説明します。 プロジェクトがドキュメントウィンドウを開いたときに、ファイルが既に開いているかどうかを確認する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6d329ce7b4f4b74b8ff77357393ffe9383a3977e
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993862"
---
# <a name="how-to-open-editors-for-open-documents"></a>方法: 開いているドキュメントのエディターを開く
プロジェクトでドキュメントウィンドウを開く前に、まず、そのファイルが別のエディターのドキュメントウィンドウで既に開いているかどうかを確認する必要があります。 このファイルは、プロジェクト固有のエディターで開くか、に登録されている標準エディターのいずれかで開くことができ [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

## <a name="open-a-project-specific-editor"></a>プロジェクト固有のエディターを開く
 既に開いているファイルのプロジェクト固有のエディターを開くには、次の手順に従います。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>開いているファイルのプロジェクト固有のエディターを開くには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> メソッドを呼び出します。

    この呼び出しは、ドキュメントの階層、階層アイテム、およびウィンドウフレームへのポインターを返します (該当する場合)。

2. ドキュメントが開いている場合、プロジェクトは、ドキュメントデータオブジェクトのみが存在するかどうか、またはドキュメントビューオブジェクトも存在するかどうかを確認する必要があります。

   - ドキュメントビューオブジェクトが存在し、このビューが別の階層または階層アイテム用である場合、プロジェクトはビューのウィンドウフレームへのポインターを使用して、既存のウィンドウを resurface します。

   - ドキュメントビューオブジェクトが存在し、このビューが同じ階層および階層アイテムに対して存在する場合、基になるドキュメントデータオブジェクトにアタッチできる場合、プロジェクトは2番目のビューを開くことができます。 それ以外の場合、プロジェクトはビューのウィンドウフレームへのポインターを使用して、既存のウィンドウを resurface する必要があります。

   - ドキュメントデータオブジェクトのみが存在する場合、プロジェクトは、そのビューにドキュメントデータオブジェクトを使用できるかどうかを判断する必要があります。 ドキュメントデータオブジェクトに互換性がある場合は、「 [プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)」で説明されている手順を実行します。

     ドキュメントデータオブジェクトに互換性がない場合は、ファイルが現在使用中であることを示すエラーがユーザーに表示されます。 このエラーは、ユーザーがコアテキストエディター以外のエディターを使用してファイルを開こうとしたときに、ファイルがコンパイルされている場合など、一時的な場合にのみ表示され [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 コアテキストエディターでは、ドキュメントデータオブジェクトをコンパイラと共有できます。

3. ドキュメントデータオブジェクトまたはドキュメントビューオブジェクトがないためにドキュメントが開いていない場合は、「 [プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)」の手順を実行します。

## <a name="open-a-standard-editor"></a>標準エディターを開く
 既に開いているファイルの標準エディターを開くには、次の手順に従います。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>開いているファイルの標準エディターを開くには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> を呼び出します。

     このメソッドは、まず、を呼び出してドキュメントがまだ開かれていないことを確認 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> します。 ドキュメントが既に開いている場合、そのエディターウィンドウは resurfaced です。

2. ドキュメントが開いていない場合は、 [「方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)」の手順を完了します。

## <a name="see-also"></a>こちらもご覧ください
- [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)
