---
title: '[ファイルを開く] コマンドを使用してファイルを表示する |Microsoft Docs'
description: Visual Studio 統合開発環境 (IDE) がファイルメニューの [ファイルを開く] コマンドを処理してファイルを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5a932a9b56a63069e010cb2b945de25564c2d135
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328341"
---
# <a name="display-files-by-using-the-open-file-command"></a>[ファイルを開く] コマンドを使用してファイルを表示する
次の手順では、IDE で [ **ファイルを開く** ] コマンドを処理する方法について説明します。これは、の [ **ファイル** ] メニューで使用でき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 この手順では、このコマンドからの呼び出しにプロジェクトが応答する方法についても説明します。

 ユーザーが **[ファイル] メニューの**[**ファイルを開く**] コマンドをクリックし、[ファイルを **開く**] ダイアログボックスでファイルを選択すると、次の処理が行われます。

1. IDE では、実行中のドキュメントテーブルを使用して、ファイルが既にプロジェクトで開かれているかどうかを判断します。

    - ファイルが開いている場合は、IDE によってウィンドウが resurfaces されます。

    - ファイルが開いていない場合、IDE は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> を呼び出して各プロジェクトに対してクエリを実行し、ファイルを開くことができるプロジェクトを判別します。

        > [!NOTE]
        > のプロジェクト実装で <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 、プロジェクトがファイルを開くレベルを示す優先度値を指定します。 優先順位値は、列挙体で指定され <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> ます。

2. 各プロジェクトは、ファイルを開くためにプロジェクトに必要な重要度を示す優先度レベルで応答します。

3. IDE では、次の基準を使用して、ファイルを開くプロジェクトを決定します。

    - 最高の優先順位 () で応答するプロジェクトは、 `DP_Intrinsic` ファイルを開きます。 複数のプロジェクトがこの優先順位で応答する場合は、最初に応答するプロジェクトがファイルを開きます。

    - 最も優先度の高い () で応答するプロジェクトがなく、 `DP_Intrinsic` すべてのプロジェクトが同じ優先度の低い優先順位で応答する場合、アクティブなプロジェクトはファイルを開きます。 アクティブなプロジェクトがない場合は、最初に応答するプロジェクトがファイルを開きます。

    - ファイルの所有権を要求しているプロジェクトがない場合 ( `DP_Unsupported` )、その他のファイルプロジェクトによってファイルが開きます。

         その他のファイルプロジェクトのインスタンスが作成された場合、プロジェクトは常に値を使用して応答 `DP_CanAddAsExternal` します。 この値は、プロジェクトがファイルを開くことができることを示します。 このプロジェクトは、他のプロジェクトに含まれていない開いているファイルを格納するために使用されます。 このプロジェクト内の項目の一覧は保存されません。このプロジェクトは、ファイルを開くために使用された場合にのみ **ソリューションエクスプローラー** に表示されます。

         その他のファイルプロジェクトでファイルを開くことができないことが示されていない場合は、プロジェクトのインスタンスが作成されていません。 この場合、IDE はその他のファイルプロジェクトのインスタンスを作成し、ファイルを開くようにプロジェクトに指示します。

4. IDE によってファイルを開くプロジェクトが決定されるとすぐに、その <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> プロジェクトでメソッドが呼び出されます。

5. プロジェクトには、プロジェクト固有のエディターまたは標準エディターを使用してファイルを開くオプションがあります。 詳細については、「 [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md) 」および「 [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [[ファイルを開くアプリケーションの表示] コマンドを使用してファイルを表示する](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)
