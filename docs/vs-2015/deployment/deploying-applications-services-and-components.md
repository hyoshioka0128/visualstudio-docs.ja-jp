---
title: アプリケーション、サービス、およびコンポーネントの配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- .NET applications, deploying
- components [Visual Studio], deploying
- installers
- publishing
- deploying applications [Visual Studio]
- deploying applications [Visual Studio], about deploying applications
- components [.NET Framework], deploying
ms.assetid: 63fcdd5b-2e54-4210-9038-65bc23167725
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 42e3a4afec71b90a087ac927f5cbbbc0b181fadd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75917551"
---
# <a name="deploying-applications-services-and-components"></a>アプリケーション、サービス、およびコンポーネントの配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーション、サービス、またはコンポーネントを配置すると、他のコンピューターのデバイス、サーバー、またはクラウドに対してインストールするために、それらを配布することになります。 必要な配置の種類に合わせて、Visual Studio で適切な手法を選択します。  
  
 次の表に、さまざまな配置シナリオに関する説明と、それらのシナリオを正常に完了する詳細な方法へのリンクを示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|配置シナリオ|関連する参照先|  
|-------------------------|------------------------|  
|**クラウドに発行する:** Visual Studio を使用してアプリケーション、サービス、およびデータをどこからでも使用できるようにし、Microsoft Azure に配置できます。|[アプリケーションを Microsoft Azure に発行する](/visualstudio/deployment/quickstart-deploy-to-azure)|  
|**Windows ストアアプリを発行する:** Windows ストアから世界中の顧客にアプリを簡単に作成、送信、販売できます。|[Windows ストア アプリのパッケージ、展開、およびクエリ](https://msdn.microsoft.com/library/hh446593\(v=vs.85\).aspx)|  
|**Windows Phone アプリを発行する:** Windows Phone デベロッパーセンターで認定を取得するために、既存のアプリに新しいアプリまたは更新プログラムを送信することができます。|[Windows Phone アプリを発行する](https://developer.microsoft.com/)|  
|**ASP.NET アプリケーションまたはサービスをデプロイします。** ASP.NET アプリケーションとサービスは、さまざまな方法でデプロイできます。|[ASP.NET web アプリケーションとサービスのデプロイ](/aspnet/mvc/overview/deployment/)|  
|**LightSwitch アプリケーションまたはサービスをデプロイします。** LightSwitch を使用してアプリケーションと OData サービスを作成した後、それらのサービスを web サーバーまたは Microsoft Azure に配置できます。|[LightSwitch アプリケーションの配置](https://msdn.microsoft.com/library/4818d933-295c-4ecc-9148-7ad9ca28dcdb)|  
|**SharePoint 用アプリの発行:** SharePoint 用アプリは、Office ストアまたは社内組織のアプリカタログに発行できます。|[Visual Studio を使用して SharePoint 用アプリを発行する](https://msdn.microsoft.com/library/office/jj220044\(v=office.15\).aspx)|  
|**Office 用アプリを発行する:** Office ストアまたは社内組織のアプリカタログに Office 用アプリを発行できます。|[Office 用アプリの発行](https://msdn.microsoft.com/library/office/fp123515.aspx)|  
|**WCF サービスをデプロイします。** 他のアプリケーションでは、web サーバーに配置する WCF RIA サービスを使用できます。|[WCF RIA Services ソリューションの配置](https://msdn.microsoft.com/library/ff426912\(v=vs.91\).aspx)|  
|**OData サービスをデプロイします。** 他のアプリケーションでは、web サーバーに配置する OData サービスを使用できます。|[OData サービスをデプロイする](https://msdn.microsoft.com/library/hh973447.aspx)|  
|**デスクトップアプリケーションを展開します。** ClickOnce 配置を使用すると、デスクトップアプリケーションを web サーバーまたはネットワークファイル共有に発行できます。 その後、ユーザーはシングル クリックでアプリケーションをインストールできます。|[ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)|  
|**セットアッププログラムを作成します。** InstallShield の制限付きエディション (無料) を使用して、セットアッププログラムを作成できます。|[InstallShield Limited Edition](../deployment/installshield-limited-edition.md)|  
|**既存のセットアッププログラムを保持する:** Visual Studio インストーラー Projects 拡張機能をインストールして、以前のバージョンの Visual Studio で作成されたセットアッププログラムを使用し続けます。|[Visual Studio インストーラープロジェクトの拡張機能](https://devblogs.microsoft.com/visualstudio/visual-studio-installer-projects-extension/)<br /><br /> インストーラープロジェクトのドキュメントについては、「 [Visual Studio インストーラー展開](https://msdn.microsoft.com/library/2kt85ked\(v=vs.100\).aspx)」を参照してください。|  
|**Visual C++ アプリケーションを展開します。** 集中配置、ローカル配置、または静的リンクを使用して、アプリケーションを使用して Visual C++ ランタイムを配置できます。|[ネイティブ デスクトップ アプリケーションの配置 (Visual C++)](/cpp/windows/deploying-native-desktop-applications-visual-cpp)|  
|**テスト用のアプリケーションを展開します。** アプリケーションを仮想環境にデプロイすることにより、より高度な開発とテストを実現できます。|[ラボ環境でのテスト](https://msdn.microsoft.com/library/14ba54c8-a158-4a6e-b00a-b00ae960feb8)|  
|**インストールの前提条件:** ブートストラップと呼ばれる汎用インストーラーを構成することにより、デスクトップアプリケーションの必須コンポーネントをインストールできます。|[アプリケーションの展開の前提条件](../deployment/application-deployment-prerequisites.md)|
