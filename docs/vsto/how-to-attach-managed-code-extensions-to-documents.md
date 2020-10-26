---
title: '方法: マネージコード拡張機能をドキュメントにアタッチする'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f44b153ac7d55704ba649a7dc09860518a5e76b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547525"
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

     [!code-csharp[Trin_VstcoreDeployment#4](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#4)]
     [!code-vb[Trin_VstcoreDeployment#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#4)]

3. 静的メソッドを呼び出し <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> ます。

     次のコード例では、オーバーロードを使用し <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> ます。 このオーバーロードは、ドキュメントの完全パスと、 <xref:System.Uri> ドキュメントに添付するカスタマイズの配置マニフェストの場所を指定するを受け取ります。 この例では、 **WordDocument1.docx** という名前の Word 文書がデスクトップ上にあり、配置マニフェストが、デスクトップ上にある **Publish** という名前のフォルダーに配置されていることを前提としています。

     [!code-csharp[Trin_VstcoreDeployment#3](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#3)]
     [!code-vb[Trin_VstcoreDeployment#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#3)]

4. プロジェクトをビルドし、カスタマイズをアタッチするコンピューターでアプリケーションを実行します。 コンピューターには、Visual Studio 2010 Tools for Office Runtime がインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [方法: マネージコード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Office ソリューションのアプリケーションマニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
