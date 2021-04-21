---
title: '方法: マネージコード拡張機能をドキュメントにアタッチする'
description: カスタマイズアセンブリを既存の Microsoft Office Word 文書または Microsoft Office Excel ブックにアタッチする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], attaching
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 60fc27345ef148fd47fdcee15924917ce63f8d68
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825499"
---
# <a name="how-to-attach-managed-code-extensions-to-documents"></a>方法: マネージコード拡張機能をドキュメントにアタッチする
  カスタマイズアセンブリは、既存の Microsoft Office Word 文書または Microsoft Office Excel ブックに添付できます。 ドキュメントまたはブックは、Visual Studio の Microsoft Office プロジェクトおよび開発ツールでサポートされている任意のファイル形式にすることができます。 詳細については、「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 カスタマイズを Word または Excel ドキュメントに添付するには、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> クラスのメソッドを使用し <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> ます。 クラスは <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> Microsoft Office がインストールされていないコンピューターで実行されるように設計されているため、この方法は、Microsoft Office 開発に直接関係のないソリューション (コンソールや Windows フォームアプリケーションなど) で使用できます。

> [!NOTE]
> 指定したドキュメントに含まれていないコントロールがコードで想定されている場合、カスタマイズは読み込みに失敗します。

### <a name="to-attach-managed-code-extensions-to-a-document"></a>マネージコード拡張機能をドキュメントにアタッチするには

1. コンソールアプリケーションや Windows フォームプロジェクトなどの Microsoft Office を必要としないプロジェクトでは、 *Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* および *Microsoft.VisualStudio.Tools.Applications.Runtime.dll* アセンブリへの参照を追加します。

2. 次の **Imports** ステートメントまたは **using** ステートメントをコードファイルの先頭に追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet4":::

3. 静的メソッド <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> を呼び出します。

     次のコード例では、オーバーロードを使用し <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> ます。 このオーバーロードは、ドキュメントの完全パスと、 <xref:System.Uri> ドキュメントに添付するカスタマイズの配置マニフェストの場所を指定するを受け取ります。 この例では、 **WordDocument1.docx** という名前の Word 文書がデスクトップ上にあり、配置マニフェストが、デスクトップ上にある **Publish** という名前のフォルダーに配置されていることを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet3":::

4. プロジェクトをビルドし、カスタマイズをアタッチするコンピューターでアプリケーションを実行します。 コンピューターには、Visual Studio 2010 Tools for Office Runtime がインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [方法: マネージコード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Office ソリューションのアプリケーションマニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
