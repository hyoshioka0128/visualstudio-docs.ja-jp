---
title: VSTO アドインのレジストリ エントリ
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- LoadBehavior entry
- add-ins [Office development in Visual Studio], registry entries
- registry keys [Office development in Visual Studio]
- application-level add-ins [Office development in Visual Studio], registry entries
- registry entries [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b02b50c42692ec2fd455358df5157e0b8481562b
ms.sourcegitcommit: b32fbbcbc43910b0ed7ce79aa9a22f2ed36ab57e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79416524"
---
# <a name="registry-entries-for-vsto-add-ins"></a>VSTO アドインのレジストリ エントリ
  Visual Studio で作成した VSTO アドインを配置するときには、一連のレジストリ エントリを作成する必要があります。 それらのレジストリ エントリで指定する情報によって、Microsoft Office アプリケーションは VSTO アドインを検出し、読み込むことができます。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 プロジェクトをビルドすると、Visual Studio によって開発用コンピューター上にレジストリ エントリが作成されるので、VSTO アドインを簡単に実行およびデバッグできます。 ClickOnce を使用して VSTO アドインを配置すると、レジストリ エントリはエンド ユーザーのコンピューターに自動的に作成されます。 Windows インストーラーを使用して VSTO アドインを展開する場合は、エンド ユーザー コンピューター上にレジストリ エントリを作成するように InstallShield 限定版プロジェクトを構成する必要があります。

 VSTO アドインの読み込みプロセス中にレジストリ エントリがどのように使用されるかについては、「 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

> [!NOTE]
> このトピックでは、テキスト *アドイン ID* は VSTO アドインの一意の ID を表します。 既定では、この ID は VSTO アドイン アセンブリの名前です。

## <a name="register-vsto-add-ins-for-the-current-user-vs-all-users"></a>現在のユーザーとすべてのユーザーの VSTO アドインを登録する
 VSTO アドインをインストールするときは、次の 2 つの方法で登録できます。

- 現在のユーザーの場合のみ (つまり、VSTO アドインがインストールされているときにコンピュータにログオンしているユーザーのみが使用できます)。 この場合、レジストリ エントリは**HKEY_CURRENT_USER**の下に作成されます。

- すべてのユーザー (つまり、コンピューターにログオンするすべてのユーザーが VSTO アドインを使用できます)。 この場合、レジストリ エントリは**HKEY_LOCAL_MACHINE**の下に作成されます。

  Visual Studio を使用して作成したすべての VSTO アドインは、現在のユーザー用に登録できます。 ただし、特定のシナリオに限り、VSTO アドインをすべてのユーザー用に登録できます。 これらのシナリオは、コンピューター上の Microsoft Office のバージョン、および VSTO アドインの配置方法によって異なります。

### <a name="deployment-type"></a>デプロイの種類
 ClickOnce を使用して VSTO アドインを配置する場合は、現在のユーザー用にのみ VSTO アドインを登録できます。 これは、ClickOnce がサポートしているキーの作成はHKEY_CURRENT_USERに限**っている**からです。 VSTO アドインをコンピューター上のすべてのユーザー用に登録する場合は、Windows インストーラーを使用して VSTO アドインを配置する必要があります。 これらの展開の種類の詳細については、「 [ClickOnce を使用して Office ソリューションを配置](../vsto/deploying-an-office-solution-by-using-clickonce.md)する」および[「Windows インストーラーを使用して Office ソリューションを配置する](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="registry-entries"></a>レジストリ エントリ
 必要な VSTO アドイン レジストリ エントリは、Root*が***HKEY_CURRENT_USER**されている次のレジストリ キーの下に配置されます**HKEY_LOCAL_MACHINE。**

|オフィスアプリケーション|構成パス|
|------------------|------------------|
|Visio|*ルート*\ソフトウェア\\\マイクロソフト*Visio*\\\アドイン*ID*|
|その他すべて|*ルート*\ソフトウェア\マイクロソフト\\*\Office Office アプリケーション名*\\\アドイン*ID*|

> [!NOTE]
> インストーラーが 64 ビット Windows 上のすべてのユーザーを対象としている場合は、HKEY_LOCAL_MACHINE\Software\Microsoft の下に 1 つ、HKEY_LOCAL_MACHINE\Software\\**WOW6432Node**\Microsoft ハイブの下に 1 つずつ、2 つのレジストリ エントリを含め、推奨されます。 これは、ユーザーがコンピューター上で 32 ビット版または 64 ビット版の Office を使用できるためです。
>
>インストーラが現在のユーザーを対象としている場合、HKEY_CURRENT_USER\ソフトウェア パスが共有されるため、WOW6432Node にインストールする必要はありません。
>
>詳細については、[レジストリの 32 ビットおよび 64 ビットのアプリケーション データを](/windows/win32/sysinfo/32-bit-and-64-bit-application-data-in-the-registry)参照してください。

 このレジストリ キーの下にあるエントリを次の表に示します。

|エントリ|Type|Value|
|-----------|----------|-----------|
|**説明**|REG_SZ|必須。 VSTO アドインの簡単な説明。<br /><br /> この説明は、ユーザーが Microsoft Office アプリケーションの **[オプション]** ダイアログ ボックスの **[アドイン]** ペインで VSTO アドインを選択したときに表示されます。|
|**Friendlyname**|REG_SZ|必須。 Microsoft Office アプリケーションの **[COM アドイン]** ダイアログ ボックスに表示される、VSTO アドインの説明的な名前。 既定値は VSTO アドイン ID です。|
|**LoadBehavior**|REG_DWORD|必須。 アプリケーションが VSTO アドインを読み込みを試行した時点と、VSTO アドインの現在の状態 (読み込まれているかアンロードされているか) を示す値。<br /><br /> このエントリの既定値は 3 です。これは、VSTO アドインが起動時に読み込まれたことを示します。 詳細については、「 [LoadBehavior 値](#LoadBehavior)」を参照してください。 **注:** ユーザーが VSTO アドインを無効にした場合、そのアクションによって **、HKEY_CURRENT_USER**レジストリ ハイブの**LoadBehavior**値が変更されます。 各ユーザーに対して、HKEY_CURRENT_USER ハイブの**LoadBehavior**値の値は **、HKEY_LOCAL_MACHINE**ハイブで定義されている既定の**LoadBehavior**をオーバーライドします。|
|**Manifest**|REG_SZ|必須。 VSTO アドインの配置マニフェストの完全なパス。 ローカル コンピューター上の場所、ネットワーク共有 (UNC)、Web サーバー (HTTP) のいずれかを指定できます。<br /><br /> Windows インストーラーを使用してソリューションを配置する場合、 **マニフェスト** パスにプレフィックス " **file:///** " を追加する必要があります。 また **、vstolocal&#124;** 文字列 (つまり、パイプ文字 **&#124;に**続く**vstolocal**) をこのパスの末尾に追加する必要があります。 これにより、ClickOnce キャッシュではなく、インストール フォルダーからソリューションが読み込まれます。 詳細については、「 [Windows インストーラを使用して Office ソリューションを配置する](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。 **注:** 開発用コンピューターで VSTO アドインをビルドすると、Visual Studio は、このレジストリ エントリに **&#124;vstolocal**文字列を自動的に追加します。|

### <a name="registry-entries-for-outlook-form-regions"></a><a name="OutlookEntries"></a>Outlook フォーム領域のレジストリ エントリ
 Outlook 用 VSTO アドインにカスタム フォーム領域を作成する場合は、フォーム領域を Outlook に登録するために追加のレジストリ エントリが使用されます。 これらのエントリは、フォーム領域がサポートするメッセージ クラスごとに異なるレジストリ キーの下に作成されます。 これらのレジストリ キーは、次の場所にあります**HKEY_LOCAL_MACHINE** *HKEY_CURRENT_USER。* **HKEY_CURRENT_USER**

 *ルート*\ソフトウェア\マイクロソフト\オフィス\Outlook\フォーム領域\\*メッセージ クラス*

 すべての VSTO アドインで共有されるその他のレジストリ エントリと同様に、プロジェクトをビルドすると、Visual Studio によって開発用コンピューター上にフォーム領域レジストリ エントリが作成されます。 ClickOnce を使用して VSTO アドインを配置すると、レジストリ エントリはエンド ユーザーのコンピューターに自動的に作成されます。 Windows インストーラーを使用して VSTO アドインを展開する場合は、エンド ユーザー コンピューター上にレジストリ エントリを作成するように InstallShield 限定版プロジェクトを構成する必要があります。

 フォーム領域のレジストリ エントリの詳細については、「[ユーザー設定フォームでフォーム領域の場所を指定する](/office/vba/outlook/Concepts/Creating-Form-Regions/specify-the-location-of-a-form-region-in-a-custom-form)」を参照してください。 Outlook フォーム領域の詳細については、「 [Outlook フォーム](../vsto/creating-outlook-form-regions.md)領域の作成 」を参照してください。

## <a name="loadbehavior-values"></a><a name="LoadBehavior"></a>読み込み動作の値
 *ルート*\ソフトウェア\Microsoft\Office\\*アプリケーション名*\Addins\\アドイン*ID*キーの下の**LoadBehavior**エントリには、VSTO アドインの実行時の動作を指定する値のビットごとの組み合わせが含まれています。 最下位のビット (値 0 および 1) は、VSTO アドインが現在アンロードされているか、または読み込み済みであるかを示します。 その他のビットは、アプリケーションが VSTO アドインを読み込もうとしていることを示します。

 通常 **、LoadBehavior**エントリは、エンド ユーザーのコンピューターに VSTO アドインをインストールするときに 0、3、または 16 (10 進数) に設定されることを意図しています。 既定では、VSTO アドインをビルドまたは発行すると、Visual Studio によってアドインの **LoadBehavior** エントリが 3 に設定されます。

 **LoadBehavior** エントリに指定できるすべての値を次の表に示します。 この表では、VSTO アドインを手動またはプログラムによって読み込む場合も示されています。 VSTO アドインを手動で読み込むには、アプリケーションの **[COM アドイン]** ダイアログ ボックスで、VSTO アドインの横にあるチェック ボックスをオンにします。 VSTO アドインをプログラムによって読み込むには、VSTO アドインを表す <xref:Microsoft.Office.Core.COMAddIn.Connect%2A> オブジェクトの <xref:Microsoft.Office.Core.COMAddIn> プロパティを **true**」を参照してください。

|値 (10 進形式)|VSTO アドインの状態|VSTO アドインの読み込み動作|説明|
|--------------------------|-------------------------|--------------------------------|-----------------|
|0|アンロードされました|自動的に読み込まない|VSTO アプリケーションは自動的にアドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 0 のままですが、 **[COM アドイン]** ダイアログ ボックスの VSTO アドインの状態は更新されて、VSTO アドインが読み込み済みであることが示されます。|
|1|読み込み|自動的に読み込まない|VSTO アプリケーションは自動的にアドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> **[COM アドイン**] ダイアログ ボックスでは、アプリケーションの起動後に VSTO アドインが読み込まれることが示されますが、VSTO アドインは手動またはプログラムで読み込まれるまで読み込まれません。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 0 に変更されます。アプリケーションの終了後も 0 のままです。|
|2|アンロードされました|スタート時に読み込む|アプリケーションは自動的に VSTO アドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 3 に変更されます。アプリケーションの終了後も 3 のままです。|
|3|読み込み|スタート時に読み込む|アプリケーションが起動時に VSTO アドインを読み込もうとします。 これは、Visual Studio で VSTO アドインをビルドまたは発行した場合の既定値です。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 3 のままです。 VSTO アドインの読み込み中にエラーが発生した場合、 **LoadBehavior** の値は 2 に変更されます。アプリケーションの終了後も 2 のままです。|
|8|アンロードされました|必要に応じて読み込む|アプリケーションは自動的に VSTO アドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 9 に変更されます。|
|9|読み込み|必要に応じて読み込む|VSTO アドインの機能を使用する UI 要素 (たとえば、リボンのカスタム ボタン) をユーザーがクリックしたときなど、アプリケーションで要求されたときにのみ VSTO アドインが読み込まれます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 9 のままですが、 **[COM アドイン]** ダイアログ ボックスの VSTO アドインの状態は更新されて、VSTO アドインが現在読み込み済みであることが示されます。 VSTO アドインの読み込み中にエラーが発生した場合は、 **LoadBehavior** の値が 8 に変更されます。|
|16|読み込み|初回に読み込み、その後必要に応じて読み込む|VSTO アドインを必要に応じて読み込む場合は、この値を設定します。 ユーザーが最初にアプリケーションを起動したときに、アプリケーションが VSTO アドインを読み込みます。 ユーザーが次にアプリケーションを実行したときには、VSTO アドインによって定義された UI 要素が読み込まれますが、VSTO アドインはユーザーが VSTO アドインに関連付けられた UI 要素をクリックするまで読み込まれません。<br /><br /> VSTO アドインの最初の読み込みが成功した場合、VSTO アドインが読み込まれている間 **LoadBehavior** の値は 16 のままです。 アプリケーションの終了後、 **LoadBehavior** の値は 9 に変更されます。|

## <a name="see-also"></a>関連項目
- [Visual Studio の Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [Office ソリューションの構築](../vsto/building-office-solutions.md)
- [Office ソリューションを展開する](../vsto/deploying-an-office-solution.md)
 