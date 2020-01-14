---
title: オプションページのオートメーションサポート |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03360bfc01110e7b4ef73956f0199aaaed9cee2c
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848963"
---
# <a name="automation-support-for-options-pages"></a>オプションページのオートメーションサポート
Vspackage では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[ツール]** メニュー ( **[ツール]** オプション ページ) にカスタム**オプション**のダイアログボックスを用意して、オートメーションモデルで使用できるようにすることができます。

## <a name="tools-options-pages"></a>[ツール] メニューの [オプション] ページ
 **ツールオプション**ページを作成するには、VSPackage メソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> の VSPackage の実装を使用して、環境に返されるユーザーコントロールの実装を提供する必要があります。 (または、マネージコードの場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> メソッドです)。

 これは省略可能ですが、オートメーションモデルを通じてこの新しいページにアクセスできるようにすることを強くお勧めします。 そのためには、次の手順を実行します。

1. IDispatch から派生したオブジェクトの実装を通じて <xref:EnvDTE._DTE.Properties%2A> オブジェクトを拡張します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> メソッドの実装 (または、<xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> メソッドのマネージコード) を IDispatch 派生オブジェクトに返します。

3. オートメーションコンシューマーがカスタム**オプション**プロパティページで <xref:EnvDTE._DTE.Properties%2A> メソッドを呼び出すと、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> メソッドを使用して、カスタム**ツールオプション**ページのオートメーション実装を取得します。

4. 次に、VSPackage のオートメーションオブジェクトを使用して、<xref:EnvDTE._DTE.Properties%2A>によって返される各 <xref:EnvDTE.Property> を指定します。

   カスタム**ツールオプション**ページを実装するサンプルについては、「 [vssdk のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクトオブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)
