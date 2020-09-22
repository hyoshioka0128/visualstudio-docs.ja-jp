---
title: プロジェクトのアップグレード |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- upgrading VSPackages
- upgrading applications, strategies
- VSPackages, upgrade support
ms.assetid: e01cb44a-8105-4cf4-8223-dfae65f8597a
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8e838cb02aa1a620356f96d9e77f1752797ac409
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841464"
---
# <a name="upgrading-projects"></a>プロジェクトのアップグレード
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトモデルをのあるバージョンから [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 次のバージョンに変更すると、新しいバージョンで実行できるように、プロジェクトとソリューションをアップグレードすることが必要になる場合があります。 には、 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 独自のプロジェクトで upgrade support を実装するために使用できるインターフェイスが用意されています。  
  
## <a name="upgrade-strategies"></a>アップグレード戦略  
 アップグレードをサポートするには、プロジェクトシステムの実装で、アップグレード戦略を定義して実装する必要があります。 戦略を決定する際には、サイドバイサイド (SxS) バックアップ、コピーバックアップ、またはその両方をサポートすることを選択できます。  
  
- SxS バックアップとは、プロジェクトでは、アップグレードが必要なファイルのみをコピーし、適切なファイル名サフィックスを追加することを意味します。たとえば、".old" のようになります。  
  
- コピーバックアップとは、プロジェクトがすべてのプロジェクト項目をユーザー指定のバックアップの場所にコピーすることを意味します。 その後、元のプロジェクトの場所にある関連ファイルがアップグレードされます。  
  
## <a name="how-upgrade-works"></a>アップグレードのしくみ  
 以前のバージョンので作成されたソリューションを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 新しいバージョンで開くと、IDE はソリューションファイルをチェックして、アップグレードが必要かどうかを判断します。 アップグレードが必要な場合は、アップグレード **ウィザード** が自動的に起動して、アップグレードプロセスをユーザーに案内します。  
  
 ソリューションをアップグレードする必要がある場合は、各プロジェクトファクトリに対して、アップグレードの戦略についてクエリを行います。 この戦略では、プロジェクトファクトリがコピーバックアップと SxS バックアップのどちらをサポートするかを決定します。 この情報は **アップグレードウィザード**に送信され、バックアップに必要な情報が収集され、該当するオプションがユーザーに提示されます。  
  
### <a name="multi-project-solutions"></a>複数のプロジェクトから成るソリューション  
 ソリューションに複数のプロジェクトが含まれており、アップグレード戦略が異なる場合 (たとえば、SxS バックアップのみをサポートする C++ プロジェクトや、コピーバックアップのみをサポートする Web プロジェクトの場合など)、プロジェクトファクトリはアップグレード戦略をネゴシエートする必要があります。  
  
 ソリューションは、の各プロジェクトファクトリに対してクエリを <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> 行います。 次に、を呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A> グローバルプロジェクトファイルのアップグレードが必要かどうかを確認し、サポートされているアップグレード方法を確認します。 次に、 **アップグレードウィザード** が呼び出されます。  
  
 ユーザーがウィザードを完了すると、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> 各プロジェクトファクトリでが呼び出され、実際のアップグレードが実行されます。 バックアップを容易にするために、IVsProjectUpgradeViaFactory メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> アップグレードプロセスの詳細をログに記録するサービスを提供します。 このサービスをキャッシュすることはできません。  
  
 関連するすべてのグローバルファイルを更新した後、プロジェクトファクトリはプロジェクトのインスタンスを選択できます。 プロジェクトの実装では、をサポートする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A>次に、メソッドを呼び出して、関連するすべてのプロジェクト項目をアップグレードします。  
  
> [!NOTE]
> メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> SVsUpgradeLogger サービスを提供しません。 このサービスは、を呼び出すことによって取得でき <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> ます。  
  
## <a name="best-practices"></a>推奨する運用方法  
 サービスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> ファイルを編集する前に編集できるかどうかを確認し、保存する前に保存しておくことができます。 これにより、バックアップとアップグレードの実装で、ソース管理下のプロジェクトファイル、十分なアクセス許可のないファイルなどを処理できます。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>アップグレードプロセスの成功または失敗に関する情報を提供するために、バックアップとアップグレードのすべてのフェーズでサービスを使用します。  
  
 プロジェクトのバックアップとアップグレードの詳細については、vsshell2 での IVsProjectUpgrade に関するコメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [イベント](../../extensibility/internals/projects.md)   
 [カスタムプロジェクトのアップグレード](../../misc/upgrading-custom-projects.md)   
 [プロジェクト項目のアップグレード](../../misc/upgrading-project-items.md)
