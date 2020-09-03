---
title: 'Excel 拡張子のサンプル: ExtensionPackage クラス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 6e45410a-1819-4d54-ac21-7280152f7e3a
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1c1f4c746fa505b50bab9caa7a516a2abc77f69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672211"
---
# <a name="sample-excel-extension-extensionpackage-class"></a>Excel 拡張子のサンプル: ExtensionPackage クラス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このクラスは <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> クラスを拡張し、[!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] ワークシートをテストするコード化された UI テストのエントリ ポイントになります。

## <a name="assembly-attribute"></a>アセンブリ属性
 ファイルは、アセンブリを UI テスト拡張として識別するアセンブリ属性で始まります。

```
[assembly: Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage(
    "ExcelExtensionPackage",
    typeof(
     Microsoft.VisualStudio.Test.Sample.UI.ExtensionPackage))]
```

 この属性は、基本クラス名、パッケージ クラスの名前、およびカスタム拡張パッケージ クラスの完全修飾クラス名を宣言します。

## <a name="simple-properties"></a>単純なプロパティ
 このクラスには、コード化された UI テスト フレームワークが拡張とアセンブリを識別および説明するために使用する値を提供するプロパティがあります。 詳細については、コードのコメントをご覧ください。

## <a name="getservice-method"></a>GetService メソッド
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> メソッドは、各オブジェクトの基底クラスによって識別され、コード化された UI テスト フレームワークがテクノロジ マネージャー、プロパティ プロバイダー、およびアクション フィルターにアクセスするために使用する単一エントリ ポイントです。

## <a name="see-also"></a>参照
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> [コード化された UI テストと操作の記録を拡張して Microsoft Exce をサポート](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)
