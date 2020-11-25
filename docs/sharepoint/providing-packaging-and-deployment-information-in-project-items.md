---
title: プロジェクト項目の & 配置情報のパッケージ化
description: フィーチャープロパティ、フィーチャーレシーバー、プロジェクト出力参照、および安全なコントロールエンティティを使用して、SharePoint プロジェクトアイテムにパッケージ化および配置データを追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SafeControlEntries
- VS.SharePointTools.Project.ProjectOutputReference
- VS.SharePointTools.Project.FeatureProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature properties
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
- feature properties [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, feature receiver
- feature receiver [SharePoint development in Visual Studio]
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f73d8727fb960cf519d368d928aa20cae38ae1a9
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95970478"
---
# <a name="provide-packaging-and-deployment-information-in-project-items"></a>プロジェクト項目でのパッケージ化と配置の情報を提供する
  のすべての SharePoint プロジェクトアイテムには [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、プロジェクトを sharepoint に配置するときに追加データを提供するために使用できるプロパティがあります。 選択できるプロパティは次のとおりです。

- 機能プロパティ

- 機能レシーバー

- プロジェクト出力参照

- 安全なコントロール エントリ

  これらのプロパティは、[ **プロパティ** ] ウィンドウに表示されます。

## <a name="feature-properties"></a>機能のプロパティ
 機能によって使用されるデータを指定するには、" **機能のプロパティ** " プロパティを使用します。 機能プロパティデータは、SharePoint に配置するときにフィーチャーに含まれる値のセットです (キーと値のペアとして格納されます)。 フィーチャーが配置されると、そのプロパティ値にコードでアクセスできるようになります。

 フィーチャープロパティ値をプロジェクト項目に追加すると、その値は項目のフィーチャーのマニフェストの要素として追加されます。 たとえば、Business Data Connectivity (BDC) モデルプロジェクトでは、ModelFileName 機能プロパティは次のように表示されます。

```xml
<Property Key="ModelFileName" Value="BdcModel1\BdcModel1.bdcm" />
```

 フィーチャーのプロパティ値を設定すると、プロジェクトの *sharepointprojectitem.spdata* ファイルに featureproperty 要素として追加されます。 SharePoint でのプロパティへのアクセスの詳細については、「 [SPFeaturePropertyCollection クラス](/previous-versions/office/sharepoint-server/ms461895(v=office.15))」を参照してください。

 すべてのプロジェクト項目の同一機能プロパティ値がフィーチャーマニフェストにマージされます。 ただし、2つの異なるプロジェクトアイテムが、一致しない値を持つ同じ特徴プロパティキーを指定した場合、検証エラーが発生します。

 機能のプロパティをフィーチャーファイル (*. feature*) に直接追加するには、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint オブジェクトモデルメソッドを呼び出し <xref:Microsoft.VisualStudio.SharePoint.Features.IPropertyCollection.Add%2A> ます。 この方法を使用する場合は、機能プロパティに同一の特徴プロパティ値を追加する場合と同じルールが、機能ファイルに直接追加されたプロパティにも適用されることに注意してください。

## <a name="feature-receiver"></a>フィーチャーレシーバー
 フィーチャーレシーバーは、プロジェクト項目の含まれている機能に対して特定のイベントが発生したときに実行されるコードです。 たとえば、機能をインストール、アクティブ化、またはアップグレードしたときに実行されるフィーチャーレシーバーを定義できます。 フィーチャーレシーバーを追加する方法の1つは、「 [チュートリアル: フィーチャーイベントレシーバーの追加](../sharepoint/walkthrough-add-feature-event-receivers.md)」の説明に従ってフィーチャーに直接追加することです。 もう1つの方法は、フィーチャーレシーバークラスの名前とアセンブリを **フィーチャーレシーバー** プロパティで参照することです。

### <a name="direct-method"></a>ダイレクト メソッド
 フィーチャーレシーバーを機能に直接追加すると、コードファイルはソリューションエクスプローラーの **機能** ノードの下に配置されます。 SharePoint ソリューションをビルドすると、コードがアセンブリにコンパイルされ、SharePoint に配置されます。 既定では、機能プロパティの [ **受信者アセンブリ** ] および [ **受信者] クラス** は、クラス名とアセンブリを参照します。

### <a name="reference-method"></a>Reference メソッド
 フィーチャーレシーバーを追加するもう1つの方法は、プロジェクト項目の " **フィーチャーレシーバー** " プロパティを使用してフィーチャーレシーバーアセンブリを参照することです。 フィーチャーレシーバープロパティ値には、**アセンブリ****名とクラス名** という2つのサブプロパティがあります。 アセンブリは、完全修飾名である "厳密な" 名前を使用する必要があり、クラス名は完全な型名である必要があります。 詳細については、「[厳密な名前付きアセンブリ](/previous-versions/dotnet/netframework-4.0/wd40t7ad(v=vs.100))」を参照してください。 ソリューションを SharePoint に配置した後、この機能は参照されている機能の受信者を使用して機能イベントを処理します。

 ソリューションのビルド時に、フィーチャーとそのプロジェクトのフィーチャーレシーバープロパティの値が結合され、SharePoint ソリューション (*.wsp*) ファイルのフィーチャーマニフェスト内のフィーチャー要素の receiverassembly 属性と receiverassembly 属性が設定されます。 したがって、プロジェクト項目とフィーチャーのアセンブリ名とクラス名プロパティの値が両方とも指定されている場合は、プロジェクト項目とフィーチャーのプロパティ値が一致する必要があります。 値が一致しない場合は、検証エラーが表示されます。 機能で使用されているものとは異なるフィーチャーレシーバーアセンブリを参照するプロジェクト項目が必要な場合は、別の機能に移動します。

 サーバー上にまだ存在しないフィーチャーレシーバーアセンブリを参照する場合は、アセンブリファイル自体をパッケージに含める必要もあります。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ユーザーには追加しません。 この機能を配置すると、アセンブリファイルは、 [!INCLUDE[TLA#tla_gac](../sharepoint/includes/tlasharptla-gac-md.md)] SharePoint 物理ディレクトリ内のシステムまたは Bin フォルダーにコピーされます。 詳細については、「方法: 追加の [アセンブリを追加および削除](../sharepoint/how-to-add-and-remove-additional-assemblies.md)する」を参照してください。

 機能レシーバーの詳細については、「 [機能イベントレシーバー](/previous-versions/office/developer/sharepoint-2007/bb862634(v=office.12)) と [機能イベント](/previous-versions/office/developer/sharepoint-2010/ms469501(v=office.14))」を参照してください。

## <a name="project-output-references"></a>プロジェクト出力参照
 "プロジェクト出力参照" プロパティは、プロジェクト項目の実行に必要な依存関係 (アセンブリなど) を指定します。 たとえば、ソリューションに BDC プロジェクトとクラスプロジェクトがあるとします。 BDC プロジェクトに、クラスプロジェクトによって出力されるアセンブリに対する依存関係がある場合は、BDC プロジェクトの "プロジェクト出力参照" プロパティでアセンブリを参照できます。 BDC プロジェクトをパッケージ化すると、依存アセンブリがパッケージに含まれます。

 通常、プロジェクト出力参照はアセンブリですが、場合によっては、他の種類のファイルにすることもできます。

 詳細については、「 [方法: プロジェクト出力参照を追加](../sharepoint/how-to-add-a-project-output-reference.md)する」を参照してください。

## <a name="safe-control-entries"></a>安全なコントロールエントリ
 SharePoint には、信頼されていないユーザーのアクセスを特定のコントロールに制限する安全なコントロールエントリと呼ばれるセキュリティメカニズムが用意されています。 仕様により、SharePoint では、信頼されていないユーザーが SharePoint サーバーに ASPX ページをアップロードして作成できます。 これらのユーザーが安全でないコードを ASPX ページに追加できないようにするため、SharePoint では *安全なコントロール* へのアクセスが制限されています。 安全なコントロールとは、セキュリティで保護された ASPX コントロールと Web パーツであり、サイト上のどのユーザーでも使用できます。 詳細については、「 [手順 4: Web パーツをセーフコントロールリストに追加する](/previous-versions/office/developer/sharepoint-2007/ms581321(v=office.12))」を参照してください。

 内のすべての SharePoint プロジェクトアイテム [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、"安全" と "**スクリプトに対して安全**" の2つのブール値サブプロパティを持つ [**セーフコントロールエントリ**] というプロパティがあり **ます**。 Safe プロパティは、信頼されていないユーザーがコントロールにアクセスできるかどうかを指定します。 "スクリプトに対して安全" プロパティは、信頼されていないユーザーがコントロールのプロパティを表示および変更できるかどうかを指定します。

 安全なコントロールエントリは、アセンブリごとに参照されます。 プロジェクトのアセンブリに安全なコントロールエントリを追加するには、プロジェクト項目の " **安全なコントロールエントリ** " プロパティに入力します。 ただし、パッケージ **デザイナー** の **[詳細設定**] タブでパッケージにアセンブリを追加すると、プロジェクトのアセンブリに安全なコントロールエントリを追加することもできます。 詳細については、「 [方法: コントロールを安全なコントロールとしてマーク](../sharepoint/how-to-mark-controls-as-safe-controls.md) する」または「 [Web パーツアセンブリをセーフコントロールとして登録](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))する」を参照してください。

### <a name="xml-entries-for-safe-controls"></a>安全なコントロールのための XML エントリ
 安全なコントロールエントリをプロジェクト項目またはプロジェクトのアセンブリに追加すると、参照は次の形式でパッケージマニフェストに書き込まれます。

```xml
<Assemblies>
    <Assembly Location="<assembly name>.dll"
      DeploymentTarget="<'GlobalAssemblyCache' or 'WebApplication'">>
        <SafeControls>
            <SafeControl Assembly="<assembly name>.dll" Namespace=
              "<SharePoint project name>" Safe="<true/false>"
                TypeName="<control name>"
                SafeAgainstScript="<true/false>" />
        </SafeControls>
    </Assembly>
</Assemblies>
```

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
