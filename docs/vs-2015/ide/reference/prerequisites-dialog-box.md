---
title: '[必須コンポーネント] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.Bootstrapper
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Prerequisites dialog box
ms.assetid: 53ac863c-77a0-409b-91e5-7a4bd8b8474e
caps.latest.revision: 79
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b8e5e004d2e337900d88f72d92bfd439103b87e0
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297844"
---
# <a name="prerequisites-dialog-box"></a>[必須コンポーネント] ダイアログ ボックス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このダイアログ ボックスでは、必須コンポーネントとしてインストールするコンポーネント、そのインストール方法、およびパッケージのインストール順序を指定します。

 このダイアログ ボックスを表示するには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー** が表示されたら、 **[発行]** タブをクリックします。 **[発行]** ページで、 **[必須コンポーネント]** をクリックします。 セットアップ プロジェクトで、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **[プロパティ ページ]** ダイアログ ボックスが表示されたら、 **[必須コンポーネント]** をクリックします。

## <a name="uielement-list"></a>UIElement の一覧

|要素|説明|
|-------------|-----------------|
|**必須コンポーネントをインストールするセットアップ プログラムを作成する**|必須コンポーネントをアプリケーションのセットアップ プログラム (Setup.exe) に含め、依存関係の順序に従って、それらのコンポーネントがアプリケーションより先にインストールされるようにします。 既定では、このチェック ボックスはオンになっています。 オフにした場合、Setup.exe は作成されません。|
|**インストールする必須コンポーネントを選択する**|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]、Crystal Reports などのコンポーネントをインストールするかどうかを指定します。<br /><br /> たとえば、 **[SQL Server 2005 Express Edition SP2]** の横のチェック ボックスをオンにした場合、セットアップ プログラムは、ターゲット コンピューターにこのコンポーネントがインストールされているかどうかを確認し、インストールされていなければインストールします。<br /><br /> 各必須パッケージの詳細については、後の「必須コンポーネント情報」を参照してください。|
|**再頒布可能コンポーネントについては、Microsoft Update を確認してください**|このリンクをクリックすると、[コンポーネントを再配布するための追加ブートストラップ パッケージ](https://go.microsoft.com/fwlink/?LinkId=208835)の Web サイトが表示されて、更新プログラムがあるかどうかを確認できます。|
|**必須コンポーネントをコンポーネントの開発元の Web サイトからダウンロードする**|販売元の Web サイトから必須コンポーネントをインストールするように指定します。 これは、既定の設定です。|
|**アプリケーションと同じ場所から必須コンポーネントをダウンロードする**|アプリケーションと同じ場所から必須コンポーネントをインストールするように指定します。 これにより、すべての必須パッケージが発行場所にコピーされます。 このオプションを使用するには、必須パッケージが開発用コンピューターに存在する必要があります。|
|**次の場所から必須コンポーネントをダウンロード**|選択した場所から必須コンポーネントをインストールするように指定します。 場所は、 **[参照]** ボタンを使って指定できます。|

## <a name="prerequisites-information"></a>必須コンポーネント情報
 **[必須コンポーネント]** ダイアログ ボックスに表示される必須コンポーネントは、後に示す一覧とは異なる場合があります。 **[必須コンポーネント] ダイアログ ボックス**にリストされている必須コンポーネントのパッケージは、ダイアログ ボックスを初めて開いたときに自動的に設定されます。 その後、プロジェクトのターゲット フレームワークを変更した場合は、新しいターゲット フレームワークに合わせて必須パッケージを手動で選択する必要があります。

|要素|説明|
|-------------|-----------------|
|**.NET Framework 3.5 SP1**|このパッケージは、次のコンポーネントをインストールします。<br /><br /> -  .NET Framework バージョン 2.0、3.0、および 3.5。<br />-   32 ビット (x86) オペレーティング システムおよび 64 ビット (x64) オペレーティング システム上の .NET Framework のすべてのバージョンに対するサポート。<br />-   パッケージと共にインストールされる各 .NET Framework バージョン用の Language Pack。<br />-   .NET Framework 2.0 および 3.0 用の Service Pack。<br /><br /> .NET Framework 3.0 は Windows Vista に含まれており、.NET Framework 3.5 は [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] に含まれています。 .NET Framework 3.5 は、32 ビット オペレーティング システム用にコンパイルされる、ターゲット フレームワークが **.NET Framework 3.5** に設定された、すべての Visual Basic プロジェクトおよび Visual C# プロジェクト、および、64 ビット オペレーティング システム用にコンパイルされる Visual Basic プロジェクトおよび Visual C# プロジェクトに必要です。 IA64 はサポートされません。Visual Basic プロジェクトおよび Visual C# プロジェクトは、既定ではどの CPU アーキテクチャにも対応するようにコンパイルされます。 詳細については、「[Visual Studio のマルチ ターゲットの概要](../../ide/visual-studio-multi-targeting-overview.md)」、「[Redistributing the .NET Framework](https://msdn.microsoft.com/a18d0456-fd89-493e-97f4-756505bfe287)」 (.NET Framework の再配布)、および「[64 ビット アプリケーションの配置のための必要条件](../../deployment/deploying-prerequisites-for-64-bit-applications.md)」を参照してください。<br /><br /> この項目は既定で選択されます。|
|**.NET Framework 3.5 SP1 Client Profile**|.NET Framework Client Profile は、クライアント アプリケーションを対象とする完全な .NET Framework 3.5 SP1 のサブセットです。 WPF (Windows Presentation Foundation)、Windows フォーム、WCF (Windows Communication Foundation)、および ClickOnce の機能の簡素化されたサブセットを提供します。 このサブセットを使用すると、.NET Framework Client Profile を対象とする WPF、Windows フォーム、WCF、およびコンソール アプリケーションの迅速な配置シナリオが可能になります。 詳細については、「[.NET Framework Client Profile](https://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1)」を参照してください。|
|**Microsoft .NET Framework 4 (x86 および x64)**|このパッケージは、.NET Framework 4 (x86 プラットフォームおよび x64 プラットフォーム用) をインストールします。<br /><br /> 詳細については、「[Visual Studio のマルチ ターゲットの概要](../../ide/visual-studio-multi-targeting-overview.md)」、「[Redistributing the .NET Framework](https://msdn.microsoft.com/a18d0456-fd89-493e-97f4-756505bfe287)」 (.NET Framework の再配布)、および「[64 ビット アプリケーションの配置のための必要条件](../../deployment/deploying-prerequisites-for-64-bit-applications.md)」を参照してください。<br /><br /> この項目は既定で選択されます。|
|**Microsoft .NET Framework 4 Client Profile (x86 および x64)**|.NET Framework 4 Client Profile は、クライアント アプリケーションを対象とする完全な .NET Framework 4 のサブセットです。 WPF (Windows Presentation Foundation)、Windows フォーム、WCF (Windows Communication Foundation)、および ClickOnce の機能の簡素化されたサブセットを提供します。 このサブセットを使用すると、.NET Framework 4 Client Profile を対象とする WPF、Windows フォーム、およびコンソール アプリケーションの迅速な配置シナリオが可能になります。 詳細については、「[.NET Framework Client Profile](https://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1)」を参照してください。|
|**Microsoft Office 2007 プライマリ相互運用機能アセンブリ**|Microsoft Office 2007 製品のプライマリ相互運用機能アセンブリをインストールします。 プライマリ相互運用機能アセンブリにより、Microsoft Office アプリケーションの COM ベースのオブジェクト モデルとマネージド コードとの相互運用を実行できるようになります。 詳細については、「[Office プライマリ相互運用機能アセンブリ](https://msdn.microsoft.com/library/aa29d12c-185f-4558-a7cd-3d85f924203d)」を参照してください。|
|**Microsoft Visual Basic PowerPacks Version 10.0**|Power Packs は、Visual Basic アプリケーションの開発を支援するアドイン、コントロール、コンポーネント、およびツールです。 このバージョンには、Windows フォームのコンテンツを印刷できるようにする[PrintForm](/previous-versions/bb882742(v=vs.140))コンポーネントと、Visual Basic 6.0 プリンターコードを変更せずに実行できるプリンター互換性ライブラリが含まれています。|
|**Microsoft Visual F# Runtime for .NET 2.0**|関数型プログラミング、および従来のオブジェクト指向プログラミングと命令型 (手続き型) プログラミングをサポートする、Visual F# ランタイム ライブラリ (x86 オペレーティング システムおよび x64 オペレーティング システム用) をインストールします。 アプリケーションまたはそのコンポーネントを Visual F# と .NET Framework 2.0、.NET Framework 3.0、または .NET Framework 3.5 で作成する場合、このパッケージをインストールする必要があります。<br /><br /> (詳細については、「[F# 言語リファレンス](https://msdn.microsoft.com/library/16b706f8-b5f2-4ff7-b2c1-64df33cd6adf)」を参照してください)。|
|**Microsoft Visual F# Runtime for .NET 4.0**|関数型プログラミング、および従来のオブジェクト指向プログラミングと命令型 (手続き型) プログラミングをサポートする、Visual F# ランタイム ライブラリ (x86 オペレーティング システムおよび x64 オペレーティング システム用) をインストールします。 アプリケーションまたはそのコンポーネントを Visual F# および .NET Framework 4 で作成する場合、このパッケージをインストールする必要があります。<br /><br /> (詳細については、「[F# 言語リファレンス](https://msdn.microsoft.com/library/16b706f8-b5f2-4ff7-b2c1-64df33cd6adf)」を参照してください)。|
|**Microsoft Visual Studio 2010 Report Viewer**|Windows フォームおよび ASP.NET アプリケーションに豊富なデータ レポート機能を追加するために使用できる、レポート ビューアー コントロールをインストールします。|
|**Microsoft Visual Studio 2010 for Office Runtime (x86 および x64)**|Visual Studio の Office 開発ツールには、Microsoft Office と連携するカスタマイズされたビジネス ソリューションを作成するための、統合された使いやすいツールが用意されています。 Office アプリケーションをユーザー インターフェイスとして使用するマネージド スマート クライアント ソリューションを作成できます。 開発者は、これらのツールを使って、配置と保守が容易な、安全なソリューションを作成できます。<br /><br /> 詳細については、「[方法: ClickOnce を使用して Office ソリューションを発行する](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)」を参照してください。|
|**SQL Server 2005 Express Edition SP2 (x86)**|Microsoft SQL Server 2005 Express Edition SP2 をインストールします。これは、[!INCLUDE[sqprsqext](../../includes/sqprsqext-md.md)] に基づくデータベース アプリケーションです。 SQL Server Express は、Microsoft SQL Server Desktop Engine (MSDE) の後継製品です。 SQL Server Express は無償で提供され、契約書に従って再配布することが可能であり、クライアント データベースとしても、基本サーバー データベースとしても機能します。 SQL Server Express は、以下の相違点を除いて SQL Server 2005 と同じです。<br /><br /> -   エンタープライズ機能をサポートしません。<br />-   1 台の CPU に制限されます。<br />-   バッファー プール用メモリが 1 ギガバイト (GB) に制限されます。<br />-   データベースの最大サイズは 4 GB です。|
|**SQL Server 2008 Express**|Microsoft SQL Server 2008 Express をインストールします。Microsoft SQL Server 2008 Express は、Microsoft SQL Server 2008 の無償のエディションであり、小規模な Web アプリケーション、サーバー アプリケーション、またはデスクトップ アプリケーションに最適なデータベースです。 Microsoft SQL Server 2008 Express は、開発環境および運用環境で無償で使用できます。 アプリケーションと共に SQL Server 2008 Express を配布するには、無償の登録が必要です。<br /><br /> ブートストラップの動作を次に示します。<br /><br /> -   コンピューターに SQL Server 2008 Express またはそれ以降が既にインストールされている場合は、SQL Server 2008 Express またはそれ以降のままです。<br />-   コンピューターに SQL Server 2008 Express またはそれ以降のいずれのバージョンもインストールされていない場合は、パッケージによって最新バージョンの SQL Server 2008 Express SP1 がインストールされます。<br /><br /> SQL Server 2008 Express の詳細については、[http://go.microsoft.com/fwlink/?LinkId=183586](https://go.microsoft.com/fwlink/?LinkId=183586) をご覧ください。|
|**Visual C++ 2010 ランタイム ライブラリ (IA64)**|Itanium アーキテクチャに対応する Visual C++ ランタイム ライブラリをインストールします。これらのライブラリは、Microsoft Windows オペレーティング システム用のプログラミング ルーチンを提供します。 これらのルーチンにより、C および C++ 言語では提供されない共通プログラミング タスクの多くを自動化できます。<br /><br /> 詳細については、「[C ランタイム ライブラリ リファレンス](https://msdn.microsoft.com/library/a503e11c-8dca-4846-84fb-025a826c32b8)」を参照してください。|
|**Visual C++ 2010 ランタイム ライブラリ (x64)**|x64 オペレーティング システムに対応する Visual C++ ランタイム ライブラリをインストールします。これらのライブラリは、Microsoft Windows オペレーティング システム用のプログラミング ルーチンを提供します。 これらのルーチンにより、C および C++ 言語では提供されない共通プログラミング タスクの多くを自動化できます。<br /><br /> 詳細については、「[C ランタイム ライブラリ リファレンス](https://msdn.microsoft.com/library/a503e11c-8dca-4846-84fb-025a826c32b8)」を参照してください。|
|**Visual C++ 2010 ランタイム ライブラリ (x86)**|x86 オペレーティング システムに対応する Visual C++ ランタイム ライブラリをインストールします。これらのライブラリは、Microsoft Windows オペレーティング システム用のプログラミング ルーチンを提供します。 これらのルーチンにより、C および C++ 言語では提供されない共通プログラミング タスクの多くを自動化できます。<br /><br /> 詳細については、「[C ランタイム ライブラリ リファレンス](https://msdn.microsoft.com/library/a503e11c-8dca-4846-84fb-025a826c32b8)」を参照してください。|
|**Windows インストーラー 3.1**|Microsoft Windows インストーラー再頒布パッケージ Version 3.1 をインストールし、Windows インストーラー セットアップ プロジェクトをインストールできるようにします。 このパッケージは、Windows Server 2003 SP1 以降にプレインストールされています。<br /><br /> この項目は既定で選択されます。|
|**Windows インストーラー 4.5**|Microsoft Windows インストーラー再頒布パッケージ Version 4.5 をインストールし、Windows インストーラー セットアップ プロジェクトをインストールできるようにします。|

## <a name="see-also"></a>関連項目
 [[発行] ページ (プロジェクトデザイナー](../../ide/reference/publish-page-project-designer.md) [アプリケーションの配置の前提条件](../../deployment/application-deployment-prerequisites.md)) .NET Framework を再[配布する](https://msdn.microsoft.com/a18d0456-fd89-493e-97f4-756505bfe287) [64 ビットアプリケーションの必須コンポーネントの配置](../../deployment/deploying-prerequisites-for-64-bit-applications.md) [Visual Studio のマルチターゲットの概要](../../ide/visual-studio-multi-targeting-overview.md)
