---
title: Web プロジェクトの基本 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 09e33248ca264fefa79a8d5d5fa5d0cfa3d2da1d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703547"
---
# <a name="web-project-essentials"></a>Web プロジェクトの基本情報
Web プロジェクトは Web アプリケーションを作成します。 Web プロジェクトを使用して、スマート Web ページを含む Web アプリケーションを作成できます。 スマート Web ページには、要求に応じて Web ページをレンダリングするサーバー側のコードがあります。

 や[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)][!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]などの従来のプログラミング言語を使用して、ユーザーから情報を収集および処理したり、データベースに格納したりするためのスマート Web ページを作成できます。

- 分離コード モデルは、依存ソース コード ファイルを、ファイル拡張子 .aspx または .asmx を持つ Web ページに関連付けます。 たとえば、hello.aspx には、依存ソース コード ファイルがhello.aspx.cs。

- スマート Web ページに関連付けられたサーバー側コードは、Web サイト /bin フォルダ内の実行可能ファイルにコンパイルされます。

- 特定の Web ページに関連付けられていないヘルパー クラスなどの追加のソース コード ファイルは、Web サイト /App_Code フォルダーにあります。

  - Web サイト プロジェクト (WSP) では、スマート Web ページごとに 1 つの実行可能ファイルが生成されます。 追加の実行可能ファイルは、/App_Code フォルダー内の任意のソース コード ファイルから生成されます。

  - Web アプリケーション プロジェクト (WAP) では、すべてのスマート Web ページのコードと /App_Code フォルダ内のすべてのソース ファイルを結合した単一の実行可能ファイルが生成されます。

- Web プロジェクトのソリューション ファイルは、Web サイト自体とは別に配置されます。 既定では、ソリューション ファイルは \ドキュメントと設定\\*にあなたのアカウント*\マイ ドキュメント\\*\<ビジュアル スタジオ ####>* \プロジェクト\\*YourWebSite*にあります。

  > [!NOTE]
  > ソリューション ファイルを Web サイトに保存する場合は、そのファイルを移動して再度開いてください。

- ソリューション ファイルが存在しない Web サイトを Visual Studio で開くと、そのソリューション ファイルに対して新しいソリューション ファイルが自動的に生成されます。

- Web プロジェクトにはプロジェクト ファイルがありません。 プロジェクト情報は、ソリューション ファイル、web.config ファイル、およびその他の場所に格納されます。

- Web プロジェクトにグローバル プロパティを追加すると、Web プロジェクト ソリューション フォルダにストレージ ファイルが自動的に作成されます。

- スマート Web ページは、Page ディレクティブまたはスクリプト runat="server" >\<タグを使用して、サーバー側のプログラミング言語に関連付けることができます。

- また、Web ページには、任意のスクリプト言語で記述されたクライアント側のスクリプト ブロックをいくつでも含めることができます。

- Web サイト プロジェクト システムは、プロジェクトテンプレートと項目テンプレートをプロジェクトに追加[!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)]し、登録することで実装されます。

- WAP システムは、プロジェクト の種類とも呼ばれるプロジェクト のサブタイプとして実装されます。 プロジェクト[!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)]は WAP サブタイプによってフレーバーされ、WAP システムが作成されます。 プロジェクトのサブタイプの詳細については、「[プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

- スマート Web ページは、HTML とサーバー側のプログラミング言語を組み合わせたページです。 サーバー側の言語は、包含言語と呼ばれます。 包含言語をサポートするには、Web プロジェクト システムがインターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage>のファミリを実装する必要があります。

  - エディターに含まれている言語をサポートするには、HTML 言語サービスは、含まれている言語サービスに含まれている言語コードの表示を延期する必要があります。

  - エラー マーカー (赤い波線) は、常にコード エディターのプライマリ バッファーに作成する必要があります。

## <a name="see-also"></a>関連項目
- [Web プロジェクト](../../extensibility/internals/web-projects.md)
