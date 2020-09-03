---
title: VSTO システムプロジェクトを作成または開くための VBA アクセス
decsprition: You must explicitly enable access to the Office VBA project system before you can create or open a Visual Studio Tools for Office system project
titleSuffix: Visual Studio Tools for Microsoft Office
ms.custom: seodec18
ms.date: 08/14/2019
ms.topic: conceptual
f1_keywords:
- vst.project.vbawrongversion
- VST.Project.VBASecurityGenericError
- VST.Project.VBASecurityPermissions
- VST.SelectDocWizard.MissingCOM
- VST.Project.VBASecurityNotSet
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3199b23f7ad1bb45fd509d2a9b5cd21da1a49971
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "69551548"
---
# <a name="enable-access-to-vba-to-create-or-open-a-visual-studio-tools-for-the-microsoft-office-system-project"></a>VBA へのアクセスを有効にして、Microsoft Office システムプロジェクトの Visual Studio Tools を作成または開く

Microsoft Office システムプロジェクトの Visual Studio Tools を作成または開くには、Microsoft Office の Visual Basic for Applications (VBA) プロジェクトシステムへのアクセスを明示的に有効にする必要があります。

 Microsoft Office の開発プロジェクトでは、プロジェクトで Visual Basic for Applications を使用していない場合でも、Microsoft Office Word と Microsoft Office Excel で Visual Basic for Applications (VBA) プロジェクトシステムにアクセスする必要があります。 Visual Basic プロジェクトと C# プロジェクトでは、デザイン時にコントロールをサポートするために Visual Basic for Applications プロジェクト システムを使用します。

 一部の Microsoft Office マクロ ウイルスは、ウイルス感染を広げる手段として Visual Basic for Applications プロジェクト システムを自動化しようとします。 Visual Basic for Applications プロジェクト システムへのアクセスを許可すると、マクロ ウイルスの感染防止に有効な保護手段が削除されます。 ただし、通常のマクロ セキュリティは有効なままであるため、コンピューターでマクロを実行するかどうかは、Office アプリケーションで保持されているマクロ セキュリティ レベルおよび信頼される発行者のリストによって決まります。

> [!NOTE]
> これは開発用のコンピューターにのみ適用されます。 エンドユーザーのコンピューターでは、Office ソリューションを実行するためにこのオプションを有効にする必要はありません。

 Visual Basic for Applications プロジェクト システムへのアクセスを禁止してもウイルスから保護されないことに注意してください。コンピューターがそれ以前に一部のマクロ ウイルスに感染していた場合にも、他の文書へのウイルス感染の防止に役立つだけです。 コンピューターに保護層を追加するこのオプションは、既定では無効になっていますが、セキュリティに関する以下のベスト プラクティスに従えば、このオプションを有効にしてもコンピューターがウイルスに感染しやすくなることはありません。

 Office マクロウイルスに対する最良の保護は、高または非常に高いセキュリティレベルで Office を実行し、検証された既知のソースからのマクロのみを信頼し、セキュリティ更新プログラムとウイルス検索プログラムを使用して最新の状態を維持することです。

 [ **Visual Basic プロジェクトへのアクセスを** 手動で信頼する] オプションを有効または無効にすることができます。

 VBA エラーまたは COM エラーが表示される場合、Office のインストールを修復できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-enable-or-disable-access-to-visual-basic-projects"></a>Visual Basic プロジェクトへのアクセスを有効または無効にするには

1. **[ファイル]** タブをクリックします。

2. **[オプション]** をクリックします。

3. [ **セキュリティセンター**] をクリックし、[ **セキュリティセンターの設定**] をクリックします。

4. **セキュリティセンター**で、[**マクロの設定**] をクリックします。

5. **VBA プロジェクトオブジェクトモデルへのアクセス権**を確認またはオフにして、Visual Basic プロジェクトへのアクセスを有効または無効にします。

6. **[OK]** をクリックします。

### <a name="to-enable-or-disable-access-to-visual-basic-projects-with-the-2007-microsoft-office-system"></a>2007 Microsoft Office システムで Visual Basic プロジェクトへのアクセスを有効または無効にするには

1. Word または Excel の [ **ツール** ] メニューの [ **マクロ**] をポイントし、[ **セキュリティ**] をクリックします。

2. [ **セキュリティ** ] ダイアログボックスで、[ **信頼された発行元** ] タブをクリックします。

3. **Visual Basic プロジェクトへのアクセス**を有効または無効にします。オフにします。

4. **[OK]** をクリックします。

## <a name="to-set-your-office-macro-security-level"></a>Office マクロのセキュリティ レベルを設定するには

1. **[ファイル]** タブをクリックします。

2. **[オプション]** をクリックします。

3. [ **セキュリティセンター**] をクリックし、[ **セキュリティセンターの設定**] をクリックします。

4. **セキュリティセンター**で、[**マクロの設定**] をクリックします。

5. [ **マクロの設定** ] セクションで、目的の設定を選択します。

6. **[OK]** をクリックします。

### <a name="to-set-your-office-macro-security-level-with-the-2007-microsoft-office-system"></a>2007 Microsoft Office システムで Office マクロのセキュリティレベルを設定するには

1. Word または Excel の [ **ツール** ] メニューの [ **マクロ**] をポイントし、[ **セキュリティ**] をクリックします。

2. [ **セキュリティレベル** ] タブで、目的の設定を選択します。

    [ **セキュリティレベル** ] タブには、各レベルの詳細が表示されます。 詳細については、Office ヘルプの「マクロのセキュリティ レベル」を参照してください。

### <a name="to-install-vba-with-the-2007-microsoft-office-system"></a>2007 Microsoft Office システムとともに VBA をインストールするには

1. コントロールパネルで、[ **プログラムの追加と削除** ] または [ **プログラムと機能**] を実行します。

2. [ **現在インストールされているプログラム** ] ボックスの一覧で [Office] を選択します。

3. **[変更]** をクリックします。

4. [ **機能の追加または削除**] を選択し、[ **続行**] をクリックします。

5. [ **アプリケーションの高度なカスタマイズを選択**する] を選択し、[ **次へ**] をクリックします。

6. [**アプリケーションおよびツールの更新オプションを選択**します] の一覧で [ **Office 共有機能**] を展開します。

7. [ **Visual Basic for Applications**] の横にあるドロップダウンメニューを開き、[ **マイコンピューターから実行**] をクリックします。

8. **[Continue]** をクリックします。

9. **[閉じる]** をクリックします。

## <a name="to-repair-your-installation-of-office"></a>Office のインストールを修復するには

1. コントロールパネルで、[ **プログラムの追加と削除** ] または [ **プログラムと機能**] を実行します。

2. **現在インストールさ**れているプログラムの一覧で、使用している Office のバージョンを選択します。

3. **[変更]** をクリックします。

4. [ **再インストールまたは修復**] を選択し、[ **次へ**] をクリックします。

5. [ **Office のインストールでエラーを検出して修復**する] を選択し、[ **インストール**] をクリックします。

## <a name="see-also"></a>関連項目
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
