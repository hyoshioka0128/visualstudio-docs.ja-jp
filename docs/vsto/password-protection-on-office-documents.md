---
title: Office ドキュメントのパスワード保護
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- passwords [Office development in Visual Studio], document protections
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e3c9521389ce348a482f35ec95c9766edea49f5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62977901"
---
# <a name="password-protection-on-office-documents"></a>Office ドキュメントのパスワード保護
  Microsoft Office Word 文書にパスワードを設定したり、Excel ブックを Microsoft Office して、パスワードを知らない人がそれらを開けないようにすることができます。 このオプションは、 **Open On Password**と呼ばれます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 開いている **パスワード** が有効になっている既存のドキュメントとブックを使用して、ドキュメントレベルのプロジェクトを作成できます。 Visual Studio での動作は、 **パスワードが Open** が有効になっている Word および Excel ドキュメントでは異なります。

 開いている **パスワード**を有効にする方法の詳細については、Word または Excel のヘルプを参照してください。

## <a name="behavior-of-excel-and-word"></a>Excel と Word の動作
 **Open**が有効になっている場合、Visual Studio で excel ブックを開くたびに、パスワードを入力するように求められます。 ソリューションをビルドするときに、ドキュメントがビルド中に開かれるため、パスワードの入力を求められます。

 **Open**が有効になっているときに、Visual Studio で word 文書を初めて開くと、パスワードを入力するようにというメッセージが表示されます。 パスワードが正常に入力されると、 **Open のパスワード** はドキュメントから削除され、ドキュメントを開くとパスワードは不要になります。 ソリューション内のドキュメントを開く前にパスワードが要求されるようにするには、最終的なビルド後、ソリューションを配置する前に、 **パスワード** を有効にする必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [ドキュメントレベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Information rights management とマネージコード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [方法: アクセス許可が制限されたドキュメントの背後でコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
