---
title: Web プロジェクトの Essentials |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 95c9f7c530d50a7eb89ebe33fad3862f036972d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825614"
---
# <a name="web-project-essentials"></a>Web プロジェクトの基本情報
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Web プロジェクトでは、Web アプリケーションを作成します。 Web プロジェクトを使用して、スマート Web ページを含む Web アプリケーションを作成できます。 スマート Web ページには、Web ページをオンデマンドでレンダリングするサーバー側コードがあります。  
  
 やなどの従来のプログラミング言語を使用すると [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 、スマート Web ページを作成して、ユーザーから情報を収集して処理したり、データベースに格納したりすることができます。  
  
- 分離コードモデルは、ファイル拡張子が .aspx または .asmx の Web ページに依存ソースコードファイルを関連付けます。 たとえば、hello .aspx は、依存するソースコードファイル hello.aspx.cs を持つ場合があります。  
  
- スマート Web ページに関連付けられているサーバー側のコードは、Web サイトの/bin フォルダーにある実行可能ファイルにコンパイルされます。  
  
- 特定の Web ページに関連付けられていないヘルパークラスなどの追加のソースコードファイルは、Web サイト/App_Code フォルダーにあります。  
  
  - Web サイトプロジェクト (WSP) では、スマート Web ページごとに1つの実行可能ファイルが生成されます。 /App_Code フォルダー内の任意のソースコードファイルから、追加の実行可能ファイルが生成されます。  

  - Web アプリケーションプロジェクト (WAP) は、すべてのスマート Web ページのコードと、/App_Code フォルダー内のすべてのソースファイルを組み合わせた1つの実行可能ファイルを生成します。  
  
- Web プロジェクトのソリューションファイルは、Web サイト自体とは別に配置されます。 既定では、ソリューションファイルは \Documents にあり、[設定] [アカウント] [\My ドキュメント]、[web サイトの設定] にあり \\ *YourAccount* \\ *\<Visual Studio ####>* \\ *YourWebSite*ます。  
  
    > [!NOTE]
    > ソリューションファイルを Web サイトと共に保持する場合は、そのファイルを移動して再度開きます。  
  
- ソリューションファイルのない Web サイトを Visual Studio に開いた場合は、新しいソリューションファイルが自動的に生成されます。  
  
- Web プロジェクトにはプロジェクトファイルがありません。 プロジェクト情報は、ソリューションファイル、web.config ファイル、その他の場所に格納されます。  
  
- グローバルプロパティを Web プロジェクトに追加すると、Web プロジェクトソリューションフォルダーにストレージファイルが自動的に作成されます。  
  
- ページディレクティブまたはタグを使用すると、スマート Web ページをサーバー側のプログラミング言語に関連付けることができ \<script runat="server"> ます。  
  
- また、Web ページには、任意のスクリプト言語で記述されたクライアント側スクリプトブロックをいくつでも含めることができます。  
  
- プロジェクトと項目テンプレートを追加し、プロジェクトに登録することで、Web サイトプロジェクトシステムが実装され [!INCLUDE[vwprvw](../../includes/vwprvw-md.md)] ます。  
  
- WAP システムはプロジェクトのサブタイプとして実装されます。プロジェクトのフレーバーとも呼ばれます。 Wap [!INCLUDE[vwprvw](../../includes/vwprvw-md.md)] システムを作成するために、プロジェクトは wap サブタイプによって flavored されます。 プロジェクトのサブタイプの詳細については、「 [プロジェクトのサブ](../../extensibility/internals/project-subtypes.md)タイプ」を参照してください。  
  
- スマート Web ページは、HTML とサーバー側プログラミング言語を組み合わせたものです。 サーバー側の言語は、含まれる言語と呼ばれます。 含まれている言語をサポートするには、Web プロジェクトシステムがインターフェイスのファミリを実装する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> ます。  
  
  - エディターで含まれている言語をサポートするには、HTML 言語サービスが、含まれている言語サービスに含まれる言語コードの表示を延期する必要があります。  

  - エラーマーカー (赤の squigglies) は、常にコードエディターのプライマリバッファーに作成する必要があります。  
  
## <a name="see-also"></a>参照  
 [Web プロジェクト](../../extensibility/internals/web-projects.md)
