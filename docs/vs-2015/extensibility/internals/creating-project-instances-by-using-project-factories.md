---
title: プロジェクトファクトリを使用したプロジェクトインスタンスの作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f26b11aaf74b73535c82ebcd6422f3be0bba3f22
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697202"
---
# <a name="creating-project-instances-by-using-project-factories"></a>プロジェクト ファクトリを使用したプロジェクト インスタンスの作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

のプロジェクトの種類で [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、プロジェクト *ファクトリ* を使用して、プロジェクトオブジェクトのインスタンスを作成します。 プロジェクトファクトリは、cocreatable 可能な COM オブジェクトの標準クラスファクトリに似ています。 ただし、プロジェクトオブジェクトは共同作成可能ではなく、プロジェクトファクトリを使用してのみ作成できます。  
  
 IDE は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ユーザーが既存のプロジェクトを読み込むか、で新しいプロジェクトを作成するときに、VSPackage に実装されているプロジェクトファクトリを呼び出し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 新しい project オブジェクトは、ソリューションエクスプローラーを設定するのに十分な情報を IDE に提供します。 新しいプロジェクトオブジェクトには、IDE によって開始された関連するすべての UI 操作をサポートするために必要なインターフェイスも用意されています。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>プロジェクトのクラスにインターフェイスを実装できます。 通常は、独自のモジュールに存在します。  
  
 インターフェイスの実装の例につい `IVsProjectFactory` ては、 [基本的なプロジェクト](https://msdn.microsoft.com/385fd2a3-d9f1-4808-87c2-a3f05a91fc36) サンプルディレクトリに含まれる PrjFac を参照してください。  
  
 所有者による集計をサポートするプロジェクトは、プロジェクトファイルで所有者キーを保持する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>所有者キーを持つプロジェクトでメソッドが呼び出されると、所有されているプロジェクトは所有者キーをプロジェクトファクトリ GUID に変換し、 `CreateProject` このプロジェクトファクトリでメソッドを呼び出して実際の作成を行います。  
  
## <a name="creating-an-owned-project"></a>所有プロジェクトの作成  
 所有者が所有するプロジェクトを作成するには、次の2つのフェーズがあります。  
  
1. メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A> ます。 これにより、所有プロジェクトは、入力の制御に基づいて集計されたプロジェクトオブジェクトを作成できるように `IUnknown` なります。 所有されているプロジェクトは、内部および集計された `IUnknown` オブジェクトを所有者プロジェクトに渡します。 これにより、所有しているプロジェクトは内部を格納する可能性が `IUnknown` あります。  
  
2. メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A> ます。 所有し `IVsProjectFactory::CreateProject` ていないプロジェクトの場合と同じように、を呼び出す代わりに、このメソッドが呼び出されると、所有されているプロジェクトはすべてのインスタンス化を行います。 通常、入力 `VSOWNEDPROJECTOBJECT` 列挙は、集計された所有プロジェクトです。 所有プロジェクトでは、この変数を使用して、プロジェクトオブジェクトが既に作成されている (cookie が NULL ではない) か、または作成する必要がある (cookie が NULL である) かどうかを判断できます。  
  
   プロジェクトの種類は、cocreatable 可能な COM オブジェクトの CLSID と同様に、一意のプロジェクト GUID によって識別されます。 通常、1つのプロジェクトファクトリは、1つのプロジェクトの種類のインスタンスの作成を処理しますが、1つのプロジェクトファクトリで1つ以上のプロジェクトの種類の GUID を処理することもできます。  
  
   プロジェクトの種類は、特定のファイル名拡張子に関連付けられています。 ユーザーが既存のプロジェクトファイルを開こうとしたとき、またはテンプレートを複製して新しいプロジェクトを作成しようとすると、IDE はファイルの拡張機能を使用して、対応するプロジェクト GUID を特定します。  
  
   IDE は、新しいプロジェクトを作成する必要があるか、特定の種類の既存のプロジェクトを開く必要があるかを判断したら、[HKEY_LOCAL_MACHINE \Software\Microsoft\VisualStudio\8.0\Projects] の下にあるシステムレジストリの情報を使用して、必要なプロジェクトファクトリを実装している VSPackage を見つけます。 IDE はこの VSPackage を読み込みます。 メソッドでは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> VSPackage はメソッドを呼び出すことによって、プロジェクトファクトリを IDE に登録する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A> ます。  
  
   インターフェイスの主要な方法 `IVsProjectFactory` は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> 既存のプロジェクトを開き、新しいプロジェクトを作成するという2つのシナリオを処理することです。 ほとんどのプロジェクトは、プロジェクトの状態をプロジェクトファイルに格納します。 通常、新しいプロジェクトを作成するには、メソッドに渡されたテンプレートファイルのコピーを作成し、その `CreateProject` コピーを開きます。 既存のプロジェクトは、メソッドに渡されたプロジェクトファイルを直接開くことによってインスタンス化され `CreateProject` ます。 メソッドは、必要に応じ `CreateProject` てユーザーに追加の UI 機能を表示できます。  
  
   プロジェクトはファイルを使用することもできません。また、プロジェクトの状態を、データベースや Web サーバーなどのファイルシステム以外のストレージメカニズムに格納することもできます。 この場合、メソッドに渡されるファイル名パラメーター `CreateProject` は、実際にはファイルシステムパスではなく、一意の文字列 (URL) であり、プロジェクトデータを識別します。 に渡されたテンプレートファイルをコピーして `CreateProject` 、実行する適切な構築シーケンスをトリガーする必要はありません。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>   
 [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
