---
title: VSIX パッケージのローカライズ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6143b21884bc92ac79ae0fd7292a11780fec4478
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841581"
---
# <a name="localizing-vsix-packages"></a>VSIX パッケージのローカライズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

各ターゲット言語の vsixlangpack ファイルを作成し、適切なフォルダーに配置することによって、VSIX パッケージをローカライズできます。 ローカライズされたパッケージをインストールすると、拡張機能のローカライズされた名前がローカライズされた説明と共に表示されます。 ローカライズされたライセンスファイル、またはローカライズされた情報を示す URL を指定すると、それらも表示されます。  
  
 VSIX パッケージに、メニューコマンドやその他の UI を追加する VSPackage が含まれている場合は、「 [メニューコマンドのローカライズ](../extensibility/localizing-menu-commands.md) 」で新しい ui 要素のローカライズについての情報を参照してください。  
  
## <a name="directory-structure"></a>ディレクトリの構造  
 ユーザーが拡張機能をインストールすると、 **拡張機能と更新プログラム** によって、ターゲットコンピューターの Visual Studio ロケールに一致する名前を持つフォルダーの VSIX パッケージの最上位レベルがチェックされます。 **拡張機能と更新プログラム**によってフォルダー内の vsixlangpack ファイルが検出されると、そのファイル内のローカライズされた値が、source.extension.vsixmanifest ファイル内の対応する値に置き換えられます。 これらの値は、拡張機能をインストールするときに表示されます。 次の例は、スペイン語 (es) とフランス語 (fr-fr) にローカライズされた VSIX パッケージのディレクトリ構造を示しています。  
  
 MyExtension.dll  
  
 拡張子 source.extension.vsixmanifest  
  
 [Content_Types] .xml  
  
 es-ES  
  
 拡張子 vsixlangpack  
  
 fr-FR  
  
 拡張子 vsixlangpack  
  
> [!NOTE]
> Vsix でサポートされているプロジェクトテンプレートでは、 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] vsix マニフェストを生成し、それに source.extension.vsixmanifest という名前を指定します。 Visual Studio によってプロジェクトがビルドされると、そのファイルの内容が VSIX パッケージの Source.extension.vsixmanifest にコピーされます。  
  
## <a name="the-extensionvsixlangpack-file"></a>Vsixlangpack ファイル  
 Vsixlangpack ファイルは、 [VSIX 言語パックのスキーマ](../extensibility/vsx-language-pack-schema-reference.md)に従います。 このスキーマには、 [VSIXLanguagePack](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md) ルート要素と、 [LocalizedName](../extensibility/localizedname-element-vsix-language-pack-schema.md)、 [LocalizedDescription](../extensibility/localizeddescription-element-vsix-language-pack-schema.md)、 [MoreInfoURL](../extensibility/moreinfourl-element-vsix-language-pack-schema.md)、 [License](../extensibility/license-element-vsix-language-pack-schema.md)の4つの子要素があります。 これらの子要素は `Name` 、 `Description` `MoreInfoURL` `License` source.extension.vsixmanifest ファイルの要素の、、、およびの各子要素に対応し `Identifier` ます。  
  
 Vsixlangpack ファイルを作成する場合は、プロパティをに設定する必要があり `Include in Vsix` `true` ます。 それ以外の場合、ローカライズされたインストールテキストは無視されます。  
  
#### <a name="to-set-the-include-in-vsix-property"></a>[Vsix に含める (Vsix に含める) プロパティを設定するには  
  
1. **ソリューションエクスプローラー**で、vsixlangpack ファイルを右クリックし、[**プロパティ**] をクリックします。  
  
2. プロパティグリッドで、[ **Vsix に含める**] をクリックし、値をに設定し `true` ます。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、source.extension.vsixmanifest ファイルの関連部分を、スペイン語用の対応する vsixlangpack ファイルと共に示します。 ターゲットコンピューターの Visual Studio ロケールがスペイン語に設定されている場合は、言語パックの値によってマニフェストの値が置き換えられます。  
  
### <a name="code"></a>コード  
 [Source.extension.vsixmanifest]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VSIX ...>  
  <Identifier ...>  
    <Name>Family Tree</Name>  
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>  
    <License>EULA.rtf</License>  
    <MoreInfoURL>http://www.contoso.com/products/FamilyTree.htm</MoreInfoURL>  
    ...  
  </Identifier>  
  <References .../>  
  <Content .../>  
</VSIX>  
```  
  
 [Vsixlangpack]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VsixLanguagePack Version="1.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema-lp/2010">  
  <LocalizedName>Arbol de Familia</LocalizedName>  
  <LocalizedDescription> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</LocalizedDescription>  
  <License>es\Eula.rtf</License>  
  <MoreInfoUrl> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfoUrl>  
</VsixLanguagePack>  
```  
  
## <a name="see-also"></a>参照  
 [VSIX LanguagePack 要素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)   
 [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)   
 [VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)
