---
title: VSTO アドインのレジストリエントリ
description: Visual Studio を使用して作成された VSTO アドインを配置するときに、特定のレジストリエントリセットを作成する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: d90b341fb4233c10c54947a6349480ea0c33b23a
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97524998"
---
# <a name="registry-entries-for-vsto-add-ins"></a>VSTO アドインのレジストリエントリ
  Visual Studio で作成した VSTO アドインを配置するときには、一連のレジストリ エントリを作成する必要があります。 それらのレジストリ エントリで指定する情報によって、Microsoft Office アプリケーションは VSTO アドインを検出し、読み込むことができます。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 プロジェクトをビルドすると、Visual Studio によって開発用コンピューター上にレジストリ エントリが作成されるので、VSTO アドインを簡単に実行およびデバッグできます。 ClickOnce を使用して VSTO アドインを配置すると、エンドユーザーのコンピューター上にレジストリエントリが自動的に作成されます。 Windows インストーラーを使用して VSTO アドインを配置する場合は、InstallShield 制限付きエディションプロジェクトを構成して、エンドユーザーのコンピューターにレジストリエントリを作成する必要があります。

 VSTO アドインの読み込みプロセス中にレジストリ エントリがどのように使用されるかについては、「 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

> [!NOTE]
> このトピックでは、テキスト *アドイン ID* は VSTO アドインの一意の ID を表します。 既定では、この ID は VSTO アドイン アセンブリの名前です。

## <a name="register-vsto-add-ins-for-the-current-user-vs-all-users"></a>現在のユーザーとすべてのユーザーに対して VSTO アドインを登録する
 VSTO アドインをインストールするときは、次の 2 つの方法で登録できます。

- 現在のユーザーのみ (つまり、VSTO アドインをインストールするときにコンピューターにログオンしているユーザーのみが使用できます)。 この場合、レジストリエントリは **HKEY_CURRENT_USER** の下に作成されます。

- すべてのユーザー (つまり、コンピューターにログオンするすべてのユーザーが VSTO アドインを使用できるようになります)。 この場合、レジストリエントリは **HKEY_LOCAL_MACHINE** の下に作成されます。

  Visual Studio を使用して作成したすべての VSTO アドインは、現在のユーザー用に登録できます。 ただし、特定のシナリオに限り、VSTO アドインをすべてのユーザー用に登録できます。 これらのシナリオは、コンピューター上の Microsoft Office のバージョン、および VSTO アドインの配置方法によって異なります。

### <a name="deployment-type"></a>デプロイの種類
 ClickOnce を使用して VSTO アドインを配置する場合は、現在のユーザー用にのみ VSTO アドインを登録できます。 これは、ClickOnce が **HKEY_CURRENT_USER** でのキーの作成のみをサポートしているためです。 VSTO アドインをコンピューター上のすべてのユーザー用に登録する場合は、Windows インストーラーを使用して VSTO アドインを配置する必要があります。 これらの展開の種類の詳細については、「 [ClickOnce を使用した office ソリューションの配置](../vsto/deploying-an-office-solution-by-using-clickonce.md) 」と「 [Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="registry-entries"></a>レジストリ エントリ
 必要な VSTO アドインレジストリエントリは、次のレジストリキーの下にあります。ここでは、インストールが現在のユーザーとすべてのユーザーのどちらであるかによって、 *ルート* が **HKEY_CURRENT_USER** または **HKEY_LOCAL_MACHINE** ます。

|Office アプリケーション|構成パス|
|------------------|------------------|
|Visio|*ルート*\Software\Microsoft \\  \\ *の Visio アドイン ID*|
|その他すべて|*ルート*\Software\Microsoft\Office \\ *Office アプリケーション名*\ アドイン \\ *ID*|

> [!NOTE]
> インストーラーが64ビットの Windows 上のすべてのユーザーを対象としている場合は、HKEY_LOCAL_MACHINE\Software\Microsoft の下に1つ、HKEY_LOCAL_MACHINE\SoftwareWOW6432Node \Microsoft hive の下に1つずつ、2つのレジストリエントリを含めることをお勧めし \\ ます。 これは、ユーザーがコンピューターで32ビット版または64ビット版の Office を使用できる可能性があるためです。
>
>インストーラーが現在のユーザーを対象としている場合は、HKEY_CURRENT_USER\Software パスが共有されているため、WOW6432Node にインストールする必要はありません。
>
>詳細について[は、レジストリの32ビットおよび64ビットアプリケーションデータ](/windows/win32/sysinfo/32-bit-and-64-bit-application-data-in-the-registry)を参照してください。

 このレジストリ キーの下にあるエントリを次の表に示します。

|入力|Type|値|
|-----------|----------|-----------|
|**説明**|REG_SZ|必須です。 VSTO アドインの簡単な説明。<br /><br /> この説明は、ユーザーが Microsoft Office アプリケーションの **[オプション]** ダイアログ ボックスの **[アドイン]** ペインで VSTO アドインを選択したときに表示されます。|
|**FriendlyName**|REG_SZ|必須です。 Microsoft Office アプリケーションの **[COM アドイン]** ダイアログ ボックスに表示される、VSTO アドインの説明的な名前。 既定値は VSTO アドイン ID です。|
|**LoadBehavior**|REG_DWORD|必須です。 アプリケーションが VSTO アドインを読み込みを試行した時点と、VSTO アドインの現在の状態 (読み込まれているかアンロードされているか) を示す値。<br /><br /> このエントリの既定値は 3 です。これは、VSTO アドインが起動時に読み込まれたことを示します。 詳細については、「 [LoadBehavior values](#LoadBehavior)」を参照してください。 **注:** ユーザーが VSTO アドインを無効にすると、その操作によって **HKEY_CURRENT_USER** レジストリハイブの **LoadBehavior** 値が変更されます。 ユーザーごとに、HKEY_CURRENT_USER hive の **LoadBehavior** 値の値によって、 **HKEY_LOCAL_MACHINE** hive で定義されている既定の **LoadBehavior** がオーバーライドされます。|
|**file:///**|REG_SZ|必須です。 VSTO アドインの配置マニフェストの完全なパス。 ローカル コンピューター上の場所、ネットワーク共有 (UNC)、Web サーバー (HTTP) のいずれかを指定できます。<br /><br /> Windows インストーラーを使用してソリューションを配置する場合、 **マニフェスト** パスにプレフィックス " **file:///** " を追加する必要があります。 また、このパスの末尾に、文字列 **&#124;vstolocal** (つまり、パイプ文字 **&#124;** の後に **vstolocal**) を追加する必要があります。 これにより、ClickOnce キャッシュではなく、インストール フォルダーからソリューションが読み込まれます。 詳細については、「 [Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。 **注:**  開発用コンピューターで VSTO アドインをビルドすると、Visual Studio によって **&#124;vstolocal** 文字列がこのレジストリエントリに自動的に追加されます。|

### <a name="registry-entries-for-outlook-form-regions"></a><a name="OutlookEntries"></a> Outlook フォーム領域のレジストリエントリ
 Outlook 用 VSTO アドインにカスタム フォーム領域を作成する場合は、フォーム領域を Outlook に登録するために追加のレジストリ エントリが使用されます。 これらのエントリは、フォーム領域がサポートするメッセージ クラスごとに異なるレジストリ キーの下に作成されます。 これらのレジストリキーは次の場所にあります。 *ルート* は **HKEY_CURRENT_USER** または **HKEY_LOCAL_MACHINE** です。

 *Root*\Software\Microsoft\Office\Outlook\FormRegions \\ *message クラス*

 すべての VSTO アドインで共有されるその他のレジストリ エントリと同様に、プロジェクトをビルドすると、Visual Studio によって開発用コンピューター上にフォーム領域レジストリ エントリが作成されます。 ClickOnce を使用して VSTO アドインを配置すると、エンドユーザーのコンピューター上にレジストリエントリが自動的に作成されます。 Windows インストーラーを使用して VSTO アドインを配置する場合は、InstallShield 制限付きエディションプロジェクトを構成して、エンドユーザーのコンピューターにレジストリエントリを作成する必要があります。

 フォーム領域レジストリエントリの詳細については、「 [カスタムフォームでのフォーム領域の位置の指定](/office/vba/outlook/Concepts/Creating-Form-Regions/specify-the-location-of-a-form-region-in-a-custom-form)」を参照してください。 Outlook フォーム領域の詳細については、「 [outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」を参照してください。

## <a name="loadbehavior-values"></a><a name="LoadBehavior"></a> LoadBehavior の値
 *ルート*\Software\Microsoft\Office アプリケーション名 **LOADBEHAVIOR** のアドイン ID キーの下にあるエントリには、 \\  \\  VSTO アドインの実行時の動作を指定する値のビットごとの組み合わせが含まれています。 最下位のビット (値 0 および 1) は、VSTO アドインが現在アンロードされているか、または読み込み済みであるかを示します。 その他のビットは、アプリケーションが VSTO アドインを読み込もうとしていることを示します。

 通常、 **LoadBehavior** エントリは、VSTO アドインをエンドユーザーのコンピューターにインストールするときに、0、3、または 16 (10 進数) に設定することを目的としています。 既定では、VSTO アドインをビルドまたは発行すると、Visual Studio によってアドインの **LoadBehavior** エントリが 3 に設定されます。

 **LoadBehavior** エントリに指定できるすべての値を次の表に示します。 この表では、VSTO アドインを手動またはプログラムによって読み込む場合も示されています。 VSTO アドインを手動で読み込むには、アプリケーションの **[COM アドイン]** ダイアログ ボックスで、VSTO アドインの横にあるチェック ボックスをオンにします。 VSTO アドインをプログラムによって読み込むには、VSTO アドインを表す <xref:Microsoft.Office.Core.COMAddIn.Connect%2A> オブジェクトの <xref:Microsoft.Office.Core.COMAddIn> プロパティを **true**」を参照してください。

|値 (10 進形式)|VSTO アドインの状態|VSTO アドインの読み込み動作|説明|
|--------------------------|-------------------------|--------------------------------|-----------------|
|0|アンロードされました|自動的に読み込まない|VSTO アプリケーションは自動的にアドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 0 のままですが、 **[COM アドイン]** ダイアログ ボックスの VSTO アドインの状態は更新されて、VSTO アドインが読み込み済みであることが示されます。|
|1|読み込み|自動的に読み込まない|VSTO アプリケーションは自動的にアドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> [ **COM アドイン** ] ダイアログボックスには、アプリケーションの起動時に vsto アドインが読み込まれることが示されますが、手動またはプログラムによって読み込まれるまで vsto アドインは読み込まれません。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 0 に変更されます。アプリケーションの終了後も 0 のままです。|
|2|アンロードされました|スタート時に読み込む|アプリケーションは自動的に VSTO アドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 3 に変更されます。アプリケーションの終了後も 3 のままです。|
|3|読み込み|スタート時に読み込む|アプリケーションが起動時に VSTO アドインを読み込もうとします。 これは、Visual Studio で VSTO アドインをビルドまたは発行した場合の既定値です。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 3 のままです。 VSTO アドインの読み込み中にエラーが発生した場合、 **LoadBehavior** の値は 2 に変更されます。アプリケーションの終了後も 2 のままです。|
|8|アンロードされました|必要に応じて読み込む|アプリケーションは自動的に VSTO アドインを読み込みません。 VSTO アドインを読み込むには、ユーザーが手動で読み込むか、またはプログラムによって読み込みます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 9 に変更されます。|
|9|読み込み|必要に応じて読み込む|VSTO アドインの機能を使用する UI 要素 (たとえば、リボンのカスタム ボタン) をユーザーがクリックしたときなど、アプリケーションで要求されたときにのみ VSTO アドインが読み込まれます。<br /><br /> VSTO アドインの読み込みが成功した場合、 **LoadBehavior** の値は 9 のままですが、 **[COM アドイン]** ダイアログ ボックスの VSTO アドインの状態は更新されて、VSTO アドインが現在読み込み済みであることが示されます。 VSTO アドインの読み込み中にエラーが発生した場合は、 **LoadBehavior** の値が 8 に変更されます。|
|16|読み込み|初回に読み込み、その後必要に応じて読み込む|VSTO アドインを必要に応じて読み込む場合は、この値を設定します。 ユーザーが最初にアプリケーションを起動したときに、アプリケーションが VSTO アドインを読み込みます。 ユーザーが次にアプリケーションを実行したときには、VSTO アドインによって定義された UI 要素が読み込まれますが、VSTO アドインはユーザーが VSTO アドインに関連付けられた UI 要素をクリックするまで読み込まれません。<br /><br /> VSTO アドインの最初の読み込みが成功した場合、VSTO アドインが読み込まれている間 **LoadBehavior** の値は 16 のままです。 アプリケーションの終了後、 **LoadBehavior** の値は 9 に変更されます。|

## <a name="see-also"></a>関連項目
- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
 