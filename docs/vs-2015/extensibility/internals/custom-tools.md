---
title: カスタムツール |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 594d564cf4a18eb0b673abd9b45b7d70e20381b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196915"
---
# <a name="custom-tools"></a>カスタム ツール
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

*カスタムツール* を使用すると、プロジェクト内の項目にツールを関連付け、ファイルが保存されるたびにそのツールを実行できます。 特定のカスタムツール ( *単一ファイルジェネレーター*と呼ばれることもあります) は、データからコードを生成したり、その逆の変換を行ったりするために頻繁に使用されます。 たとえば、単一ファイルジェネレーターは、 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 設定ファイルと .resx ファイルからソースコードを作成します。 生成されたソースコードは、設定ファイルおよび .resx ファイル内のデータへの厳密に型指定されたアクセスを提供します。 およびプロジェクトの種類では、 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] カスタムツールがサポート [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] されます。プロジェクトの種類には対応していません。 独自のプロジェクトの種類で、カスタムツールをサポートすることもできます。  
  
 カスタムツールは、インターフェイスを実装する登録済みのコンポーネントです `IVsSingleFileGenerator` 。  
  
 カスタムツールはインターフェイスオブジェクトに関連付けられて `ProjectItem` おり、デザイナーやエディターに似ています。 カスタムツールは、によって表されるファイルを `ProjectItem` 入力として受け取り、そのファイル名がメソッドによって提供される新しいファイルを書き込み `DefaultExtension` ます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)  
 インターフェイスを使用してカスタムツールを実装する方法について説明し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> ます。  
  
 [プロジェクトの既定の名前空間の決定](../../misc/determining-the-default-namespace-of-a-project.md)  
 使用されている言語に基づいて正しい名前空間を確認する方法について説明します。  
  
 [単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)  
 カスタムツールのすべてのレジストリエントリについて説明します。  
  
 [ビジュアル デザイナーへのタイプの公開](../../extensibility/internals/exposing-types-to-visual-designers.md)  
 プロジェクトシステムが、生成されたクラスと型に一時的なポータブル実行可能 (PE) ファイルを介してアクセスするためのサポートを提供する方法について説明します。  
  
 [プロジェクト項目のプロパティの保存](../../extensibility/persisting-the-property-of-a-project-item.md)  
 ソースファイルの作成者などのプロジェクト項目のプロパティをプロジェクトファイルに保存する方法について説明します。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>1 つの入力ファイルをコンパイルしたりプロジェクトに追加したりできる1つの出力ファイルに変換する、の詳細について説明します。  
  
 <xref:EnvDTE.ProjectItem>  
 `ProjectItem`プロジェクト内の項目を表すインターフェイスについて説明します。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>  
 `DefaultExtension`出力ファイル名に指定されたファイル名拡張子を取得するメソッドについて詳しく説明します。  
  
## <a name="related-sections"></a>関連項目  
 [プロジェクトの拡張](../../extensibility/extending-projects.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
