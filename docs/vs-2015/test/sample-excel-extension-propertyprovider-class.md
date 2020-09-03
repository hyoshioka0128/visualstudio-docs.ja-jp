---
title: 'Excel 拡張機能のサンプル: PropertyProvider クラス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 075d9b8d-8658-4fca-8711-08304dbac1c5
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8ae254f85b00c47ba00250641f7afe0a638ceabc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660421"
---
# <a name="sample-excel-extension-propertyprovider-class"></a>Excel 拡張子のサンプル: PropertyProvider クラス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この内部クラスによって <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> クラスが拡張されます。また、この内部クラスは、ユーザー インターフェイス (UI) テストの記録と再生に使用する [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 要素のプロパティ サービスを提供します。

## <a name="getcontrolsupportlevel-method"></a>GetControlSupportLevel メソッド
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A> メソッドは、指定されたコントロールに対してプロパティ プロバイダーが提供できるサポート レベルを示す数値を返します。 戻り値が大きくなるほど、コントロールに対するプロパティ プロバイダーのサポート レベルは高くなります。 このメソッドの例では、指定されたコントロールの <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IUITechnologyElement.TechnologyName%2A> プロパティの値が確認されます。 値が "Excel" で、<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IUITechnologyElement.ControlTypeName%2A> が `CellElement` であると指定されている場合、メソッドからは最も高い値が返されます。それ以外の場合はゼロが返されます。これは、サポートが提供されていないことを示します。

## <a name="getpropertynames-method"></a>GetPropertyNames メソッド
 Excel Cell コントロールのサポートされているプロパティに関して、プロパティ名とプロパティ記述子のディクショナリを返します。

## <a name="getpropertydescriptor-method"></a>GetPropertyDescriptor メソッド
 このメソッドは、指定されたプロパティ名の定義済みプロパティ記述子を取得するために、テスト フレームワークによって呼び出されます。

## <a name="getpropertyvalue-and-setpropertyvalue-methods"></a>GetPropertyValue メソッドと SetPropertyValue メソッド
 `GetPropertyValue` メソッドはこの拡張機能の `Communicator` クラスを使用して Excel のプロパティ値を返します。 `SetPropertyValue` メソッドは <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard> クラスと `Communicator` コンポーネントを使用してプロパティ値を設定しています。 これらのメソッドはテスト フレームワークによって呼び出されます。

## <a name="code-generation-customization-methods"></a>コード生成カスタマイズ メソッド
 この拡張機能でこれらのメソッドは実装されていません。 そのため、`null` が返されるか、<xref:System.NotImplementedException> がスローされます。

## <a name="see-also"></a>参照
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard>
 [コード化された UI テストと操作の記録を拡張して Microsoft Exce をサポート](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)
