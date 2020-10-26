---
title: デザイナーの初期化とメタデータの構成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2dec3937616c712c56b7012949e044702e6b11f2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703064"
---
# <a name="designer-initialization-and-metadata-configuration"></a>デザイナーの初期化とメタデータの構成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デザイナーまたはデザイナーコンポーネントに関連付けられているメタデータ属性およびフィルター属性を操作すると、アプリケーションは、デザイナー <xref:System.Type> が使用できるとき、および Visual STUDIO IDE がデザイナーをサポートするように構成されているかどうか (たとえば、 **ツールボックス** のカテゴリまたはタブが使用可能な場合) を定義できます。  
  
 には、 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] デザイナーまたはデザイナーコンポーネントの初期化と、VSPackage によるメタデータの操作の制御を容易にするいくつかのメカニズムが用意されています。  
  
## <a name="initializing-metadata-and-configuration-information"></a>メタデータと構成情報の初期化  
 Vspackage は要求時に読み込まれるため、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デザイナーをインスタンス化する前に、環境によって読み込まれていない可能性があります。 したがって、Vspackage は、イベントを処理するために、作成時にデザイナーまたはデザイナーコンポーネントを構成するための標準メカニズムを使用することはできません <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> 。 代わりに、VSPackage はインターフェイスのインスタンスを実装 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> し、それ自体を登録して、デザインサーフェイス拡張機能と呼ばれるカスタマイズを提供します。  
  
### <a name="customizing-initialization"></a>カスタマイズ (初期化を)  
 デザイナー、コンポーネント、またはデザイナー画面をカスタマイズするには、次の操作を行います。  
  
1. デザイナーのメタデータを変更し、特定のに <xref:System.Type> アクセスまたは変換する方法を効果的に変更する。  
  
     通常、これはまたはのメカニズムを使用して行われ <xref:System.Drawing.Design.UITypeEditor> <xref:System.ComponentModel.TypeConverter> ます。  
  
     たとえば、ベースの <xref:System.Windows.Forms> デザイナーが初期化されると、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] <xref:System.Drawing.Design.UITypeEditor> リソースマネージャーを使用して <xref:System.Web.UI.WebControls.Image> ファイルシステムではなくビットマップを取得するために、デザイナーで使用するオブジェクトのが環境によって変更されます。  
  
2. たとえば、イベントをサブスクライブしたり、プロジェクトの構成情報を取得したりして、環境と統合します。 インターフェイスを取得することで、プロジェクトの構成情報を取得し、イベントをサブスクライブでき <xref:System.ComponentModel.Design.ITypeResolutionService> ます。  
  
3. 適切な **ツールボックス** カテゴリをアクティブにしたり、デザイナーにクラスのインスタンスを適用してデザイナーの適用性を制限したりすることによって、ユーザー環境を変更し <xref:System.ComponentModel.ToolboxItemFilterAttribute> ます。  
  
### <a name="designer-initialization-by-a-vspackage"></a>VSPackage によるデザイナーの初期化  
 VSPackage は、次の方法でデザイナーの初期化を処理する必要があります。  
  
1. クラスを実装するオブジェクトを作成 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> します。  
  
   > [!NOTE]
   > クラスは、 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> クラスと同じオブジェクトに実装しないでください <xref:Microsoft.VisualStudio.Shell.Package> 。  
  
2. <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>のインスタンスを適用することによって、VSPackage のデザイナー拡張機能のサポートを提供するように、クラスを登録し <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ます。また、VSPackage のの実装を提供するクラスにを実装し <xref:Microsoft.VisualStudio.Shell.Package> ます。  
  
   デザイナーまたはデザイナーコンポーネントが作成されるたびに、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境は次のようになります。  
  
3. 登録されている各デザインサーフェイス拡張機能プロバイダーにアクセスします。  
  
4. 各デザインサーフェイス拡張機能プロバイダーのオブジェクトのインスタンスをインスタンス化し、初期化します。 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>  
  
5. 各デザインサーフェイス拡張機能プロバイダーの <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> メソッドまたは <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> メソッドを (必要に応じて) 呼び出します。  
  
   <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>オブジェクトを VSPackage のメンバーとして実装する場合は、次の点を理解しておくことが重要です。  
  
6. 環境では、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 特定のプロバイダーによって変更されるメタデータやその他の構成設定を制御することはできません `DesignSurfaceExtension` 。 競合する方法で、2つ以上の `DesignSurfaceExtension` プロバイダーが同じデザイナー機能を変更し、最終的な変更が明確になる可能性があります。 どの変更が最後に適用されたかは不確定です。  
  
7. <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>のインスタンスをその実装に適用することで、オブジェクトの実装を特定のデザイナーに明示的に制限することができ <xref:System.ComponentModel.ToolboxItemFilterAttribute> ます。 **ツールボックス**項目のフィルター処理の詳細については、「」および「」を参照してください <xref:System.ComponentModel.ToolboxItemFilterAttribute> <xref:System.ComponentModel.ToolboxItemFilterType> 。  
  
## <a name="additional-metadata-provisioning"></a>追加のメタデータのプロビジョニング  
 VSPackage は、デザイン時以外のデザイナーまたはデザイナーコンポーネントの構成を変更できます。  
  
 クラスは、 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> プログラムで使用することも、デザイナーを提供する VSPackage に適用することもできます。  
  
 クラスのインスタンス <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> は、デザインサーフェイスで作成されたコンポーネントのメタデータを変更するために使用されます。 たとえば、カスタムプロパティブラウザーを使用して、オブジェクトによって使用される既定のプロパティブラウザーを置き換えることができ <xref:System.Windows.Forms.CommonDialog> ます。  
  
 の VSPackage の実装に適用されるのインスタンスによって提供される変更 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> <xref:Microsoft.VisualStudio.Shell.Package> は、次の2つのスコープのいずれかを持つことができます。  
  
- Global--指定されたコンポーネントのすべての新しいインスタンスに対して  
  
- Local--現在の VSPackage によって提供されるデザインサーフェイス上に作成されたコンポーネントのインスタンスにのみ関連します。  
  
  `IsGlobal` <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> VSPackage のの実装に適用されるインスタンスのプロパティによって、 <xref:Microsoft.VisualStudio.Shell.Package> このスコープが決まります。  
  
  次のように、に設定されているオブジェクトのプロパティを使用しての実装に属性を適用する <xref:Microsoft.VisualStudio.Shell.Package> <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> と、 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> `true` 環境全体のブラウザーが変更され [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
  Global フラグがに設定されている場合、 `false` メタデータの変更は現在の VSPackage でサポートされている現在のデザイナーに対してローカルになります。  
  
  `[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`  
  
  `internal class MyPackage : Package {}`  
  
> [!NOTE]
> 現時点では、デザインサーフェイスはコンポーネントの作成のみをサポートしているため、ローカルメタデータを持つことができるのはコンポーネントのみです。 上の例では、オブジェクトのプロパティなどのプロパティを変更しようとしてい `Color` ます。 `false`がグローバルフラグに渡された場合、 `CustomBrowser` デザイナーは実際にのインスタンスを作成することはないため、は表示されません `Color` 。 グローバルフラグをに設定すると、 `false` コントロール、タイマー、ダイアログボックスなどのコンポーネントに役立ちます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>   
 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>   
 <xref:System.ComponentModel.ToolboxItemFilterType>   
 [デザイン時サポートの拡張](https://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)
