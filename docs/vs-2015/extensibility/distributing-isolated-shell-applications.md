---
title: 分離シェルアプリケーションの配布 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c503a985-d67a-4ef8-9123-7744a78f2f17
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bf0d8a4cab8d30a56e84d1a6869c2c842b982aea
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204676"
---
# <a name="distributing-isolated-shell-applications"></a>分離シェル アプリケーションの配布
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分離シェルアプリケーションを作成するには、Visual Studio と Visual Studio SDK をインストールする必要があります。 他のユーザーまたは顧客のコンピューターにアプリケーションを配布するには、分離シェル用の特別な再頒布可能パッケージを含める必要があります。  
  
## <a name="prerequisites-for-distributing-isolated-shell-applications"></a>分離シェルアプリケーションを配布するための前提条件  
  
|名前|説明|  
|----------|-----------------|  
|Visual Studio SDK|の拡張機能を開発およびテストするために必要な SDK [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 また、SDK を使用して、Visual Studio 分離シェルのインスタンスを作成することもできます。<br /><br /> SDK の前提条件として Visual Studio が使用されています。|  
|Microsoft Visual Studio 分離シェル再頒布可能パッケージ|Visual Studio の分離シェルでツール環境を構築するときに、セットアッププログラムに含める再頒布可能パッケージ。 分離シェル再頒布可能パッケージには、.NET Framework 4.5 が含まれています。|  
  
## <a name="creating-an-installation-program-for-the-application"></a>アプリケーションのインストールプログラムを作成する  
 統合または分離されたシェルアプリケーション用の特別なインストールプログラムを作成する必要があります。 詳細については、「 [分離シェルアプリケーションのインストール](../extensibility/installing-an-isolated-shell-application.md)」を参照してください。  
  
## <a name="allowing-for-updates-to-your-application"></a>アプリケーションの更新を許可する  
 インストールプログラムによって、Microsoft の更新プログラムまたは会社の更新プログラムによって、アプリケーションが更新される可能性があります。 更新プログラムの詳細については、「 [分離シェルアプリケーションのサービスガイドライン](../extensibility/servicing-guidelines-for-isolated-shell-applications.md)」を参照してください。
