---
title: Web サイトのサポート属性 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef75f99480145475278357a552f3ac74c0289800
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703497"
---
# <a name="web-site-support-attributes"></a>Web サイト サポートの属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]Web サイト プロジェクトを拡張して、Web プログラミング言語のサポートを提供できます。 言語を選択したときにプロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]テンプレートを [**新しい Web サイト**] ダイアログ ボックスに表示できるように、言語は に登録する必要があります。

IronPython スタジオのサンプルには、Web サイトのサポートが含まれています。 このサンプルには、新しい Web プロジェクトの分離コード言語として IronPython を登録するための次の属性クラスが含まれています。

## <a name="websiteprojectattribute"></a>サイトプロジェクト属性
 この属性は、言語プロジェクトに配置されます。 [**新しい**Web サイト] ダイアログ ボックスの [言語] ボックスの一覧で **、Web**プログラミング言語の一覧に言語が追加されます。 たとえば、次のコードは、リストに IronPython を追加します。

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 この属性は、テンプレート フォルダーを指すテンプレート パスも設定します。 テンプレート フォルダの場所の詳細については、「 Web[サイト サポート テンプレート](../../extensibility/internals/web-site-support-templates.md)」を参照してください。

## <a name="websiteprojectrelatedfilesattribute"></a>Web サイト プロジェクト関連ファイル属性
 この属性は、言語プロジェクトに配置されます。 Web サイト プロジェクトは、ソリューション エクスプローラで、あるファイルの種類 (関連) を別のファイルの種類 (プライマリ) の下に入れ子**にできます**。

 たとえば、次のコードは、IronPython の分離コード ファイルが .aspx ファイルに関連付けられていることを指定します。 新しい .aspx Web ページが IronPython Web サイト ソリューションで作成されると、新しい .py ソース ファイルが生成され、.aspx ページの子ノードとして表示されます。

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>アプロビティ・インテリセンス・プロバイダー属性
 この属性は、言語プロジェクト パッケージに配置されます。 言語の IntelliSense プロバイダーを選択します。

 たとえば、次のコードでは、言語サービスを提供するためにオンデマンドで<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>を実装する PythonIntellisenseProvider のインスタンスを作成するように指定しています。

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 IVsIntellisenseProject 実装は、参照を処理し、コードを含む Web ページが要求されたがキャッシュされていない場合に言語コンパイラを呼び出します。

## <a name="see-also"></a>関連項目
- [Web サイト サポート](../../extensibility/internals/web-site-support.md)
