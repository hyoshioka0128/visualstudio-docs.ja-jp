---
title: シェル (分離または統合) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell
- Visual Studio, Shell
- Shell [Visual Studio]
- Visual Studio shell, shell-based applications
- Shell [Visual Studio], shell-based applications
ms.assetid: c64a9bf0-9bf8-45c3-8fa2-306fa6cab66a
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aa346ebfe321e4672ea3fa71a4dcc872ebf22cda
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75850231"
---
# <a name="shell-isolated-or-integrated"></a>シェル (分離または統合)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

独自の Visual Studio ベースのアプリケーションは、統合モードまたは分離モードで作成できます。 統合モードでは、アプリケーションに加えて Visual Studio の多くの機能を使用できます。 分離モードでは、独自の拡張機能と共に配布する Visual Studio の機能のサブセットを選択します。  
  
## <a name="integrated-mode"></a>統合モード  
 統合モードでは、ユーザーは、カスタムツールと共に、標準の Visual Studio 機能を使用できます。 統合シェルは、主にプログラミング言語とソフトウェア開発ツールをホストするためのものです。  
  
 統合シェル上に構築されたカスタムツールは、同じコンピューターにインストールされている Visual Studio の他のエディションと自動的にマージされます。 Visual Studio がまだインストールされていない場合は、Visual Studio 統合シェルの再頒布可能バージョンを提供できます。  
  
 Visual Studio 統合シェルの再頒布可能バージョンには、プログラミング言語と、それぞれのプロジェクトシステムをサポートする機能は含まれていません。  
  
> [!NOTE]
> Visual Studio shell 統合モードは、Express エディションを除く、Visual Studio のすべてのエディションと共にインストールできます。  
  
 詳細については、「 [Visual Studio Shell (Integrated)](../extensibility/visual-studio-shell-integrated.md)」を参照してください。  
  
## <a name="isolated-mode"></a>分離モード  
 分離モードでは、Visual Studio の他のバージョンとサイドバイサイドで実行するカスタムツールを作成できます。 これは主に、visual studio のすべての標準機能に依存せずに Visual Studio サービスにアクセスできるツールを対象としています。 Visual Studio の分離シェルでビルドされたアプリケーションの外観をカスタマイズできます。 アプリケーションと一緒に表示しない機能やメニューコマンドグループは、簡単に無効にすることができます。  
  
 詳細については、「 [Visual Studio の分離シェル](../extensibility/visual-studio-isolated-shell.md)」を参照してください。  
  
## <a name="distributing-your-integrated-or-isolated-shell-application"></a>統合または分離されたシェルアプリケーションの配布  
 統合または分離されたシェルアプリケーションを配布するには、アプリケーション、特別な統合または分離されたシェル再頒布可能パッケージ、およびインストールプログラムを含める必要があります。 配布とインストールの詳細については、「 [分離シェルアプリケーションの配布](../extensibility/distributing-isolated-shell-applications.md)」を参照してください。  
  
> [!IMPORTANT]
> Visual Studio 統合シェルと分離シェルの [使用許諾契約書 (EULA)](https://www.visualstudio.com/support/legal/mt171552) には、データコレクション (セクション 3) のセクションが含まれてい**ます。データ**)。  ここでは、アプリケーションに組み込む統合シェルソフトウェアまたは分離シェルソフトウェアのユーザーから Microsoft によって収集される可能性のある顧客の使用状況データについて説明します。 詳細については、「 [Microsoft Visual Studio 製品ファミリのプライバシー](https://www.visualstudio.com/dn948229)に関する声明」を参照してください。  
> 
> アプリケーションを使用して顧客から個別の使用状況データを収集する場合は、収集対象のアプリケーションのユーザーに適切な通知を提供する必要があります。  Visual Studio ソフトウェア開発キットのライセンスに従って、アプリケーションの一部として分離または統合されたシェルソフトウェアを配布する場合は、次のいずれかを含める必要があります。  
> 
> - アプリケーションライセンスの一部として使用許諾契約書  
> - お客様が、Visual Studio の統合シェルまたは分離シェルを、少なくともシェルソフトウェアの Microsoft エンドユーザーライセンス条項に従って保護するという条件に同意することを必要とする独自の EULA。  
  
## <a name="additional-resources"></a>その他のリソース  
 再頒布可能パッケージの詳細については、「 [Visual Studio 拡張機能のダウンロード](https://msdn.microsoft.com/vstudio/bb984878.aspx) 」 Web サイトを参照してください。  
  
## <a name="see-also"></a>参照  
 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
