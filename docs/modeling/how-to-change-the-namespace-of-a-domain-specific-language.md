---
title: '方法: ドメイン固有言語の名前空間を変更する'
description: ドメイン固有言語の名前空間を変更する方法について説明します。
ms.date: 10/31/2018
ms.topic: how-to
titleSuffix: ''
helpviewer_keywords:
- Domain-Specific Language, namespace
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 747095a876b353aeef76e2f5321e7f2ffc46136f
ms.sourcegitcommit: a18c7e9b367c2f92f6e54c3eaef442775d457667
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90100801"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>方法: ドメイン固有言語の名前空間を変更する

ドメイン固有言語の名前空間を変更できます。 Dsl **エクスプローラー**、dsl パッケージプロジェクトのプロパティ、およびアセンブリ情報に変更を加えます。

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>ドメイン固有言語の名前空間を変更するには

1. **Dsl エクスプローラー**で**dsl**ノードを選択します。

2. [ **プロパティ** ] ウィンドウで、" **名前空間** " プロパティを変更します。

3. ソリューションを保存し、テンプレートを変換します。

4. [ **プロジェクト** ] メニューの [ **Dsl プロパティ**] を選択します。

   プロジェクトのプロパティが表示されます。

5. **[アプリケーション]** タブを選択します。

6. " **既定の名前空間** " プロパティを新しい名前空間の名前に変更します。

7. アセンブリの名前も変更する場合は、[**アセンブリ名] プロパティ**を変更します。

8. アセンブリ名を変更した場合は、この行を開き、次の行を更新します。

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. カスタムコードを記述した場合は、コードファイル内の名前空間とクラス参照を必ず変更してください。

10. Visual Studio の実験的なインスタンスをリセットします。

    1. Delete **\ Users \\ **_{your name}_**\AppData\Local\Microsoft\VisualStudio \\ \* Exp**。

    2. Windows の [**スタート**] メニューで、[**すべてのプログラム**] を選択し  >  ます。**2010 SDK**  >  **Tools**Microsoft Visual Studio  >  **実験用インスタンスをリセット**します。

11. [ **ビルド** ] メニューの [ **ソリューションのリビルド**] をクリックします。

## <a name="see-also"></a>関連項目

[ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)