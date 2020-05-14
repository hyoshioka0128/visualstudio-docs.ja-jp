---
title: Web サイトのサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 22047ad1b0709cefa200656e61f8e0d39ace94c9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703441"
---
# <a name="web-site-support"></a>Web サイト サポート
Web サイト プロジェクト システムは、Web プロジェクトを作成するプロジェクト システムです。 Web プロジェクトは、次に Web アプリケーションを作成します。 Web サイト プロジェクトでは、関連付けられたコードを持つ Web ページごとに 1 つの実行可能ファイルが生成されます。 追加の実行可能ファイルは、/App_Code フォルダー内のソース コード ファイルから生成されます。

 Web サイト プロジェクト システムは、既存のプロジェクト システムにテンプレートと登録属性を追加することによって作成されます。 これらの属性の 1 つは、言語の IntelliSense プロバイダーを選択します。 IntelliSense プロバイダーの実装は、参照を処理し、キャッシュされていないスマート Web ページが要求されたときに言語コンパイラを呼び出します。

 Web ページのコンパイルに使用する言語コンパイラは、[!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]に登録する必要があります。 次の例に[\<示すように、コンパイラ>要素](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element)を Web.config ファイルで使用してコンパイラを登録できます。

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>このセクションの内容
- [Web サイト サポートのテンプレート](../../extensibility/internals/web-site-support-templates.md)

 新しい Web サイト プロジェクトおよび関連するアイテムを作成するために使用できるテンプレートの一覧が表示されます。

- [Web サイト サポートの属性](../../extensibility/internals/web-site-support-attributes.md)

 Web サイト プロジェクトを 接続する登録属性[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を[!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]表示し、 .

## <a name="related-sections"></a>関連項目
- [Web プロジェクト](../../extensibility/internals/web-projects.md)

 Web サイト プロジェクトと Web アプリケーション プロジェクトの 2 種類の Web プロジェクトの概要を示します。
