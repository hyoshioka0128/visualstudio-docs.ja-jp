---
title: Office ソリューションの共同開発
description: 複数の開発者が、他の Visual Studio プロジェクトで共同作業するのと同じ方法で Office プロジェクトを操作できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], collaborative development
- Office development in Visual Studio, collaboration
- source control [Office development in Visual Studio]
- collaborative development [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d30f28b3e97469bc9e0bf921438960206b4f89c0
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845805"
---
# <a name="collaborative-development-of-office-solutions"></a>Office ソリューションの共同開発
  複数の開発者は、他の Visual Studio プロジェクトで共同作業するのと同じ方法で Office プロジェクトを操作できます。 Office が異なる場所にインストールされている場合でも、Visual Studio は各コンピューターに Microsoft Office のインストールを正しく検索します。 ただし、注意すべき重要な考慮事項がいくつかあります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="debug-properties-are-not-shared"></a>デバッグプロパティは共有されていません
 デバッグ プロパティは、ソース管理で複数のユーザー間では共有されません。 Visual Basic および Visual C# プロジェクトは、ユーザー固有のファイル (*projectname*. .vbproj. ユーザーまたは *projectname*. .csproj) にデバッグプロパティを格納します。このファイルはソース管理されていません。 複数のユーザーがデバッグを実行する場合は、各自が手動でデバッグ プロパティを入力する必要があります。

 プロジェクトがソース管理ではなくネットワーク共有に置かれている場合は、コラボレーション開発者がソリューションを開いてアセンブリをテストできるようにするために、いくつかの追加手順を実行する必要があります。

## <a name="source-control-requires-checking-out-all-files"></a>ソース管理では、すべてのファイルをチェックアウトする必要があります
 プロジェクトにソース管理を使用する場合は、コードファイルを変更するたびに、既定で非表示になっているファイルでも、 **ソリューションエクスプローラー** のコードファイル ( *ThisDocument*、 *ThisWorkbook*、または *ThisAddIn* コードファイルなど) の下にあるすべてのファイルをチェックアウトする必要があります。 最上位レベルのコードファイルのみをチェックアウトすると、変更が失われる可能性があります。

 変更が完了したら、すべてのファイルを再度確認します。 プロジェクト内の非表示コードファイルの詳細については、「 [Visual Studio 環境の Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="security-for-informal-collaboration-on-a-network"></a>ネットワークで非公式に共同作業を行うためのセキュリティ
 ネットワークの場所にあるすべてのドキュメントレベルのソリューション (Servername Sharename など) については、使用している \\ \\ *Servername* \\ *Sharename* Microsoft Office アプリケーションの信頼されたフォルダーの一覧に、完全修飾された場所を追加する必要があります。 メインフォルダーの下にサブディレクトリを含めるか、またはデバッグフォルダーとビルドフォルダーを信頼されたフォルダーの一覧に追加するオプションを選択します。 これを行う方法の詳細については、「 [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

 ビルド時に自動的に生成される一時的な証明書は、パスワードによって保護されません。 証明書には、開発者のログイン名とその他の個人情報が含まれています。 一時的な証明書によって署名されたカスタマイズを展開する場合、他のユーザーがこの情報にアクセスできる可能性があります。

## <a name="see-also"></a>関連項目
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
