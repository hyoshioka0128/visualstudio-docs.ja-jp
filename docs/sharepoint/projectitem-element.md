---
title: ProjectItem 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 44fc1b918960f0268d916ccfa560f118cea47144
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85536878"
---
# <a name="projectitem-element"></a>ProjectItem 要素
  SharePoint プロジェクトアイテムを表します。 この要素は、 *sharepointprojectitem.spdata* ファイルの必須のルート要素です。

## <a name="syntax"></a>構文

```xml
<ProjectItem DefaultFile = "File that opens in the editor when you open the project item"
    FeatureReceiverClass = "Class that implements a feature receiver for the project item"
    FeatureReceiverAssembly = "Assembly that defines a feature receiver for the project item"
    SupportedTrustLevels = "Trust levels that the project item supports"
    SupportedDeploymentScopes = "Deployment scopes that the project item supports"
    Type="Identifier for the project item">
  <Files>...</Files>
  <ProjectItemFolder>...</ProjectItemFolder>
  <SafeControls>...</SafeControls>
  <FeatureProperties>...</FeatureProperties>
  <ExtensionData>...</ExtensionData>
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**DefaultFile**|**Xs: string**属性 (省略可能)。<br /><br /> **ソリューションエクスプローラー**で SharePoint プロジェクト項目を開いたときに Visual Studio エディターで開くファイルの相対パス (ファイル名を含む)。 パスは、 *sharepointprojectitem.spdata* ファイルを含むフォルダーからの相対パスです。|
|**FeatureReceiverClass**|**Xs: string**属性 (省略可能)。<br /><br /> この SharePoint プロジェクトアイテムのフィーチャーレシーバークラスの完全修飾名。 フィーチャーレシーバーの詳細については、「 [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。|
|**FeatureReceiverAssembly**|**Xs: string**属性 (省略可能)。<br /><br /> この SharePoint プロジェクトアイテムのフィーチャーレシーバーを定義するアセンブリの完全修飾名を指定します。 フィーチャーレシーバーの詳細については、「 [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。 完全修飾アセンブリ名の詳細については、「 [アセンブリ名](/dotnet/framework/app-domains/assembly-names)」を参照してください。|
|**SupportedTrustLevels**|**Xs: string**属性 (省略可能)。<br /><br /> この SharePoint プロジェクト項目でサポートされる信頼レベルを指定します。 この値には、次の文字列のいずれかを指定できます: サンドボックス、FullTrust、またはすべて。 値 All は、サンドボックスと FullTrust の両方を指定します。<br /><br /> カスタム SharePoint プロジェクト項目の種類では、この属性の値は、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> メソッドの実装でプロパティに割り当てる値に対応し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> ます。 この属性に別の値を指定すると、Visual Studio は、プロパティで指定したのと同じ信頼レベルを指定するように値を上書きし <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> ます。|
|**SupportedDeploymentScopes**|**Xs: string**属性 (省略可能)。<br /><br /> この SharePoint プロジェクトアイテムがサポートする配置スコープを指定します。 この値は、ファーム、サイト、Web、WebApplication、またはパッケージの1つ以上の文字列で構成されるコンマ区切りの文字列です。 例: `Web, Site`<br /><br /> カスタム SharePoint プロジェクト項目の種類では、この属性の値は、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> メソッドの実装でプロパティに割り当てる値に対応し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> ます。 この属性に別の値を指定すると、Visual Studio は、プロパティで指定したのと同じ信頼レベルを指定するように値を上書きし <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> ます。|
|**Type**|**Xs: string**属性が必要です。<br /><br /> SharePoint プロジェクトアイテムの識別子。 カスタム SharePoint プロジェクト項目の種類では、識別子はに渡す文字列です <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 。 詳細については、「 [方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。<br /><br /> Visual Studio に含まれる組み込みの SharePoint プロジェクト項目の識別子の一覧については、「 [sharepoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|省略可能な要素です。<br /><br /> SharePoint プロジェクトアイテムに関連付けられているカスタムデータアイテムのコレクションを表します。<br /><br /> 1つの **Extensiondata** 要素だけを含めることができます。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|省略可能な要素です。<br /><br /> SharePoint に配置されるときにフィーチャーに含まれるプロパティ値のコレクションを表します。<br /><br /> **Featureproperties**要素を1つだけ含めることができます。|
|[[ファイル]](../sharepoint/files-element.md)|省略可能な **FileCollectionType** 要素。<br /><br /> SharePoint プロジェクトアイテムと共に配置するファイルを指定します。たとえば、フィーチャー要素ファイルや SharePoint 以外の依存プロジェクトの出力などです。<br /><br /> **ファイル**または**ProjectItemFolder**要素のいずれかを含めますが、両方を含めることはできません。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|省略可能な **ProjectItemFolderType** 要素。<br /><br /> マップされたフォルダーを表します。<br /><br /> **ファイル**または**ProjectItemFolder**要素のいずれかを含めますが、両方を含めることはできません。|
|[SafeControls](../sharepoint/safecontrols-element.md)|省略可能な要素です。<br /><br /> SharePoint サイトの任意の ASPX ページですべてのユーザーがアクセスできるようにセキュリティで保護されたものとして指定された ASPX コントロールおよび Web パーツのコレクションを表します。<br /><br /> **SafeControls**要素を1つだけ含めることができます。|

### <a name="parent-elements"></a>親要素
 なし。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
[SharePoint プロジェクト項目スキーマ rseference](../sharepoint/sharepoint-project-item-schema-reference.md)
