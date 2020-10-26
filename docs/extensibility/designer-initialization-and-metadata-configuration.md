---
title: デザイナーの初期化とメタデータの構成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], initializing
- designers [Visual Studio SDK], configuring metadata
ms.assetid: f7fe9a7e-f669-4642-ad5d-186b2e6e6ec9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f48d8ebb285bdc8211f590f49e615042b7029d70
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011710"
---
# <a name="designer-initialization-and-metadata-configuration"></a>デザイナーの初期化とメタデータの構成

デザイナーまたはデザイナーコンポーネントに関連付けられているメタデータ属性およびフィルター属性を操作すると、アプリケーションは、デザイナー <xref:System.Type> が使用できるとき、および Visual STUDIO IDE がデザイナーをサポートするように構成されているかどうか (たとえば、 **ツールボックス** のカテゴリまたはタブが使用可能な場合) を定義できます。

には、 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] デザイナーまたはデザイナーコンポーネントの初期化と、VSPackage によるメタデータの操作の制御を容易にするいくつかのメカニズムが用意されています。

## <a name="initialize-metadata-and-configuration-information"></a>メタデータと構成情報の初期化
 Vspackage は要求時に読み込まれるため、デザイナーをインスタンス化する前に、Visual Studio 環境によって読み込まれていない可能性があります。 したがって、Vspackage は、イベントを処理するために、作成時にデザイナーまたはデザイナーコンポーネントを構成するための標準メカニズムを使用することはできません <xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated> 。 代わりに、VSPackage はインターフェイスのインスタンスを実装 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> し、それ自体を登録して、デザインサーフェイス拡張機能と呼ばれるカスタマイズを提供します。

### <a name="customize-initialization"></a>初期化のカスタマイズ

デザイナー、コンポーネント、またはデザイナー画面をカスタマイズするには、次の操作を行います。

1. デザイナーのメタデータを変更し、特定のに <xref:System.Type> アクセスまたは変換する方法を効果的に変更する。

    通常、これはまたはのメカニズムを使用して行われ <xref:System.Drawing.Design.UITypeEditor> <xref:System.ComponentModel.TypeConverter> ます。

    たとえば、ベースの <xref:System.Windows.Forms> デザイナーが初期化されると、Visual Studio 環境は、 <xref:System.Drawing.Design.UITypeEditor> <xref:System.Web.UI.WebControls.Image> リソースマネージャーを使用してファイルシステムではなくビットマップを取得するために、デザイナーで使用されるオブジェクトのを変更します。

2. たとえば、イベントをサブスクライブしたり、プロジェクトの構成情報を取得したりして、環境と統合します。 インターフェイスを取得することで、プロジェクトの構成情報を取得し、イベントをサブスクライブでき <xref:System.ComponentModel.Design.ITypeResolutionService> ます。

3. 適切な **ツールボックス** カテゴリをアクティブにしたり、デザイナーにクラスのインスタンスを適用してデザイナーの適用性を制限したりすることによって、ユーザー環境を変更し <xref:System.ComponentModel.ToolboxItemFilterAttribute> ます。

### <a name="designer-initialization-by-a-vspackage"></a>VSPackage によるデザイナーの初期化

VSPackage は、次の方法でデザイナーの初期化を処理する必要があります。

1. クラスを実装するオブジェクトを作成 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> します。

   > [!NOTE]
   > クラスは、 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> クラスと同じオブジェクトに実装しないでください <xref:Microsoft.VisualStudio.Shell.Package> 。

2. を実装するクラスを、 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> VSPackage のデザイナー拡張機能のサポートを提供するように登録します。 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>、、およびのインスタンスを、 <xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute> VSPackage の <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> の実装を提供するクラスに適用して、クラスを登録し <xref:Microsoft.VisualStudio.Shell.Package> ます。

デザイナーまたはデザイナーコンポーネントが作成されるたびに、Visual Studio 環境は次のようになります。

- 登録されている各デザインサーフェイス拡張機能プロバイダーにアクセスします。

- 各デザインサーフェイス拡張機能プロバイダーのオブジェクトのインスタンスをインスタンス化し、初期化し <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension> ます。

- 各デザインサーフェイス拡張機能プロバイダーの <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A> メソッドまたは <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A> メソッドを (必要に応じて) 呼び出します。

<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>オブジェクトを VSPackage のメンバーとして実装する場合は、次の点を理解しておくことが重要です。

- Visual Studio 環境では、特定のプロバイダーによって変更されるメタデータやその他の構成設定を制御することはできません `DesignSurfaceExtension` 。 競合する方法で、2つ以上の `DesignSurfaceExtension` プロバイダーが同じデザイナー機能を変更し、最終的な変更が明確になる可能性があります。 どの変更が最後に適用されたかは不確定です。

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>のインスタンスをその実装に適用することで、オブジェクトの実装を特定のデザイナーに明示的に制限することができ <xref:System.ComponentModel.ToolboxItemFilterAttribute> ます。 **ツールボックス**項目のフィルター処理の詳細については、「」および「」を参照してください <xref:System.ComponentModel.ToolboxItemFilterAttribute> <xref:System.ComponentModel.ToolboxItemFilterType> 。

## <a name="additional-metadata-provisioning"></a>追加のメタデータのプロビジョニング

VSPackage は、デザイン時以外のデザイナーまたはデザイナーコンポーネントの構成を変更できます。

クラスは、 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> プログラムで使用することも、デザイナーを提供する VSPackage に適用することもできます。

クラスのインスタンス <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> は、デザインサーフェイスで作成されたコンポーネントのメタデータを変更するために使用されます。 たとえば、オブジェクトによって使用される既定のプロパティブラウザーを <xref:System.Windows.Forms.CommonDialog> カスタムプロパティブラウザーに置き換えることができます。

の VSPackage の実装に適用されるのインスタンスによって提供される変更 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> <xref:Microsoft.VisualStudio.Shell.Package> は、次の2つのスコープのいずれかを持つことができます。

- Global--指定されたコンポーネントのすべての新しいインスタンスに対して

- Local--現在の VSPackage によって提供されるデザインサーフェイス上に作成されたコンポーネントのインスタンスにのみ関連します。

`IsGlobal` <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> VSPackage のの実装に適用されるインスタンスのプロパティによって、 <xref:Microsoft.VisualStudio.Shell.Package> このスコープが決まります。

次に示すように、に設定されているオブジェクトのプロパティを使用しての実装に属性を適用する <xref:Microsoft.VisualStudio.Shell.Package> <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A> と、 <xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute> `true` Visual Studio 環境全体のブラウザーが変更されます。

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

Global フラグがに設定されている場合、 `false` メタデータの変更は現在の VSPackage でサポートされている現在のデザイナーに対してローカルになります。

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> デザインサーフェイスはコンポーネントの作成のみをサポートするため、ローカルメタデータを持つことができるのはコンポーネントのみです。 上の例では、オブジェクトのプロパティなどのプロパティを変更しようとしてい `Color` ます。 `false`がグローバルフラグに渡された場合、 `CustomBrowser` デザイナーは実際にのインスタンスを作成することはないため、は表示されません `Color` 。 グローバルフラグをに設定すると、 `false` コントロール、タイマー、ダイアログボックスなどのコンポーネントに役立ちます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [デザイン時サポートの拡張](/previous-versions/37899azc(v=vs.140))