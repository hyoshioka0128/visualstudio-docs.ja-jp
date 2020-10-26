---
title: ドキュメントレベルのソリューションにおけるドキュメントの保護
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio], restricted permissions
- documents [Office development in Visual Studio], restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6c5f019907495c3cad3fddef501455aedf345bb2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "71253807"
---
# <a name="document-protection-in-document-level-solutions"></a>ドキュメントレベルのソリューションにおけるドキュメントの保護
  ドキュメントレベルのプロジェクトで Microsoft Office Word および Excel Microsoft Office の保護機能を使用できます。 これらの機能は、承認されていないユーザーがドキュメントの保護された部分を変更できないようにします。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Excel を使用すると、デザイナーでブックを開いているときに保護をオンまたはオフにできます。 Word を使用すると、デザイナーの外部でのみ保護を有効にすることができます。 実行時に、Word と Excel の両方でプログラムによって保護を有効または無効にすることができます。

 デザイナーで開かれているドキュメントでドキュメント保護が有効になっていると、すべてのコントロールが **ツールボックス** から削除されるか、使用できなくなります。また、[ **データソース** ] ウィンドウからドキュメントに何もドラッグすることはできません。

## <a name="serverdocument-and-protected-documents"></a>ServerDocument と保護されたドキュメント
 ドキュメントが保護されている場合、ドキュメントの外部からデータキャッシュにアクセスすることはできません。 クラスを使用して、 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 保護されたドキュメントにキャッシュされているデータを取得または操作したり、クラスの他のメソッドを使用したりすることはできません <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 。

## <a name="word-document-protection-in-the-designer"></a>デザイナーでの Word 文書の保護
 Visual Studio で Word 文書またはテンプレートを開いているときに保護を追加した場合、デザイナーでの保護の強制を開始することはできません。 ドキュメントは Visual Studio で開かれている間はデザインモードであり、保護の適用を開始する前に実行モードになっている必要があります。

 ただし、保護が有効になっている既存の Word 文書を使用するプロジェクトを作成した場合、デザイナーで開かれている間、ドキュメントは保護されます。 ドキュメントの保護された部分を編集することはできませんが、コードエディターでコードを記述してドキュメントを自動化することはできます。 また、Visual Studio でドキュメントを開いているときに保護が有効になっている場合は、プロジェクトをビルドできません。

 ドキュメントを編集してプロジェクトをビルドできるように、デザイナーでドキュメントが開いている間は保護をオフにすることができます。 デバッグ中にデザイナーでコピーの保護を無効にすることはできません。デバッグ中に開かれるドキュメントは、デザイナーで開いているものとは別のコピーです (出力コピーは、Visual Basic の *\bin* ディレクトリと C# の場合は *\bin\debug* ディレクトリに格納されます)。

 デザイナーで開くドキュメントのコピーを保護するには、Visual Studio でプロジェクトを終了し、プロジェクトディレクトリにあるドキュメントのコピーを開いて、保護を有効にします。

## <a name="enforce-word-document-protection-on-build"></a>ビルド時に Word 文書保護を適用する
 Visual Studio は、ビルド処理中に Word 文書とテンプレートの保護の適用を開始します。これにより、ドキュメントがデバッグ用に開いたときに保護が有効になります。 ドキュメントは空のパスワードで保護されています。

 ビルド中に保護が有効になるため、例外を発生させる可能性のあるコードがドキュメントイベントに存在する場合 <xref:Microsoft.Office.Tools.Word.Document.Startup> や、アプリケーションの動作を変更する場合に、このコードを正しくデバッグできます。 ドキュメントを開いた後で保護を有効にした場合、初期化コードをデバッグまたはテストすることはできません。

## <a name="setting-the-password"></a>パスワードの設定
 Visual Studio では自動的に保護が有効になりますが、既定ではパスワードは提供されません。 ドキュメント保護にパスワードを設定する場合は、ソリューションを配置する前に追加する必要があります。 パスワードを追加すると、承認されたユーザーがドキュメントから保護を削除できるようになります。パスワードがないと、保護を簡単に削除できません。 パスワードの設定の詳細については、特定の Office アプリケーションのヘルプを参照してください。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書および文書の一部を保護する](../vsto/how-to-programmatically-protect-documents-and-parts-of-documents.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [Information rights management とマネージコード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [方法: アクセス許可が制限されたドキュメントの背後でコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
