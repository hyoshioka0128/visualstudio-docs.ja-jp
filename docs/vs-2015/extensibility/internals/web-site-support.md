---
title: Web サイトのサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1a96504783de466551c6fb9d055b95ba38df760
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687690"
---
# <a name="web-site-support"></a>Web サイト サポート
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Web サイトプロジェクトシステムは、Web プロジェクトを作成するプロジェクトシステムです。 Web プロジェクトは、Web アプリケーションを作成します。 Web サイトプロジェクトは、コードが関連付けられている Web ページごとに1つの実行可能ファイルを生成します。 /App_Code フォルダー内のソースコードファイルから、追加の実行可能ファイルが生成されます。  
  
 Web サイトプロジェクトシステムは、既存のプロジェクトシステムにテンプレートと登録属性を追加することによって作成されます。 これらの属性のいずれかによって、言語の IntelliSense プロバイダーが選択されます。 IntelliSense プロバイダーの実装は、キャッシュされていないスマート Web ページが要求されたときに、参照を処理し、言語コンパイラを呼び出します。  
  
 Web ページのコンパイルに使用される言語コンパイラは、に登録されている必要があり [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ます。 次の例に示すように、Web.config ファイルで[ \<compiler> 要素](https://msdn.microsoft.com/library/7a151659-b803-4c27-b5ce-1c4aa0d5a823)を使用して、コンパイラを登録できます。  
  
```  
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>  
```  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Web サイト サポートのテンプレート](../../extensibility/internals/web-site-support-templates.md)  
 新しい Web サイトプロジェクトと関連アイテムを作成するために使用できるテンプレートの一覧を示します。  
  
 [Web サイト サポートの属性](../../extensibility/internals/web-site-support-attributes.md)  
 Web サイトプロジェクトをとに接続する登録属性を [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 示し [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ます。  
  
## <a name="related-sections"></a>関連項目  
 [Web プロジェクト](../../extensibility/internals/web-projects.md)  
 2種類の Web プロジェクト、Web サイトプロジェクト、および Web アプリケーションプロジェクトの概要について説明します。
