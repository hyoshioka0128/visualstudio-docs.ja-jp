---
title: フィーチャーマニフェストとパッケージマニフェストの XML のマージ |Microsoft Docs
description: SharePoint のフィーチャーマニフェストとパッケージマニフェストに、デザイナーによって生成された、ユーザーが追加した XML コードをマージします。 フィーチャーマニフェストとパッケージマニフェストの要素とマージ例外について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 16305ed63f48d9f14e35aeb8d37e35f23f40be25
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304231"
---
# <a name="merge-xml-in-feature-and-package-manifests"></a>フィーチャーマニフェストとパッケージマニフェストの XML のマージ
  フィーチャーとパッケージは、マニフェストファイルによって定義され [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。 これらのパッケージマニフェストは、デザイナーから生成されたデータと、 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ユーザーによってマニフェストテンプレートに入力されたカスタムデータの組み合わせです。 パッケージ化時に、は、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] パッケージ化された [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] マニフェストファイルを形成するために用意されているカスタムステートメントとデザイナーをマージし [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。 同様の要素は、後の「マージ例外」で説明されている例外を使用してマージされ、 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] SharePoint にファイルを配置した後に検証エラーが発生しないようにし、マニフェストファイルを小さく、効率的にします。

## <a name="modify-the-manifests"></a>マニフェストを変更する
 パッケージマニフェストファイルは、機能またはパッケージデザイナーを無効にするまで、直接変更することはできません。 ただし、 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 機能およびパッケージデザイナーまたはエディターを使用して、カスタム要素をマニフェストテンプレートに手動で追加することができ [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。 詳細については、「 [方法: Sharepoint 機能をカスタマイズ](../sharepoint/how-to-customize-a-sharepoint-feature.md) する」および「 [方法: sharepoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)」を参照してください。

## <a name="feature-and-package-manifest-merge-process"></a>機能とパッケージのマニフェストのマージプロセス
 カスタム要素とデザイナーで提供される要素を組み合わせる場合、で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は次のプロセスを使用します。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 各要素に一意のキー値があるかどうかを確認します。 要素に一意のキー値がない場合は、パッケージマニフェストファイルに追加されます。 同様に、複数のキーを持つ要素をマージすることはできません。 そのため、マニフェストファイルに追加されます。

 要素に一意のキーがある場合、は [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーとカスタムキーの値を比較します。 値が一致する場合は、1つの値にマージされます。 値が異なる場合、デザイナーのキー値は破棄され、カスタムキー値が使用されます。 コレクションもマージされます。 たとえば、デザイナーで生成された [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] とカスタムの [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 両方にアセンブリコレクションが含まれている場合、パッケージ化されたマニフェストにはアセンブリコレクションが1つだけ含まれます。

## <a name="merge-exceptions"></a>例外のマージ
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 、一意の識別属性が1つしかない限り、ほとんどのデザイナー要素を類似したカスタム要素とマージします。 ただし、マージに必要な一意の識別子を持たない要素もあり [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。 これらの要素は *マージ例外* と呼ばれます。 このような場合、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は、カスタム要素とデザイナーで提供される要素をマージせずに、 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] パッケージマニフェストファイルに追加します。

 フィーチャーマニフェストファイルとパッケージマニフェストファイルのマージ例外の一覧を次に示し [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。

|デザイナー|XML 要素|
|--------------|-----------------|
|フィーチャーデザイナー|ActivationDependency|
|フィーチャーデザイナー|UpgradeAction|
|パッケージデザイナー|SafeControl|
|パッケージデザイナー|CodeAccessSecurity|

## <a name="feature-manifest-elements"></a>フィーチャーマニフェストの要素
 次の表に、マージ可能なすべてのフィーチャーマニフェスト要素と、一致に使用される一意のキーの一覧を示します。

|要素名|一意キー|
|------------------|----------------|
|機能 (すべての属性)|*属性名* (フィーチャー要素の各属性名は一意のキーです)。|
|ElementFile|場所|
|ElementManifests/Elementmanifests|場所|
|プロパティ/プロパティ|Key|
|CustomUpgradeAction|名前|
|CustomUpgradeActionParameter|名前|

> [!NOTE]
> CustomUpgradeAction 要素を変更する唯一の方法はカスタムエディターであるため [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 、マージしない場合の効果は低くなります。

## <a name="package-manifest-elements"></a>パッケージマニフェスト要素
 次の表に、マージ可能なすべてのパッケージマニフェスト要素と、一致に使用される一意のキーの一覧を示します。

|要素名|一意キー|
|------------------|----------------|
|ソリューション (すべての属性)|*属性名* (ソリューション要素の各属性名は一意のキーです)。|
|ApplicationResourceFiles/ApplicationResourceFile|場所|
|アセンブリ/アセンブリ|場所|
|ClassResources/Classresources|場所|
|DwpFiles/Dwpfiles|場所|
|FeatureManifests/Featuremanifests|場所|
|リソース/リソース|場所|
|RootFiles/Rootfiles|場所|
|SiteDefinitionManifests/Sitedefinitionmanifests|場所|
|WebTempFile|場所|
|TemplateFiles/TemplateFile|場所|
|SolutionDependency|SolutionID|

## <a name="manually-add-deployed-files"></a>展開されたファイルを手動で追加する
 ApplicationResourceFile や DwpFiles などのマニフェスト要素の中には、ファイル名を含む場所を指定するものがあります。 ただし、マニフェストテンプレートにファイル名のエントリを追加しても、基になるファイルはパッケージに追加されません。 このファイルをパッケージに含めるには、ファイルをプロジェクトに追加し、その展開の種類のプロパティを適宜設定する必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
