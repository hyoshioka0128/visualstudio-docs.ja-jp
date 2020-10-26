---
title: 'CA2210: アセンブリには有効な厳密な名前 | が必要です。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8f800a550717abfabdfb9296fc8f6de49d127d73
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548201"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210:アセンブリには有効な厳密な名前が必要です
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 アセンブリが厳密な名前で署名されていないか、厳密な名前を確認できなかったか、またはコンピューターの現在のレジストリ設定がないと厳密な名前が有効ではありません。

## <a name="rule-description"></a>ルールの説明
 このルールは、アセンブリの厳密な名前を取得して検証します。 次のいずれかに該当する場合は、違反が発生します。

- アセンブリに厳密な名前がありません。

- 署名後にアセンブリが変更されました。

- アセンブリは遅延署名されています。

- アセンブリが正しく署名されていないか、署名に失敗しました。

- アセンブリには、検証に合格するためのレジストリ設定が必要です。 たとえば、厳密名ツール (Sn.exe) は、アセンブリの検証をスキップするために使用されていました。

  厳密な名前によって、改ざんされたアセンブリを、クライアントが無意識のうちに読み込む問題を防ぐことができます。 厳密な名前のないアセンブリが配置される状況は、限定されます。 適切に署名されていないアセンブリを共有または配布すると、アセンブリが改ざんされる場合、共通言語ランタイムでアセンブリを読み込むことができない場合、またはユーザーのコンピューターで検証を無効にする必要がある場合などの問題が考えられます。 厳密な名前を持たないアセンブリには、次のような欠点があります。

- そのオリジンを検証できません。

- 共通言語ランタイムは、アセンブリの内容が変更されている場合、ユーザーに警告することはできません。

- グローバルアセンブリキャッシュに読み込むことはできません。

  遅延署名されたアセンブリを読み込んで分析するには、アセンブリの検証を無効にする必要があることに注意してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 **キーファイルを作成するには**

 次の手順のいずれかを使用します。

- SDK によって提供されるアセンブリリンカーツール (Al.exe) を使用し [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。

- V1.0 または v1.1 では、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] または属性のいずれかを使用し <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName> ます。

- で [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] `/keyfile` は、または `/keycontainer` コンパイラオプション [/Keyfile (アセンブリに署名するためのキーまたはキーペアの指定)](https://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06) または [/KEYCONTAINER (アセンブリに署名するためのキーコンテナーの指定)](https://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e) リンカーオプションを C++ で使用します。

  **Visual Studio で厳密な名前を使用してアセンブリに署名するには**

1. で [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、ソリューションを開きます。

2. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[プロパティ] をクリックし**ます。**

3. [ **署名** ] タブをクリックし、[ **アセンブリの署名** ] チェックボックスをオンにします。

4. **[厳密な名前のキーファイルを選択**してください] で、[**新規**] を選択します。

    [ **厳密な名前キーの作成** ] ウィンドウが表示されます。

5. [ **キーファイル名**] に、厳密な名前のキーの名前を入力します。

6. パスワードを使用してキーを保護するかどうかを選択し、[ **OK]** をクリックします。

7. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[**ビルド**] をクリックします。

   **Visual Studio の外部でアセンブリに厳密な名前で署名するには**

- SDK によって提供される厳密な名前ツール (Sn.exe) を使用し [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。 詳細については、「 [Sn.exe (厳密名ツール)](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)」を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 コンテンツの改ざんが心配でない環境でアセンブリが使用されている場合にのみ、この規則の警告を非表示にします。

## <a name="see-also"></a>参照
 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
 [方法: 厳密な名前でアセンブリに署名](https://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67)する [Sn.exe (厳密名ツール)](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)
