---
title: '[新しい項目の追加] ダイアログボックスへの項目の追加 |Microsoft Docs'
description: Visual Studio の [新しい項目の追加] ダイアログボックスに項目を追加して、プロジェクトで使用するテンプレートとプロジェクト要素を表示できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 99377db0e835de8d84485d0254d84892a360f5f0
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190162"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログボックスへの項目の追加
[ **新しい項目の追加** ] ダイアログボックスに項目を追加するプロセスは、レジストリキーから開始されます。 次のレジストリエントリに示すように、[ **Additemtemplates** ] セクションには、[ **新しい項目の追加** ] ダイアログボックスで使用できる項目が配置されているディレクトリのパスと名前が含まれています。

> [!NOTE]
> コードセグメントのすぐ後のテーブルには、レジストリエントリに関する追加情報が含まれています。

 このセクションは、[ **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects**] の下にあります。

 最初の GUID は、この種類のプロジェクトの CLSID です。2番目の GUID は、項目の追加テンプレートに登録されているプロジェクトの種類を示します。

 **\\{C061DB26-5833-11D2-96F5-000000000000} \\AddItemTemplates \\ templates dir \\ {ACEF4EB2-57CF-11D2-96F4-000000000000} \\ 1**

 **@** = #6

 **Templates**  =  \\ ディレクトリ &lt;Visual Studio SDK のインストールパス &gt; \\ vsintegration \\ &lt; フォルダー &gt; \\ &lt; &gt; \\ &lt; &gt; \\ &lt; があります。&gt;

 **Sortpriority** = dword: 00000064

| 名前 | Type | データ ( *.rgs* ファイルから) | 説明 |
|------------------|-----------| - | - |
| @ (既定値) | REG_SZ | % IDS_ADDITEM_TEMPLATES_ENTRY% | 項目テンプレートの **追加** 用のリソース ID。 |
| Val Templates ディレクトリ | REG_SZ | % TEMPLATE_PATH% \\ &lt; SomeProjectItems&gt; | **新しい項目の追加** ウィザードのダイアログに表示されるプロジェクト項目のパス。 |
| Val SortPriority | REG_DWORD | 100 ( [!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)] ) | [ **新しい項目の追加** ] ダイアログボックスに表示されるファイルのツリーノード内の並べ替え順序を決定します。 |

> [!NOTE]
> Visual C# の GUID と Visual Basic のプロジェクトの種類は次のとおりです。
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 **Templates dir**( *% TEMPLATE_PATH% \\ &lt; SomeProjectItems &gt;*) に一覧表示されているディレクトリは、[**新しい項目の追加**] ダイアログボックスツリーの左側にあるノードです。 ツリー内のその他の要素は、そのルートディレクトリ内のサブディレクトリに基づいています。 プロジェクトに追加できるファイルは、[ **新しい項目の追加** ] ダイアログボックスの右ペインの項目です。

 通常、このフォルダーには、テンプレート HTML や *.cpp* ファイルなどのプロジェクトのテンプレートファイルと、ウィザードを起動するための *.vsz* ファイルが含まれます。 項目の表示方法を制御するには、ディレクトリ名とアイコンをローカライズするための *vsdir* ファイルを含めることもできます。 ローカライズされた文字列は、[ **新しい項目の追加** ] ダイアログボックスツリー内のこのノードを表すダイアログボックスに表示されるキャプションです。

 ただし、すべてのファイルを1つの *.vsdir* ファイルに含める必要はありません。 ディレクトリ内のすべての項目に対して1つの *.vsdir* ファイルを使用できます。 詳細については、「 [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md) と [テンプレートディレクトリの説明 (.vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)」を参照してください。

> [!NOTE]
> テンプレートディレクトリ内の *.vsdir* ファイルは省略可能です。 プロジェクト要素をディレクトリに配置し、[ **新しい項目の追加** ] ダイアログボックスに表示するだけの場合は、 **templates dir** ステートメントで指定された templates ディレクトリにそのファイルを配置できます。 その後、そのプロジェクトの [ **新しい項目の追加** ] ダイアログボックスの右ペインにファイルが表示されます。 ただし、ファイルまたはアイコンのローカライズされたキャプションを表示する場合は、templates ディレクトリに少なくとも1つの *.vsdir* ファイルを含める必要があります。

## <a name="group-project-items"></a>プロジェクト項目のグループ化
 [ **新しい項目の追加** ] ダイアログボックスツリーのフォルダーにテンプレートグループを含めるには、ルートテンプレートディレクトリの下にサブディレクトリがあり、その中に項目が含まれている必要があります。 [ **新しい項目の追加** ] ダイアログボックスがユーザーに表示されると、サブフォルダーも表示され、そこからプロジェクト要素を選択できるようになります。

 コードセグメント内の並べ替えの優先順位によって、ツリーノードの他の要素を基準として、ツリー内でこのテンプレートディレクトリが作成される場所が決まります。 [ **新しい項目の追加** ] ダイアログボックスでは、並べ替えの優先順位がすべて含まれている必要があります。これにより、ダイアログボックスの正しい場所に項目が表示されるようになります。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>[**新しい項目の追加**] ダイアログボックスに表示される内容をフィルター処理するためのインターフェイスを実装することもできます。 このインターフェイスを実装することで、50テンプレートやウィザードファイルなど、1つのテンプレートディレクトリをディスク上に設定できます。 この方法では、1つのプロジェクトの種類に属する20個のファイル、別のプロジェクトの種類に属する他の30個のファイル、および一般的な種類のプロジェクトで使用できるすべてのファイルを含むさまざまな種類のプロジェクトを作成できます。 この方法では、作成されるプロジェクトテンプレートに応じて、異なるテンプレートファイルのセットを表示できます。

 たとえば、Visual Basic プロジェクトでは、Web プロジェクトとクライアントプロジェクトがある場合があります。 Web フォームは、クライアントプロジェクトに追加するのに便利な項目ではなく、Web サーバープロジェクトに追加するのに役立つ項目ではありません。 そのため、両方の種類のプロジェクトのすべてのファイルを含む1つのテンプレートディレクトリを作成できます。 次に、を実装することで、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> プロジェクトのプロジェクト設定またはプロジェクト設定の種類に基づいて表示されない項目を非表示にすることができます。

## <a name="filter-project-items"></a>プロジェクト項目のフィルター
 `IVsFilterAddProjectItemDlg2` では、次の方法でツリー (左側のウィンドウ) およびプロジェクトファイル (右側のウィンドウ) の要素をフィルター処理できます。

- によって提供される、ローカライズされた名前 ( *.vsdir* ファイルに格納されているダイアログボックスに表示されるキャプション) `IVsFilterAddProjectItemDlg` 。

- によって提供される、ディスク上のファイルおよびフォルダーの実際の名前 (ローカライズされ *ていないファイル)* `IVsFilterAddProjectItemDlg` 。

- カテゴリ別。によって提供され `IVsFilterAddProjectItemDlg2` ます。

  カテゴリでフィルター処理するには、Visual Basic の *Web フォーム* や *クライアント項目* など、 *.vsdir* ファイル内の項目にカテゴリ文字列を指定します。 次に、ダイアログボックスコードは、 *.vsdir* ファイルからカテゴリ分類を取得し、それを渡します。 その後、その情報をの実装に渡して `IVsFilterAddProjectItemDlg2` 、[ **新しい項目の追加** ] ダイアログボックスをカテゴリ別にフィルター処理できます。 Web ページまたはクライアントの Win32 アプリケーションケースとして、項目をフィルター処理することもできます。 また、 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] タグ付き項目は、Microsoft Foundation Classes (MFC) 項目または active template library (ATL) 項目として識別できます。 これらの項目を識別すると、プロジェクトシステムで独自の分類を定義して、カテゴリと分類に基づいてシステムをフィルター処理できるようにすることができます。

  このフィルター機能を実装する場合は、非表示にする必要があるすべての項目のテーブルをマップする必要はありません。 単純に項目を型に分類し、その分類を *.vsdir* ファイルに含めることができます。 その後、インターフェイスを実装することによって、特定の分類を持つすべての項目を非表示にすることができます。 このようにして、[ **新しい項目の追加** ] ダイアログボックスの項目を、プロジェクト内の状態に基づいて動的に設定できます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [プロジェクトの拡張に通常使用されるオブジェクトの Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [テンプレートディレクトリの説明 (.vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
