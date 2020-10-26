---
title: Visual Studio 内での Office 機能の使用
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], document protection
- Office applications [Office development in Visual Studio]
- Office functionality inside Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c47ed9639a33ecdea3451c63b729d959f6855e5d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62982345"
---
# <a name="use-office-functionality-inside-of-visual-studio"></a>Visual Studio 内での Office 機能の使用
  ドキュメントレベルのプロジェクトを作成すると、ドキュメントと関連付けられているアプリケーションが Visual Studio 内でホストされるため、ドキュメントを直接デザインして操作できます。 Visual Studio で Microsoft Office アプリケーションを開いている場合は、通常、想定どおりに動作します。 ただし、アプリケーションの機能の中には、異なるものやアクセスできないものがあります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="document-protection"></a>ドキュメントの保護
 Microsoft Office Word および Microsoft Office Excel では、プロジェクトで使用できるドキュメント保護機能が用意されています。 ただし、ドキュメントが Visual Studio で開かれている間にドキュメント保護が有効になっている場合は、デザインを変更できないことがあります。 詳細については、「ドキュメント [レベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)」を参照してください。

## <a name="information-rights-management"></a>Information rights management
 Information Rights Management (IRM) は Microsoft Office Word および Microsoft Office Excel で使用できます。 IRM は、承認されていないユーザーが機密情報を表示または変更できないようにするのに役立ちます。 ただし、IRM によってコードが実行されないようにすることもできます。 詳細については、「 [information rights management」と「マネージコード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)」を参照してください。

## <a name="password-protection"></a>パスワード保護
 Word 文書や Microsoft Office Excel ブックを Microsoft Office、パスワードを知らない人が開けないように設定できます。 パスワード保護は Word と Excel では異なる方法で処理されるため、開発プロセスに影響を与える可能性があります。 詳細については、「 [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [ドキュメントレベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Information rights management とマネージコード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [方法: コードを実行せずに Office ソリューションを開く](../vsto/how-to-open-office-solutions-without-running-code.md)
