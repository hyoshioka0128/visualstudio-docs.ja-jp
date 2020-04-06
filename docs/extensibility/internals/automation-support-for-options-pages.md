---
title: オプション ページのオートメーションサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe45238948d5b4cdebbf9f002f6b242515e7622e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709932"
---
# <a name="automation-support-for-options-pages"></a>オプション ページのオートメーション サポート
VSPackages は、カスタム**オプション**ダイアログ ボックスを [ツール][!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]メニュー **([ツール****オプション**] ページ) に提供し、オートメーション モデルで使用できるようにします。

## <a name="tools-options-pages"></a>[ツール] メニューの [オプション] ページ
 **ツール オプション**ページを作成するには、VSPackage は、VSPackage のメソッドの実装を通じて環境に返されるユーザー<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>コントロールの実装を提供する必要があります。 (または、マネージ コードの<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>場合は、メソッド)。

 これはオプションですが、自動化モデルを通じてこの新しいページにアクセスできるように強くお勧めします。 次の手順で行うことができます。

1. IDispatch<xref:EnvDTE._DTE.Properties%2A>派生オブジェクトの実装を使用してオブジェクトを拡張します。

2. メソッドの実装 (<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>またはメソッドの<xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A>マネージ コード) を IDispatch 派生オブジェクトに返します。

3. オートメーション コンシューマがカスタムの<xref:EnvDTE._DTE.Properties%2A> **Option**プロパティ ページでメソッドを呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>すと、環境はメソッドを使用して、カスタム**ツール オプション**ページのオートメーション実装を取得します。

4. VSPackage のオートメーション オブジェクトを使用して、 によって<xref:EnvDTE.Property>返される<xref:EnvDTE._DTE.Properties%2A>各オブジェクトを提供します。

   カスタム**ツール オプション**ページを実装するサンプルについては、「 [VSSDK のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト オブジェクトを公開する](../../extensibility/internals/exposing-project-objects.md)
