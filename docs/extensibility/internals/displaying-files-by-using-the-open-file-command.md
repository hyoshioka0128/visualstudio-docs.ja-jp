---
title: '[ファイルを開く] コマンドを使用してファイルを表示する |マイクロソフトドキュメント'
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
ms.openlocfilehash: cc18442c55b6989c4d8668e1425fdd62a2d4b1b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708594"
---
# <a name="display-files-by-using-the-open-file-command"></a>[ファイルを開く] コマンドを使用してファイルを表示する
次の手順では、 の [ファイル]**メニューで**使用できる [ファイルを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**開く**] コマンドを IDE で処理する方法について説明します。 また、このコマンドから発信された呼び出しに対してプロジェクトがどのように応答するかについても説明します。

 ユーザーが [ファイル]**メニューの**[**ファイルを開く**] をクリックし、[**ファイルを開く**] ダイアログ ボックスでファイルを選択すると、次の処理が実行されます。

1. 実行中のドキュメントテーブルを使用して、IDE は、ファイルがプロジェクトで既に開いているかどうかを判断します。

    - ファイルが開いている場合、IDE はウィンドウを再表示します。

    - ファイルが開いていない場合、IDE は各<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>プロジェクトに対してクエリを実行し、ファイルを開くことができるプロジェクトを判別します。

        > [!NOTE]
        > のプロジェクト実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>で、プロジェクトがファイルを開くレベルを示す優先度値を指定します。 優先順位の値は、列挙<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>体で提供されます。

2. 各プロジェクトは、ファイルを開くプロジェクトに対する重要度を示す優先度レベルで応答します。

3. IDE では、次の基準を使用して、ファイルを開くプロジェクトを決定します。

    - 最も高い優先度 (`DP_Intrinsic`) で応答するプロジェクトがファイルを開きます。 複数のプロジェクトがこの優先度で応答する場合、最初に応答するプロジェクトがファイルを開きます。

    - 最も高い優先度 ( )`DP_Intrinsic`で応答するプロジェクトがなく、すべてのプロジェクトが同じ低い優先度で応答する場合、アクティブなプロジェクトがファイルを開きます。 アクティブなプロジェクトがない場合、最初に応答したプロジェクトがファイルを開きます。

    - ファイルの所有権を要求するプロジェクトがない場合`DP_Unsupported`は、 ( その他のファイル ) プロジェクトによってファイルが開きます。

         その他のファイル プロジェクトのインスタンスが作成されると、プロジェクトは常に値`DP_CanAddAsExternal`を返します。 この値は、プロジェクトがファイルを開くことができることを示します。 このプロジェクトは、他のプロジェクトにない開いているファイルを収容するために使用されます。 このプロジェクトの項目のリストは保持されません。このプロジェクトは、ファイルを開くときに使用される場合にのみ**ソリューション エクスプローラー**に表示されます。

         その他のファイル プロジェクトでファイルを開くことができると示されていない場合、プロジェクトのインスタンスは作成されていません。 この場合、IDE は「その他のファイル」プロジェクトのインスタンスを作成し、ファイルを開くようにプロジェクトに指示します。

4. IDE は、ファイルを開くプロジェクトを決定すると、そのプロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>のメソッドを呼び出します。

5. プロジェクトは、プロジェクト固有のエディターまたは標準エディターを使用してファイルを開くオプションを持っています。 詳細については、「方法[: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」および「[方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [[ファイルから開く] コマンドを使用してファイルを表示する](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)
