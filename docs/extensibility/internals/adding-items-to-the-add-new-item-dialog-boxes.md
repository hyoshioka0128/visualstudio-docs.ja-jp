---
title: '[新しい項目の追加] ダイアログ ボックスに項目を追加する |マイクロソフトドキュメント'
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
ms.openlocfilehash: af7f9e5c792785a23ad1674a50abeb4eb6d3cba9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710212"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>[新しい項目の追加] ダイアログ ボックスに項目を追加する
**[新しい項目の追加**] ダイアログ ボックスに項目を追加するプロセスは、レジストリ キーで開始されます。 次のレジストリ エントリに示すように **、AddItemTemplates**セクションには、**新しい項目の追加**ダイアログ ボックスで使用可能になった項目が格納されているディレクトリのパスと名前が含まれています。

> [!NOTE]
> コード セグメントの直後の表には、レジストリ エントリに関する追加情報が含まれています。

 このセクションは **、HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\14.0Exp\プロジェクト**にあります。

 最初の GUID は、この種類のプロジェクトの CLSID です。2 番目の GUID は、項目の追加テンプレートに登録されているプロジェクトの種類を示します。

 **\\{C061DB26-5833-11D2-96F5-0000000000}テンプレートの追加ディレクトリ\\{ACEF4EB2-57CF-11D2-96F4-0000000000}\\ \\\\**

 **@**= #6

 **テンプレートディレクトリビジュアル** = \\&lt;スタジオSDKインストールパス&gt;\\VS統合\\&lt;いくつかのフォルダ&gt;\\&lt;いくつかのパッケージ&gt;\\&lt;いくつかの&gt;\\プロジェクト&lt;いくつかのプロジェクトアイテム&gt;

 **ソート優先順位**= ドード:00000064

| 名前 | Type | データ *(.rgs*ファイルから) | 説明 |
|------------------|-----------| - | - |
| @ (デフォルト) | REG_SZ | #%IDS_ADDITEM_TEMPLATES_ENTRY% | **項目追加**テンプレートのリソース ID。 |
| ヴァル テンプレートディレクトリ | REG_SZ | %TEMPLATE_PATH%\\&lt;一部のプロジェクトアイテム&gt; | **新しい項目の追加**ウィザードのダイアログに表示されるプロジェクト項目のパス。 |
| ヴァル ソート優先順位 | REG_DWORD | 100[!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)]( ) | [**新しい項目の追加**] ダイアログ ボックスに表示されるファイルのツリー ノードでの並べ替え順序を指定します。 |

> [!NOTE]
> Visual C# および Visual Basic プロジェクトの種類の GUID は次のとおりです。
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 **TemplatesDir**に一覧表示されているディレクトリは *%TEMPLATE_PATH%\\&lt;&gt;SomeProjectItems*で、**新しい項目の追加**ダイアログ ボックス ツリーの左側にあるノードです。 ツリー内の追加要素は、そのルート ディレクトリ内のサブディレクトリに基づいています。 プロジェクトに追加できるファイルは、[**新しい項目の追加**] ダイアログ ボックスの右側のウィンドウの項目です。

 通常、このフォルダには、テンプレート HTML ファイルや *.cpp*ファイルなどのプロジェクトのテンプレート ファイルと、ウィザードを起動するための *.vsz*ファイルが含まれます。 項目の表示方法を制御するために、ディレクトリ名とアイコンをローカライズするための *.vsdir*ファイルを含めることもできます。 ローカライズされた文字列は、ダイアログ ボックスに表示されるキャプションで、[**新しい項目の追加**] ダイアログ ボックス ツリーのこのノードを表します。

 ただし、1 つの *.vsdir*ファイルにすべてを含める必要はありません。 ディレクトリ内のすべての項目に対して 1 つの *.vsdir*ファイルを作成できます。 詳細については、「[ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)」および[「テンプレート ディレクトリの説明 (.vsdir) ファイル 」](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)を参照してください。

> [!NOTE]
> テンプレート ディレクトリ内の *.vsdir*ファイルはオプションです。 プロジェクト要素をディレクトリに配置し、[**新しい項目の追加**] ダイアログ ボックスに表示するだけの場合は **、TemplatesDir**ステートメントで指定された templates ディレクトリにそのファイルを配置できます。 その後、そのプロジェクトの **[新しい項目の追加**] ダイアログ ボックスの右側のウィンドウにファイルが表示されます。 ただし、ファイルまたはアイコンのローカライズされたキャプションを表示する場合は、テンプレート ディレクトリに少なくとも 1 つの *.vsdir*ファイルを含める必要があります。

## <a name="group-project-items"></a>プロジェクト項目のグループ化
 **[新しい項目の追加]** ダイアログ ボックスツリーのフォルダにテンプレート グループを含める場合は、ルート テンプレート ディレクトリの下に、それらの項目を含むサブディレクトリが必要です。 [**新しい項目の追加**] ダイアログ ボックスがユーザーに表示されると、ユーザーはサブフォルダも表示され、そこからプロジェクト要素を選択できるようになります。

 コード セグメントの並べ替えの優先順位によって、ツリー ノードの他の要素に対して、このテンプレート ディレクトリがツリー内で作成される場所が決まります。 [**新しい項目の追加]** ダイアログ ボックスでは、ダイアログ ボックスの正しい場所にアイテムが表示されるように、並べ替えの優先順位がすべて必要です。

 また、インターフェイスを実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>して、[**新しい項目の追加]** ダイアログ ボックスに表示される内容をフィルター処理することもできます。 このインターフェイスを実装すると、50 個のテンプレート ファイルやウィザード ファイルなどを含むディスク上に 1 つのテンプレート ディレクトリを設定できます。 このように、1 つのプロジェクトの種類に属する 20 のファイル、別のプロジェクトの種類に属する他の 30 ファイル、および一般的な種類のプロジェクトで使用できるすべてのファイルを使用して、異なるプロジェクトの種類を設定できます。 この方法で、作成するプロジェクト テンプレートに応じて、異なるテンプレート ファイルのセットを表示できます。

 たとえば、Visual Basic プロジェクトでは、Web プロジェクトとクライアント プロジェクトを使用できます。 Web フォームは、クライアント プロジェクトに追加する場合には役に立たない項目であり、Windows フォームは Web サーバー プロジェクトに追加する際に役立つ項目ではありません。 したがって、両方の種類のプロジェクトのすべてのファイルを含む 1 つのテンプレート ディレクトリを作成できます。 その後、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>を実装することにより、プロジェクトのプロジェクトまたはプロジェクトの設定の種類に基づいて表示しない項目を非表示にできます。

## <a name="filter-project-items"></a>プロジェクト項目のフィルター処理
 `IVsFilterAddProjectItemDlg2`では、ツリー (左側のペイン) とプロジェクト ファイル (右側のペイン) の要素を次のようにフィルタ処理できます。

- で提供されるローカライズされた名前 *(.vsdir*ファイルに含まれているダイアログ ボックスに表示されるキャプション)`IVsFilterAddProjectItemDlg`によって。

- ディスク上のファイルとフォルダの実際の名前 (ローカライズされていない *-vsdir*ファイルなし) によって`IVsFilterAddProjectItemDlg`提供されます。

- カテゴリ別に提供されます`IVsFilterAddProjectItemDlg2`。

  カテゴリ別にフィルタを適用するには *、.vsdir*ファイルの項目 *(Visual* Basic の Web フォームや*クライアントアイテム*など) にカテゴリ文字列を指定します。 ダイアログ ボックスコードは *、.vsdir*ファイルからカテゴリ分類を取得し、それをユーザーに渡します。 その後、その情報を実装に渡`IVsFilterAddProjectItemDlg2`して、[**新しい項目の追加**] ダイアログ ボックスをカテゴリ別にフィルター処理できます。 Web ページまたはクライアント Win32 アプリケーションのケースのアイテムをフィルター処理することもできます。 また、タグ付けされた[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]項目を MFC (MFC) またはアクティブ なテンプレート ライブラリ (ATL) 項目として識別できます。 これらの項目を識別すると、プロジェクト システムは独自の分類を定義して、カテゴリと分類に基づいてシステムをフィルター処理できるようにします。

  このフィルタ機能を実装する場合、非表示にする必要があるすべての項目のテーブルをマップする必要はありません。 項目をタイプに分類し *、.vsdir*ファイルに分類を入れるだけで済みます。 その後、インターフェイスを実装することで、特定の分類を持つ項目を非表示にできます。 この方法では、プロジェクト内の状態に基づいて **、[新しい項目の追加]** ダイアログ ボックスの項目を動的にできます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [プロジェクトおよび項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [テンプレート ディレクトリの説明 (.vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
