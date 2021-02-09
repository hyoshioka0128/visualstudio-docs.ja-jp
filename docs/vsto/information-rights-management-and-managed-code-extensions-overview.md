---
title: Information rights management & マネージコード拡張機能
description: IRM (Information Rights Management) について説明します。これは、承認されていないユーザーが機密情報を表示または変更できないようにするための機能です。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- IRM [Office development in Visual Studio]
- documents [Office development in Visual Studio], restricted permissions
- rights management [Office development in Visual Studio]
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8fc6a37a327c26ec46777575c3976c227e2d1de9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881491"
---
# <a name="information-rights-management-and-managed-code-extensions-overview"></a>Information rights management とマネージコード拡張機能の概要
  Microsoft Office Word および Microsoft Office Excel は情報 Rights Management (IRM) を提供します。これは、承認されていないユーザーが機密情報を表示または変更できないようにするための機能です。 情報 Rights Management のしくみの詳細については、特定の Office アプリケーションのヘルプを参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="run-code-behind-documents-with-restricted-permissions"></a>アクセス許可が制限されたドキュメントの分離コードを実行する
 IRM を使用するドキュメントまたはブックがソリューションに含まれている場合、既定では、Word と Excel ではコードの実行が許可されません。 ドキュメントの作成者である場合、またはフルコントロールアクセス権を持っている場合は、ソリューションが機能するように既定値を変更できます。 詳細については、「 [方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)」を参照してください。

 IRM <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> を使用すると、ドキュメントにキャッシュされているデータを取得または操作できなくなります。

## <a name="end-users-to-restrict-permissions-to-documents-that-use-managed-code-extensions"></a>エンドユーザーが、マネージコード拡張機能を使用するドキュメントに対するアクセス許可を制限する
 ソリューション内のドキュメントまたはブックに対するフルコントロールアクセス権を持つユーザーは、IRM を使用してアクセス許可を制限できます。 たとえば、会計部門のエンドユーザーが、データベースのデータをワークシートに自動的に入力するソリューションを使用している場合、そのユーザーは自分の部署のユーザーにのみ変更アクセスを許可し、他のユーザーには読み取りアクセスを許可することができます。 ユーザーが制限されたアクセス許可を追加すると、既定では、ワークシートの背後にあるコードを実行できず、ワークシートにデータが設定されません。

 この問題を解決するには、ドキュメントまたはブックに対するフルコントロールアクセス権を持つユーザーが、オブジェクトモデルにプログラムでアクセスできるように、既定のアクセス許可設定を変更する必要があります。 詳細については、「 [方法: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメントレベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
