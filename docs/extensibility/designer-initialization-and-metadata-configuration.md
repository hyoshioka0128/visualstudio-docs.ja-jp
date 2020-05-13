---
title: デザイナーの初期化とメタデータの構成 |マイクロソフトドキュメント
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
ms.openlocfilehash: e876dd9e6fa95bbe180d1737bc8c4911f16e1e9a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712224"
---
# <a name="designer-initialization-and-metadata-configuration"></a>デザイナーの初期化とメタデータの構成

デザイナーまたはデザイナー コンポーネントに関連付けられたメタデータ属性とフィルター属性を操作すると、デザイナーが使用できる場合に、特定のデザイナーで使用<xref:System.Type>するツール (データ構造、クラス、グラフィカル エンティティなど) を定義したり、Visual Studio IDE がデザイナーをサポートするように構成する方法 (**ツールボックス**カテゴリまたはタブが使用可能な場合など) を定義するメカニズムが提供されます。

には[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]、デザイナーまたはデザイナー コンポーネントの初期化と VSPackage によるメタデータの操作を容易にするためのいくつかのメカニズムが用意されています。

## <a name="initialize-metadata-and-configuration-information"></a>メタデータと構成情報の初期化
 必要に応じて読み込まれるため、デザイナーのインスタンス化前に、VsPackage が Visual Studio 環境によって読み込まれていない可能性があります。 したがって、VSPackages は、デザイナーまたはデザイナー コンポーネントを作成時に構成するための標準のメカニズムを<xref:System.ComponentModel.Design.IDesignerEventService.DesignerCreated>使用できません。 代わりに、VSPackage は<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>インターフェイスのインスタンスを実装し、デザイン サーフェイス拡張機能と呼ばれるカスタマイズを提供するために自身を登録します。

### <a name="customize-initialization"></a>初期化のカスタマイズ

デザイナー、コンポーネント、またはデザイナー画面のカスタマイズには、次の作業が含まれます。

1. デザイナー メタデータを変更し、特定<xref:System.Type>のメタデータへのアクセスまたは変換方法を効果的に変更する。

    これは通常、 または<xref:System.Drawing.Design.UITypeEditor><xref:System.ComponentModel.TypeConverter>機構を通じて行われます。

    たとえば、ベースの<xref:System.Windows.Forms>デザイナーが初期化されると、Visual Studio 環境は、リソース<xref:System.Drawing.Design.UITypeEditor><xref:System.Web.UI.WebControls.Image>マネージャーを使用してファイル システムではなくビットマップを取得するように、デザイナーで使用されるオブジェクトを変更します。

2. イベントのサブスクライブやプロジェクト構成情報の取得などにより、環境との統合。 インターフェイスを取得すると、プロジェクト構成情報を取得し、イベントを<xref:System.ComponentModel.Design.ITypeResolutionService>サブスクライブできます。

3. 適切な**ツールボックス**カテゴリをアクティブにするか、クラスのインスタンスをデザイナーに適用することによってデザイナーの適用性を<xref:System.ComponentModel.ToolboxItemFilterAttribute>制限することによって、ユーザー環境を変更します。

### <a name="designer-initialization-by-a-vspackage"></a>VS パッケージによるデザイナーの初期化

VSPackage は、デザイナーの初期化を次の方法で処理する必要があります。

1. クラスを実装するオブジェクト<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>を作成します。

   > [!NOTE]
   > クラス<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>は、クラスと同じオブジェクト<xref:Microsoft.VisualStudio.Shell.Package>に実装しないでください。

2. VSPackage のデザイナー拡張機能<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>のサポートを提供するとして実装するクラスを登録します。 <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute><xref:Microsoft.VisualStudio.Shell.ProvideObjectAttribute>の<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>インスタンスを適用して、クラスを登録します<xref:Microsoft.VisualStudio.Shell.Package>。

デザイナーまたはデザイナー コンポーネントが作成されるたびに、Visual Studio 環境は次のようになります。

- 登録されている各デザイン サーフェイス拡張プロバイダーにアクセスします。

- 各デザイン サーフェイス拡張機能プロバイダーの<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>オブジェクトのインスタンスをインスタンス化して初期化します。

- 各デザイン サーフェイス拡張プロバイダーの<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnDesignerCreated%2A>メソッドまたは<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension.OnComponentCreated%2A>メソッドを呼び出します (必要に応じて)。

VSPackage<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>のメンバーとしてオブジェクトを実装する場合、次の点を理解することが重要です。

- Visual Studio 環境では、特定`DesignSurfaceExtension`のプロバイダーが変更するメタデータやその他の構成設定を制御することはできません。 2 つ以上`DesignSurfaceExtension`のプロバイダーが、競合する方法で同じデザイナー機能を変更し、最終的な変更が確実である可能性があります。 どの変更が最後に適用されたかは不確定です。

- のインスタンスをその実装に適用することで、<xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>オブジェクトの実装を特定の<xref:System.ComponentModel.ToolboxItemFilterAttribute>デザイナーに明示的に制限できます。 **ツールボックス**項目のフィルター処理の詳細については、「 」<xref:System.ComponentModel.ToolboxItemFilterAttribute>および<xref:System.ComponentModel.ToolboxItemFilterType>「 」を参照してください。

## <a name="additional-metadata-provisioning"></a>追加のメタデータプロビジョニング

VSPackage は、デザイン時以外のデザイナーまたはデザイナー コンポーネントの構成を変更できます。

クラス<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>はプログラムで使用することも、デザイナーを提供する VSPackage に適用することもできます。

クラスのインスタンスは<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>、デザイン サーフェイスで作成されたコンポーネントのメタデータを変更するために使用されます。 たとえば、<xref:System.Windows.Forms.CommonDialog>オブジェクトで使用される既定のプロパティ ブラウザをカスタム プロパティ ブラウザに置き換えることができます。

VSPackage の<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>実装に適用されるインスタンスによって提供される変更は<xref:Microsoft.VisualStudio.Shell.Package>、次の 2 つのスコープのいずれかを持つことができます。

- グローバル -- 指定されたコンポーネントのすべての新しいインスタンスに対して

- ローカル -- 現在の VSPackage によって提供されるデザイン サーフェイスで作成されたコンポーネントのインスタンスにのみ関連します。

VSPackage`IsGlobal`の<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>実装に適用されるインスタンスのプロパティによって、この<xref:Microsoft.VisualStudio.Shell.Package>スコープが決定されます。

<xref:Microsoft.VisualStudio.Shell.Package>次のように、オブジェクトの<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute.IsGlobal%2A>プロパティを<xref:Microsoft.VisualStudio.Shell.Design.ProvideDesignerMetadataAttribute>`true`に設定しての実装に属性を適用すると、Visual Studio 環境全体のブラウザーが変更されます。

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=true`  `)]`

`internal class MyPackage : Package {}`

グローバル フラグが に`false`設定されている場合、メタデータの変更は、現在の VSPackage でサポートされている現在のデザイナーに対してローカルになります。

`[ProvideDesignerMetadata(typeof(Color), typeof(CustomBrowser),`   `IsGlobal=false`  `)]`

`internal class MyPackage : Package {}`

> [!NOTE]
> デザインサーフェイスではコンポーネントの作成のみがサポートされているため、ローカルメタデータを持つことができるコンポーネントだけが可能です。 上の例では、オブジェクトのプロパティなどのプロパティを`Color`変更しようとしています。 グローバル`false`フラグに渡された場合、`CustomBrowser`デザイナーは実際に`Color`のインスタンスを作成しないため、表示されることはありません。 グローバル フラグをに`false`設定すると、コントロール、タイマー、ダイアログ ボックスなどのコンポーネントに便利です。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtension>
- <xref:Microsoft.VisualStudio.Shell.Design.DesignSurfaceExtensionAttribute>
- <xref:System.ComponentModel.ToolboxItemFilterType>
- [デザイン時サポートの拡張](https://msdn.microsoft.com/Library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)
