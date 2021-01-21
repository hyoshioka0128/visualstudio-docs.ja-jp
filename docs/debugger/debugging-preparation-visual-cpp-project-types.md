---
title: C++ プロジェクトのデバッグを準備する | Microsoft Docs
description: Visual Studio で、Visual C++ プロジェクト テンプレートによって作成された基本的な種類のプロジェクトをデバッグするための準備に関する情報をお届けします。
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- project templates, debugging
- C++ projects, debugging
- debug builds, project settings
- debugging [C++]
ms.assetid: 912b4ba2-7719-43d5-b087-db33e3f9329a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 1e399b28d3ddce07cae263550b536c21ad1db028
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97728305"
---
# <a name="debugging-preparation-c-project-types"></a>デバッグの準備:C++ プロジェクトの種類
ここでは、[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] プロジェクト テンプレートで作成された基本的なプロジェクトの種類をデバッグする方法について説明します。

 出力として DLL を作成するプロジェクトは、共通する特徴があるため「[DLL プロジェクトのデバッグ](../debugger/debugging-dll-projects.md)」にグループ化されています。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
 [プロパティの推奨設定](#BKMK_Recommended_Property_Settings)

 [Win32 プロジェクト](#BKMK_Win32_Projects)

- [C または C++ の Win32 アプリケーションをデバッグするには](#BKMK_To_debug_a_C_or_C___Win32_application)

- [デバッグ構成を手動で設定するには](#BKMK_To_manually_set_a_Debug_configuration)

  [Windows フォーム アプリケーション (.NET)](#BKMK_Windows_Forms_Applications___NET_)

## <a name="recommended-property-settings"></a><a name="BKMK_Recommended_Property_Settings"></a> プロパティの推奨設定
 プロパティによっては、すべてのアンマネージ デバッグ シナリオで同じように設定する必要があります。 プロパティの推奨設定を以下に示します。 ここに記載されていない設定は、アンマネージ プロジェクトの種類によって異なる場合があります。 詳細については、「[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)」を参照してください。

### <a name="configuration-properties-124-cc-124-optimization-node"></a>構成プロパティ &#124; C/C++ &#124; 最適化ノード

|プロパティ名|設定|
|-------------------|-------------|
|**Optimization**|**[無効 (/0d)]** に設定します。 最適化されたコードは、生成された命令がソース コードと直接対応していないため、デバッグが困難です。 プログラムで、最適化されたコード内だけに現れるバグが見つかった場合は、この設定を有効にできます。 **[逆アセンブル]** ウィンドウに表示されるコードは最適化されたソースから生成されているため、ソース ウィンドウに表示されるコードとは一致しない可能性があります。 また、ステップなどの他の機能が正常に動作しない場合もあります。|

### <a name="configuration-properties-124-linker-124-debugging-node"></a>構成プロパティ &#124; リンカー &#124; デバッグ ノード

|プロパティ名|設定|
|-------------------|-------------|
|**デバッグ情報の生成**|このオプションは、デバッグ シンボルとデバッグに必要なファイルを作成するために常に **[はい (/DEBUG)]** に設定する必要があります。 アプリケーションを稼働するときは、このオプションをオフに設定できます。|

 [このトピックの内容](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)

## <a name="win32-projects"></a><a name="BKMK_Win32_Projects"></a> Win32 プロジェクト
 Win32 アプリケーションは、C または C++ で記述される従来の Windows プログラムです。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、この種類のアプリケーションを簡単にデバッグできます。

 Win32 アプリケーションには、MFC アプリケーションと ATL プロジェクトが含まれます。 これらは Windows API を使用します。MFC や ATL を使用することはありますが、共通言語ランタイム (CLR: Common Language Runtime) は使用しません。 ただし、CLR を使用するマネージド コードを呼び出すことはできます。

 次の手順では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内から Win32 プロジェクトをデバッグする方法を説明します。 Win32 アプリケーションをデバッグするもう 1 つの方法では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の外部でアプリケーションを起動してアタッチします。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

### <a name="to-debug-a-c-or-c-win32-application"></a><a name="BKMK_To_debug_a_C_or_C___Win32_application"></a> C または C++ の Win32 アプリケーションをデバッグするには

1. Visual Studio でプロジェクトを開きます。

2. **[デバッグ]** メニューの **[開始]** を選びます。

3. 「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」で説明されている手法を使用してデバッグ ます。

### <a name="to-manually-set-a-debug-configuration"></a><a name="BKMK_To_manually_set_a_Debug_configuration"></a> デバッグ構成を手動で設定するには

1. **[表示]** メニューの **[プロパティ ページ]** をクリックします。

2. **[構成プロパティ]** ノードが開いていない場合は、ノードをクリックして開きます。

3. **[全般]** をクリックし、 **[出力]** 行の値を **[デバッグ]** に設定します。

4. **[C/C++]** ノードを開き、 **[全般]** をクリックします。

    **[デバッグ]** 行で、コンパイラで生成するデバッグ情報の種類を指定します。 選択できる値は、 **[プログラム データベース (/Zi)]** 、 **[エディット コンティニュ用プログラム データベース (/ZI)]** などです。

5. **[最適化]** をクリックし、 **[最適化]** 行で、ドロップダウン リストの **[無効 (/0d)]** をクリックします。

    最適化されたコードは、生成された命令がソース コードと直接対応していないため、デバッグが困難です。 プログラムで、最適化されたコード内だけに現れるバグが見つかった場合は、この設定を有効にできます。[逆アセンブル] ウィンドウに表示されるコードは最適化されたソースから生成されているため、ソース ウィンドウに表示されるコードとは一致しない可能性があります。 ステップ実行などの機能で、ブレークポイントや実行ポイントが正しく表示されない場合があります。

6. **[リンカー]** ノードを開き、 **[デバッグ]** をクリックします。 最初の **[デバッグ情報の生成]** 行で、ドロップダウン リストの **[はい (/DEBUG)]** をクリックします。 デバッグ時には、必ずこのオプションを設定する必要があります。

   詳細については、「[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)」を参照してください。

   [このトピックの内容](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)

## <a name="windows-forms-applications-net"></a><a name="BKMK_Windows_Forms_Applications___NET_"></a> Windows フォーム アプリケーション (.NET)
 **Windows フォーム アプリケーション (.NET)** テンプレートを使用して [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] Windows フォーム アプリケーションを作成できます。 詳細については、[Windows アプリケーション プロジェクトを作成する](/previous-versions/visualstudio/visual-studio-2010/42wc9kk5(v=vs.100))」を参照してください。

 この種のアプリケーションを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でデバッグする作業は、マネージド Windows フォーム アプリケーションのデバッグ作業に似ています。

 プロジェクト テンプレートを使用して Windows フォーム プロジェクトを作成する場合、デバッグ構成とリリース構成に必要な設定は [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって自動的に作成されます。 必要に応じて、これらの設定を **[\<project name> プロパティ ページ]** ダイアログ ボックスで変更できます。 詳細については、[デバッグ構成とリリース構成](../debugger/how-to-set-debug-and-release-configurations.md)に関するページを参照してください。

 詳細については、「[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)」を参照してください。

 Windows フォーム アプリケーションをデバッグするもう 1 つの方法では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の外部でアプリケーションを起動してアタッチします。 詳細については、「[実行中のプログラムまたは複数のプログラムへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。

 [このトピックの内容](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)

## <a name="see-also"></a>関連項目
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [実行中のプログラムまたは複数のプログラムへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [デバッグ構成とリリース構成](../debugger/how-to-set-debug-and-release-configurations.md)
- [方法: Windows アプリケーション プロジェクトを作成する](/previous-versions/visualstudio/visual-studio-2010/42wc9kk5(v=vs.100))