---
title: アクセス許可が制限されたドキュメントの背後でのコードの実行を許可する
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- IRM [Office development in Visual Studio]
- code [Office development in Visual Studio], running behind restricted documents
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 14c468a806160fd31c84b164a4b995f904e71fc6
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "92298492"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>方法: アクセス許可が制限されたドキュメントの背後でコードの実行を許可する
  Microsoft Office の Information Rights Management (IRM) 機能を使用して、ドキュメントまたはブックへのアクセス許可を制限できます。 既定では、制限された Microsoft Office Word 文書または Microsoft Office Excel ブックの背後にあるコードは実行できません。 マネージコード拡張機能がオブジェクトモデルにアクセスできるように、既定値を変更することができます。これにより、ソリューションが機能します。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 アクセス許可の設定を変更できるようにするには、ドキュメントまたはブックの作成者であるか、フルコントロールアクセス権を持っている必要があります。

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>アクセス許可が制限されたドキュメントの背後でコードを実行できるようにするには

1. Word または Excel で文書またはブックを開きます。

2. [ **ファイル** ] タブをクリックし、[ **準備**] をポイントして、[ **アクセス許可の制限**] をポイントし、[ **制限付きアクセス**] をクリックします。

   > [!NOTE]
   > 初回使用時には、Windows Rights Management クライアントをインストールするように求められます。 クライアントをインストールした後、手順を繰り返すことが必要になる場合があります。

3. [ **アクセス許可** ] ダイアログボックスで、[ **このドキュメントに対するアクセス許可を制限する**] を選択し、[ **その他のオプション**] をクリックします。

4. [ **ユーザーの追加のアクセス許可**] で、[ **プログラムによるコンテンツへのアクセス**] を選択します。

   Word または Excel では、オブジェクトモデルへのプログラムによるアクセスが許可されます。

## <a name="see-also"></a>関連項目
- [Information rights management とマネージコード拡張機能の概要](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [ドキュメントレベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)
- [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
