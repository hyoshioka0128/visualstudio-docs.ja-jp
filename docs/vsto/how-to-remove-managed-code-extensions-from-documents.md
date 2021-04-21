---
title: '方法: マネージコード拡張をドキュメントから削除する'
description: Microsoft Word または Excel のドキュメントレベルのカスタマイズの一部であるドキュメントまたはブックから、プログラムによってカスタマイズアセンブリを削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 129b1bda44abf7283efe1996f1898491025ee9d9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825447"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>方法: マネージコード拡張をドキュメントから削除する
  Microsoft Office Word または Microsoft Office Excel のドキュメントレベルのカスタマイズの一部であるドキュメントまたはブックから、プログラムによってカスタマイズアセンブリを削除できます。 その後、ユーザーはドキュメントを開いて内容を表示できますが、ドキュメントに追加したカスタムユーザーインターフェイス (UI) は表示されず、コードは実行されません。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 によって提供されるメソッドのいずれかを使用して、カスタマイズアセンブリを削除でき `RemoveCustomization` [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ます。 どの方法を使用するかは、実行時にカスタマイズを削除するか (Word 文書または Excel ブックが開いているときにカスタマイズでコードを実行するか)、または閉じたドキュメントまたは Microsoft Office がインストールされていないサーバー上のドキュメントからカスタマイズを削除するかどうかによって異なります。

## <a name="to-remove-the-customization-assembly-at-run-time"></a>実行時にカスタマイズアセンブリを削除するには

1. カスタマイズコードで、 <xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> メソッド (Word の場合) または <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> メソッド (Excel の場合) を呼び出します。 このメソッドは、カスタマイズが不要になった後にのみ呼び出す必要があります。

     コード内でこのメソッドを呼び出す場所は、カスタマイズの使用方法によって異なります。 たとえば、ユーザーがドキュメントそのものだけを必要とする他のクライアント (カスタマイズではない) にドキュメントを送信する準備ができてからカスタマイズの機能を使用する場合は、顧客がクリックしたときにを呼び出す UI を提供でき `RemoveCustomization` ます。 また、カスタマイズによってドキュメントが最初に開かれたときにデータを入力する場合でも、ユーザーが直接アクセスする他の機能がカスタマイズによって提供されない場合は、カスタマイズによってドキュメントの初期化が完了したらすぐに RemoveCustomization を呼び出すことができます。

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>閉じられたドキュメントまたはサーバー上のドキュメントからカスタマイズアセンブリを削除するには

1. コンソールアプリケーションや Windows フォームプロジェクトなどの Microsoft Office を必要としないプロジェクトでは、 *Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* アセンブリへの参照を追加します。

2. 次の **Imports** ステートメントまたは **using** ステートメントをコードファイルの先頭に追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet1":::

3. クラスの静的メソッドを呼び出し、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> パラメーターのソリューションドキュメントパスを指定します。

     次のコード例では、デスクトップ上の *WordDocument1.docx* という名前のドキュメントからカスタマイズを削除することを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet2":::

4. プロジェクトをビルドし、カスタマイズを削除するコンピューターでアプリケーションを実行します。 コンピューターには、Visual Studio 2010 Tools for Office runtime がインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [方法: マネージコード拡張機能をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
