---
title: Web サイトのサポート |Microsoft Docs
description: 既存のプロジェクトシステムにテンプレートと登録属性を追加することによって作成される web サイトプロジェクトシステムについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16de0fdc2c4e65dfe6c2ae2c6dc3cdc6902fa8b0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069115"
---
# <a name="web-site-support"></a>Web サイト サポート
Web サイトプロジェクトシステムは、Web プロジェクトを作成するプロジェクトシステムです。 Web プロジェクトは、Web アプリケーションを作成します。 Web サイトプロジェクトは、コードが関連付けられている Web ページごとに1つの実行可能ファイルを生成します。 /App_Code フォルダー内のソースコードファイルから、追加の実行可能ファイルが生成されます。

 Web サイトプロジェクトシステムは、既存のプロジェクトシステムにテンプレートと登録属性を追加することによって作成されます。 これらの属性のいずれかによって、言語の IntelliSense プロバイダーが選択されます。 IntelliSense プロバイダーの実装は、キャッシュされていないスマート Web ページが要求されたときに、参照を処理し、言語コンパイラを呼び出します。

 Web ページのコンパイルに使用される言語コンパイラは、に登録されている必要があり [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] ます。 次の例に示すように、Web.config ファイルで[ \<compiler> 要素](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element)を使用して、コンパイラを登録できます。

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>このセクションの内容
- [Web サイト サポートのテンプレート](../../extensibility/internals/web-site-support-templates.md)

 新しい Web サイトプロジェクトと関連アイテムを作成するために使用できるテンプレートの一覧を示します。

- [Web サイト サポートの属性](../../extensibility/internals/web-site-support-attributes.md)

 Web サイトプロジェクトをとに接続する登録属性を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 示し [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] ます。

## <a name="related-sections"></a>関連項目
- [Web プロジェクト](../../extensibility/internals/web-projects.md)

 2種類の Web プロジェクト、Web サイトプロジェクト、および Web アプリケーションプロジェクトの概要について説明します。
