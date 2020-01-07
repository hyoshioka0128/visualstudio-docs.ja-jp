---
title: '方法: Office ソリューションを開発するようにコンピューターを構成する'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- prerequisites [Office development in Visual Studio]
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb29dc4151bc457eb60ce836986817bc1b0137c9
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985960"
---
# <a name="how-to-configure-a-computer-to-develop-office-solutions"></a>方法: Office ソリューションを開発するようにコンピューターを構成する
  Visual Studio の Microsoft Office Developer Tools を使用できるように開発コンピューターを構成するには、次のトピックの手順を実行します。 これらの手順を実行するには、開発コンピューターの管理特権を保持している必要があります。

### <a name="to-configure-the-development-computer"></a>開発コンピューターを構成するには

1. Office Developer Tools が含まれているバージョンの Visual Studio をインストールします。 Office 開発者ツールは既定でインストールされます。 インストールする機能を選択して Visual Studio のインストールをカスタマイズする場合は、セットアップ時に**Microsoft Office 開発者ツール**が選択されていることを確認してください。 Office developer tools を含む Visual Studio のバージョンの詳細については、「 [office ソリューションを開発するためのコンピューターの構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

2. Visual Studio の Office Developer Tools によってサポートされているバージョンの Office をインストールします。 詳細については、「 [Office ソリューションを開発するためのコンピューターの構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

     インストールするバージョンの Office の PIA もインストールされることを確認してください。 PIA は、既定では Office と共にインストールされます。 Office セットアップを変更する場合は、対象とするアプリケーションに対して **[.Net プログラミングサポート]** 機能が選択されていることを確認してください。

3. 英語版の Visual Studio を使用していて、Windows に英語以外の設定を使用している場合は、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 言語パックをインストールして、Windows と同じ言語のメッセージを [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 表示することができます。 英語版以外の Visual Studio では、この言語パックが自動的にインストールされます。 言語パックは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=54246)から入手できます。

## <a name="see-also"></a>関連項目

- [Visual Studio &#40;での Office 開発の概要&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [方法: Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [方法: Office プライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)
