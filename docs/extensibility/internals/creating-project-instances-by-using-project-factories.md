---
title: プロジェクト ファクトリを使用してプロジェクト インスタンスを作成する |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4a02d6dd09ec019ad05404c033889f89ed140dd1
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219498"
---
# <a name="create-project-instances-by-using-project-factories"></a>プロジェクト ファクトリを使用してプロジェクトのインスタンスを作成します。
プロジェクトの種類に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を使用して、*プロジェクト ファクトリ*プロジェクトのオブジェクトのインスタンスを作成します。 プロジェクト ファクトリは、標準のクラス ファクトリ cocreatable COM オブジェクトに似ています。 ただし、プロジェクトのオブジェクトが cocreatable;プロジェクト ファクトリを使用してのみ作成できます。  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE は、ユーザーが既存のプロジェクトを読み込みますかで新しいプロジェクトを作成、VSPackage の実装プロジェクト ファクトリを呼び出す[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。 新しいプロジェクトのオブジェクトを設定するための十分な情報を使用して IDE を提供する**ソリューション エクスプ ローラー**します。 新しいプロジェクトのオブジェクトには、IDE によって開始されたすべての関連する UI 操作をサポートするため、必要なインターフェイスも提供します。  
  
 実装することができます、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>プロジェクト内のクラスのインターフェイス。 通常、独自のモジュールに存在します。  
  
 所有者によって集計をサポートするプロジェクトは、プロジェクト ファイルで、所有者のキーを保持する必要があります。 ときに、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 、所有者キー プロジェクトでメソッドを呼び出すと、所有しているプロジェクトは、その所有者のキーを GUID を呼び出してプロジェクト ファクトリに変換します、`CreateProject`を実際の作成を行うには、このプロジェクト ファクトリ メソッド。  
  
## <a name="create-an-owned-project"></a>所有プロジェクトを作成します。  
 所有者は、2 つのフェーズで、所有しているプロジェクトを作成します。  
  
1. 呼び出すことによって、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A>メソッド。 これは、方法により所有されているプロジェクト、入力の制御に基づく集計プロジェクト オブジェクトを作成する`IUnknown`します。 所有されているプロジェクト内部の渡します`IUnknown`と所有者のプロジェクトに集計されたオブジェクト。 これは、方法により、所有しているプロジェクト内部に格納する`IUnknown`します。  
  
2. 呼び出すことによって、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>メソッド。 呼び出す代わりにこのメソッドが呼び出されたときに、所有しているプロジェクトは、すべてのインスタンス生成`IVsProjectFactory::CreateProject`が所有していないプロジェクトの場合と同様です。 入力`VSOWNEDPROJECTOBJECT`列挙体は、通常、集計、所有しているプロジェクト。 所有しているプロジェクトは、この変数を使用して、プロジェクト、そのオブジェクトが既に作成されているかどうかを判断する (cookie は NULL は等しくない) か、(クッキー等しい NULL) を作成する必要があります。  
  
   プロジェクトの種類は、GUID、cocreatable COM オブジェクトの CLSID のような一意のプロジェクトによって識別されます。 通常、1 つのプロジェクト ファクトリのハンドルが 1 つのプロジェクト ファクトリことはできますが、1 つのプロジェクトの種類のインスタンスを作成するは、1 つ以上のプロジェクト型 GUID を処理します。  
  
   プロジェクトの種類は、特定のファイル名拡張子に関連付けられます。 ユーザーは、既存のプロジェクト ファイルを開こうとしたり、テンプレートを複製して新しいプロジェクトを作成しようとしています、IDE は、対応するプロジェクトの GUID を決定するのにファイルの拡張機能を使用します。  
  
   IDE が下のシステム レジストリに情報を使用して、IDE では、新しいプロジェクトを作成するか、特定の型の既存のプロジェクトを開く必要がありますかを決定、すぐ **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]** を検索する VSPackage は、必要なプロジェクト ファクトリを実装します。 IDE には、この VSPackage が読み込まれます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>メソッド、VSPackage は呼び出すことにより、IDE でそのプロジェクト ファクトリを登録する必要があります、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A>メソッド。  
  
   主な方法、`IVsProjectFactory`インターフェイスは<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>、2 つのシナリオを処理する必要があります。 既存のプロジェクトを開き、新しいプロジェクトを作成します。 ほとんどのプロジェクトでは、プロジェクト ファイルで、プロジェクトの状態を格納します。 渡されるテンプレート ファイルのコピーを活用することで新しいプロジェクトを作成する、通常、`CreateProject`メソッドをコピーします。 既存のプロジェクトをインスタンス化に渡されるプロジェクト ファイルを開き直接`CreateProject`メソッド。 `CreateProject`メソッドは、必要に応じてユーザーに追加の UI 機能を表示できます。  
  
   プロジェクトは、ファイルも使用しないでき、代わりに、データベースや Web サーバーなど、ファイル システム以外のストレージ メカニズムにそのプロジェクトの状態を格納できます。 この例では、ファイル名のパラメーターが渡される、`CreateProject`メソッドではありませんが、ファイル システム パスを実際には、一意の文字列-URL: プロジェクト データを識別するためにします。 渡されるテンプレート ファイルをコピーする必要はありません`CreateProject`を実行する適切な作成のシーケンスをトリガーします。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>   
 [チェックリスト: 新しいプロジェクトの種類を作成します。](../../extensibility/internals/checklist-creating-new-project-types.md)