---
title: プロジェクトの拡張に通常使用されるオブジェクトの Catid
description: Visual Basic、Visual C#、Visual C++ プロジェクトのプロジェクトと ProjectItem オートメーションオブジェクトを拡張するために使用されるオブジェクトの Catid について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, CATIDs
- GUIDs, VSPackages
- CATIDs for VSPackages
ms.assetid: 0c7fdb66-ed96-4b36-89f6-021bca573572
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bebaf35fc19cbad86a1e1ee4c8bbeddef0259cb4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99905876"
---
# <a name="catids-for-objects-that-are-typically-used-to-extend-projects"></a>プロジェクトの拡張に通常使用されるオブジェクトの Catid
次の表に、 `Project` `ProjectItem` 、、およびの各プロジェクトのオブジェクトを拡張するために使用される catid の一覧を示し [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ます。 これらの Catid は、 *VSLangProj* で定義されています。

## <a name="listing-of-catids"></a>Catid の一覧

|名前|GUID|
|----------|----------|
|<xref:VSLangProj.PrjCATID.prjCATIDProject>|{610D4614-D0D5-11D2-8599-006097C68E81}|
|<xref:VSLangProj.PrjCATID.prjCATIDProjectItem>|{610D4615-D0D5-11D2-8599-006097C68E81}|

## <a name="visual-basic-catids"></a>Visual Basic Catid
 次の表に、参照オブジェクトを拡張するために使用される Catid の一覧を示し [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ます。 これらはすべて、 *VSLangProj* で定義されています。

|名前|GUID|
|----------|----------|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectBrowseObject>|{E0FDC879-C32A-4751-A3D3-0B3824BD575F}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectConfigBrowseObject>|{67F8DD11-14EB-489b-87F0-F01C52AF3870}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFileBrowseObject>|{EA5BD05D-3C72-40A5-95A0-28A2773311CA}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFolderBrowseObject>|{932DC619-2EAA-4192-B7E6-3D15AD31DF49}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBReferenceBrowseObject>|{2289B812-8191-4e81-B7B3-174045AB0CB5}|

## <a name="visual-c-catids"></a>Visual C# catid
 次の Catid を使用して、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 参照オブジェクトを拡張できます。 これらはすべて、 *VSLangProj* で定義されています。

|名前|GUID|
|----------|----------|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectBrowseObject>|{4EF9F003-DE95-4d60-96B0-212979F2A857}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectConfigBrowseObject>|{A12CE10A-227F-4963-ADB6-3A43388513CA}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFileBrowseObject>|{8D58E6AF-ED4E-48B0-8C7B-C74EF0735451}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFolderBrowseObject>|{914FE278-054A45BF9E-5F22484 CC84 C}|
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpReferenceBrowseObject>|{2F0FA3B8-C855-4a4e-95A5-CB45C67D6C27}|

## <a name="c-catids"></a>C++ Catid
 次の [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトシステム catid は、.net 2003 のタイプライブラリで公開されていません。これらのプロジェクトオブジェクトを拡張する場合は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必ずコードに含める必要があります。 これらの Catid は、の今後のリリースでタイプライブラリに含まれる予定 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] です。

|名前|GUID|
|----------|----------|
|`CVCProjectNode`|{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCFolderNode`|{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCFileNode`|{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|

 次のコード例は、コードでこれらの Catid をプログラミングする方法を示しています。

```
const LPOLESTR CVCProjectNode::s_wszCATID = L"{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCFolderNode::s_wszCATID = L"{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCFileNode::s_wszCATID = L"{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";
```

 次の [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] project System catid は、.net 2003 のタイプライブラリにも公開されていません。これらのプロジェクトオブジェクトを拡張する場合は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必ずコードに含める必要があります。 これらの Catid は .Net 2003 でのみ使用でき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、の今後のリリースでは使用できません [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

|名前|GUID|
|----------|----------|
|`CVCAssemblyReferenceNode`|{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|
|`CVCProjectReferenceNode`|{593DCFCE-20A7-48e4-ACA1-49ADE9049887}|
|`CVCActiveXReferenceNode`|{9E8182d3-c60a47 4F4-a74b14c90ef9cace}|
|`CVCReferences`|{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|

 次のコード例は、コードでこれらの Catid をプログラミングする方法を示しています。

```
const LPOLESTR CVCAssemblyReferenceNode::s_wszCATID = L"{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";
const LPOLESTR CVCProjectReferenceNode::s_wszCATID = L"{593DCFCE-20A7-48e4-ACA1-49ADE9049887}";
const LPOLESTR CVCActiveXReferenceNode::s_wszCATID = L"{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}";
const LPOLESTR CVCReferences::s_wszCATID = L"{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";
```

 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]次の表に、およびプロジェクトの種類の guid を [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 示します。

| プロジェクトの種類 | GUID |
| - | - |
| [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] | {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC} |
| [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] | {F184B08F-C81C-45F6-A57F-5ABD9991F28F} |

## <a name="see-also"></a>関連項目
- [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
