---
title: プロジェクト項目のアップグレード |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- upgrading project items
- projects [Visual Studio SDK], upgrading items
- project items [Visual Studio], upgrading
ms.assetid: 8af29dd4-eaf1-4b3c-b602-198e1a3dff23
caps.latest.revision: 14
manager: jillfra
ms.openlocfilehash: eb3619e187c7856cf03ee60c8a04cbe527bf0a69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65698685"
---
# <a name="upgrading-project-items"></a>プロジェクト項目のアップグレード
を実装していないプロジェクトシステム内の項目を追加または管理する場合は、プロジェクトのアップグレードプロセスに参加する必要があります。 Crystal Reports は、プロジェクトシステムに追加できるアイテムの例です。  
  
 通常、プロジェクト項目の実装者は、既に完全にインスタンス化され、アップグレードされたプロジェクトを活用する必要があります。これは、プロジェクトが参照している内容と、アップグレードを決定するためにどのようなプロジェクトプロパティがあるかを把握する必要があるためです。  
  
### <a name="to-get-the-project-upgrade-notification"></a>プロジェクトのアップグレード通知を取得するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading>プロジェクト項目の実装でフラグ (vsshell80 で定義) を設定します。 これにより、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトシステムがアップグレード中であることがシェルによって判断されたときに、プロジェクト項目 VSPackage が自動読み込みされます。  
  
2. メソッドを使用してインターフェイスをアドバイスし <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A> ます。  
  
3. この <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> インターフェイスは、プロジェクトシステムの実装がアップグレード操作を完了し、アップグレードされた新しいプロジェクトが作成された後に発生します。 シナリオによっては、、、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> またはメソッドの後にインターフェイスが起動され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> ます。  
  
### <a name="to-upgrade-the-project-item-files"></a>プロジェクト項目ファイルをアップグレードするには  
  
1. プロジェクト項目の実装では、ファイルのバックアッププロセスを慎重に管理する必要があります。 これは、並列バックアップの場合に特に当てはまります。この場合、 `fUpgradeFlag` <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> バックアップされたファイルは、".old" として指定されたファイルに従って配置されます。 プロジェクトをアップグレードしたときのシステム時刻より古いバックアップファイルは、古いものとして指定できます。 また、これを回避する特定の手順を実行しない限り、上書きされる可能性があります。  
  
2. プロジェクト項目がプロジェクトのアップグレードの通知を受け取ると、 **Visual Studio 変換ウィザード** が引き続き表示されます。 したがって、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> ウィザードの UI にアップグレードメッセージを提供するには、インターフェイスのメソッドを使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [Visual Studio 変換ウィザード](https://msdn.microsoft.com/4acfd30e-c192-4184-a86f-2da5e4c3d83c)   
 [カスタム プロジェクトのアップグレード](../misc/upgrading-custom-projects.md)