---
title: '方法: ドメイン固有言語の名前空間を変更する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, namespace
ms.assetid: f20c47e5-230d-4f0e-812f-5c6edb86866c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8b61b248876f701e9d5286063f28b4f71d73e18b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671729"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>方法: ドメイン固有言語の名前空間を変更する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドメイン固有言語の名前空間を変更できます。 Dsl **エクスプローラー**、dsl パッケージプロジェクトのプロパティ、およびアセンブリ情報に変更を加える必要があります。

### <a name="to-change-the-namespace-of-a-domain-specific-language"></a>ドメイン固有言語の名前空間を変更するには

1. **Dsl エクスプローラー**で、 **dsl**ノードをクリックします。

2. [ **プロパティ** ] ウィンドウで、" **名前空間** " プロパティを変更します。

3. ソリューションを保存し、テンプレートを変換します。

4. [ **プロジェクト** ] メニューの [ **Dsl プロパティ**] をクリックします。

     プロジェクトのプロパティが表示されます。

5. **[アプリケーション]** タブをクリックします。

6. " **既定の名前空間** " プロパティを新しい名前空間の名前に変更します。

7. アセンブリの名前も変更する場合は、[**アセンブリ名] プロパティ**を変更します。

8. アセンブリ名を変更した場合は、この行を開き、次の行を更新します。

     `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. カスタムコードを記述した場合は、コードファイル内の名前空間とクラス参照を必ず変更してください。

10. Visual Studio の実験的なインスタンスをリセットします。

    1. Delete **\ Users \\ **_{your name}_**\AppData\Local\Microsoft\VisualStudio \\ \* Exp**

    2. Windows の [ **スタート** ] メニューで、[ **すべてのプログラム**]、 **Microsoft Visual Studio 2010 SDK**、[ **ツール**] の順に選択し、 **実験用インスタンスをリセット**します。

11. [ **ビルド** ] メニューの [ **ソリューションのリビルド**] をクリックします。

## <a name="see-also"></a>参照
 [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
