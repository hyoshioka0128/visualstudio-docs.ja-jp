---
title: ドキュメントへの信頼の付与
description: ドキュメントレベルのプロジェクトで、証明書を使用してマニフェストに署名したり、信頼プロンプトをクリックしたりするなど、アプリケーションレベルのプロジェクトと同じセキュリティ要件を持つ方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], trust
- inclusion lists [Office development in Visual Studio], about inclusion lists
- trust [Office development in Visual Studio], 2007 Office system
- granting trust [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9d91a86f8596e0ed7a04ae68099c7c9ab6099a40
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847742"
---
# <a name="grant-trust-to-documents"></a>ドキュメントへの信頼の付与
  ドキュメント レベルのプロジェクトでは、証明書を使用したマニフェストへの署名や、信頼プロンプトのクリックなど、アプリケーション レベルのプロジェクトと同じセキュリティ要件が適用されます。 また、ドキュメントまたはブックは、信頼できる場所として指定されたディレクトリに置く必要があります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="trusted-locations"></a>信頼できる場所
 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]と Office 2010 のアプリケーションには、信頼できる場所などのセキュリティとプライバシーの設定をユーザーが構成できる信頼センターがあります。 Officeソリューションでは、ローカル コンピューターは信頼できる場所と見なされます。 ただし、ディレクトリの中には、リスクが高めであるために信頼できないものもあります (システム、各ユーザー、Internet Explorer 用の一時フォルダーなど)。

 セキュリティセンターの詳細については、「 [Office 2010 のセキュリティとポリシー」と「設定](/previous-versions/office/office-2010/cc178946(v=office.14))」を参照してください。 信頼されたフォルダーを作成、管理、削除、および構成する方法の詳細については、「 [2007 Office システムで信頼できる場所と信頼](/previous-versions/office/office-2007-resource-kit/cc178948(v=office.12)) された発行元の設定を構成する」および「 [ファイルの信頼できる場所を作成、削除、または変更](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)する」を参照してください。

## <a name="security-considerations-for-office-solutions"></a>Office ソリューションのセキュリティに関する考慮事項
 どのフォルダーを信頼できる場所に追加するかを検討するときには、以下のセキュリティ上の問題に留意する必要があります。

- ローカル フォルダーは安全性が高いと見なされ、暗黙的に信頼されます。  ファイル共有などのリモートの場所は、信頼できる場所として指定する必要があります。

- 信頼できる場所にディレクトリを追加すると、Office ソリューションだけでなく VBA コードおよび ActiveX コードにも完全な信頼が付与されます。 このため、ルートディレクトリと *[マイドキュメント* ] フォルダーは信頼済みとして指定しないでください。

- ドキュメント自体は信頼できる場所を使用することによって信頼されますが、カスタマイズを信頼するためには追加のアクセス許可が必要です。 証明書を使用したマニフェストへの署名、信頼プロンプトのクリック、または *Program Files* ディレクトリへの Office ソリューションのインストールを使用して、カスタマイズに対する完全な信頼を付与することができます。

- ドキュメント レベルのソリューションのドキュメントまたはブックは、アセンブリと同じディレクトリ、または別のディレクトリに保存できます。 たとえば、ドキュメントを SharePoint サーバー上に置き、アセンブリをネットワーク ファイル共有に置くことも可能です。 詳細については、「 [方法: ClickOnce を使用してドキュメントレベルの Office ソリューションを SharePoint サーバーに発行](/previous-versions/bb608595(v=vs.110))する」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)
- [Office ソリューションのセキュリティに関するトラブルシューティング](../vsto/troubleshooting-office-solution-security.md)
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)