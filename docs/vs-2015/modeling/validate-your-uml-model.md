---
title: UML モデルを検証する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML, constraints
- UML, validation
ms.assetid: deed5092-c11d-4431-a801-1e866a103075
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8dfaf19e358d96b7737b06880d6fa4581b5c54f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659368"
---
# <a name="validate-your-uml-model"></a>UML モデルの検証
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio で描画できる UML モデルの一部が、プロジェクトでは無効と見なされる場合があります。 たとえば、ユース ケースのアクターを表す生存線のあるシーケンス図には必ずユース ケースをリンクするように求める場合があります。 このような要件にチームが準拠するための *制約* をインストールまたは定義できます。 制約は、ユーザーがモデルを保存するときまたは開くときに適用することが可能で、メニュー コマンドで呼び出すことができます。

 制約は、チームが UML モデルをどのように解釈して使用するかによって異なるため、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] には制約は付属していません。 しかし、独自の制約を定義したり、他のユーザーが定義した制約をインストールしたりすることはできます。 制約を定義し、それらを分布用にパッケージ化する方法については、「 [UML モデルの検証制約を定義](../modeling/define-validation-constraints-for-uml-models.md)する」を参照してください。

## <a name="invoking-validation"></a>検証の呼び出し
 検証拡張機能のインストールが完了している場合、それによって提供される制約は、次のケースで適用できます。 一部の制約は、これらのケースの一部でのみ適用されるように設定されています。

- **検証コマンド。** 検証をいつでも呼び出すには、[**アーキテクチャ**] メニューの [ **UML モデルの検証**] をクリックします。

  > [!NOTE]
  > 検証制約がインストールされている場合に限り、コマンドが表示されます。

- **モデルの保存時。** モデルを保存するとき、検証制約を適用できます。 これらの制約の目的は、プロジェクトの解釈に従った場合に無効であるモデルが保存されることがないようにすることです。

   エラーがある場合は、モデルを保存するかどうかを確認するメッセージが表示されます。 エラーを修正するか、またはモデルをそのまま保存するかを選択することができます。

- **モデルを開くとき。** モデルを開くときに、検証メソッドを適用して、モデルを保存したときに存在していたエラー メッセージを復元できます。 エラーは、1 つのモデルの異なる部分で作業していた複数のユーザーによって加えられた変更の間の不整合が原因で発生する場合もあります。 詳細については、「 [モデルの共有」および「ダイアグラムのエクスポート](../modeling/share-models-and-exporting-diagrams.md)」を参照してください。

  検証エラーは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] エラー ウィンドウで報告されます。

  図の中でエラーが発生している要素を選択するには、エラーをダブルクリックします。 この操作は、エラーが発生している要素を、開いている図に表示できる場合に限り有効です。

## <a name="installing-validation-constraints"></a>検証制約のインストール
 制約は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張 (VSIX) ファイル内にパッケージ化されます。 通常、一連の制約は、メニュー コマンド、プロファイル、ツールボックス項目などの他の定義も含んだ拡張機能の一部となります。

#### <a name="to-install-a-visual-studio-extension"></a>Visual Studio 拡張機能をインストールするには

1. エクスプローラー (またはファイルエクスプローラー) で **.vsix** ファイルをダブルクリックします。

2. 既に実行されている [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインスタンスを再起動します。

## <a name="disabling-and-uninstalling-validation-constraints"></a>検証制約の無効化およびインストール
 制約を適用しないモデルを操作するとき、制約を含んだ拡張機能を一時的に無効にすることができます。 この方法により、各種の拡張機能を有効または無効にして、さまざまなモデルを個別に操作できます。

#### <a name="to-disable-or-uninstall-a-visual-studio-extension"></a>Visual Studio 拡張機能を無効化またはアンインストールするには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. 拡張子の横にある [ **無効** ] をクリックして、拡張機能を一時的に無効にします。 後で再び有効にするには、[ **拡張機能と更新プログラム** ] ウィンドウに戻ります。

     \- または

     拡張機能を削除するには、[ **アンインストール** ] をクリックします。

3. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を再起動します。

## <a name="see-also"></a>参照
 [UML モデルの検証制約を定義](../modeling/define-validation-constraints-for-uml-models.md)する[アプリの](../modeling/create-models-for-your-app.md)モデルを作成する[開発プロセスで](../modeling/use-models-in-your-development-process.md)のモデルの使用
