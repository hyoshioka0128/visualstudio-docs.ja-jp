---
title: '方法: C# プロジェクトでコードを VBA に公開する'
description: 2種類のコードが相互に対話できるようにする場合に、Visual C# プロジェクトのコードを Visual Basic for Applications (VBA) コードに公開する方法について説明します。
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1df1eed4edec3efdbf93f4effc352b3d02656d04
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889409"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>方法: Visual C# プロジェクトでコードを VBA に公開する
  2種類のコードが相互に対話できるようにする場合は、Visual C# プロジェクトのコードを Visual Basic for Applications (VBA) コードに公開できます。

 Visual C# のプロセスは、Visual Basic プロセスとは異なります。 詳細については、「 [方法: Visual Basic プロジェクトでコードを VBA に公開](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)する」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>Visual C# プロジェクトでコードを公開する
 VBA コードが Visual C# プロジェクトのコードを呼び出せるようにするには、コードを変更して COM に表示されるようにし、デザイナーで **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定します。

 VBA から Visual C# プロジェクトのメソッドを呼び出す方法を示すチュートリアルについては、「 [チュートリアル: Visual C&#35; プロジェクトの vba からコードを呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)」を参照してください。

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>Visual C# プロジェクトのコードを VBA に公開するには

1. マクロをサポートし、既に VBA コードが含まれている Word 文書、Excel ブック、または Excel テンプレートに基づくドキュメントレベルのプロジェクトを開くか、作成します。

    マクロをサポートするドキュメントファイル形式の詳細については、「 [VBA とドキュメントレベルのカスタマイズの結合](../vsto/combining-vba-and-document-level-customizations.md)」を参照してください。

   > [!NOTE]
   > この機能は、Word テンプレート プロジェクトでは使用できません。

2. マクロを有効にするようユーザーに求めることなく、ドキュメント内の VBA コードの実行が許可されていることを確認します。 Word または Excel のセキュリティ センター設定の信頼できる場所の一覧に Office プロジェクトの場所を追加することによって、VBA コードの実行を信頼することができます。

3. VBA に公開するメンバーをプロジェクトのパブリッククラスに追加し、新しいメンバーを **パブリック** として宣言します。

4. 次の <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性と <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性を、VBA に公開するクラスに適用します。 これらの属性によってクラスが COM で表示されるようになりますが、クラスのインターフェイスは生成されません。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. プロジェクトのホスト項目クラスの **GetAutomationObject** メソッドをオーバーライドして、VBA に公開するクラスのインスタンスを返します。

   - ホスト項目クラスを VBA に公開する場合は、このクラスに属する **GetAutomationObject** メソッドをオーバーライドし、クラスの現在のインスタンスを返します。

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - ホスト項目ではないクラスを VBA に公開する場合は、プロジェクト内の任意のホスト項目の **GetAutomationObject** メソッドをオーバーライドし、非ホスト項目クラスのインスタンスを返します。 たとえば、次のコードは、という名前のクラスを VBA に公開していることを前提としてい `DocumentUtilities` ます。

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     ホスト項目の詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

6. VBA に公開しているクラスからインターフェイスを抽出します。 [ **インターフェイスの抽出** ] ダイアログボックスで、インターフェイス宣言に含めるパブリックメンバーを選択します。 詳細については、「 [インターフェイスの抽出リファクタリング](../ide/reference/extract-interface.md)」を参照してください。

7. **パブリック** キーワードをインターフェイス宣言に追加します。

8. インターフェイスに次の属性を追加して、インターフェイスが COM に表示されるようにし <xref:System.Runtime.InteropServices.ComVisibleAttribute> ます。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. のデザイナーで、ドキュメント (Word の場合) またはワークシート (Excel の場合) を開き [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

10. **[プロパティ]** ウィンドウで、 **ReferenceAssemblyFromVbaProject** プロパティを選択し、値を **True** に変更します。

    > [!NOTE]
    > ブックまたはドキュメントに VBA コードが含まれていない場合、またはドキュメント内の VBA コードの実行が信頼されていない場合は、 **ReferenceAssemblyFromVbaProject** プロパティを **True** に設定するとエラーメッセージが表示されます。 これは、このような状況では、Visual Studio がドキュメントのVBA プロジェクトを変更できないためです。

11. 表示されるメッセージで **[OK]** をクリックします。 このメッセージは、からプロジェクトを実行するときに、ブックまたはドキュメントに VBA コードを追加した場合、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 次回プロジェクトをビルドするときに vba コードが失われることを通知します。 これは、プロジェクトをビルドするたびに、ビルド出力フォルダー内のドキュメントが上書きされるためです。

     この時点で、VBA プロジェクトがアセンブリを呼び出すことができるように、Visual Studio によってプロジェクトが構成されます。 また、Visual Studio では、という名前のメソッドが `GetManagedClass` VBA プロジェクトに追加されます。 Vba プロジェクト内の任意の場所からこのメソッドを呼び出して、VBA に公開したクラスにアクセスできます。

12. プロジェクトをビルドします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [VBA とドキュメントレベルのカスタマイズの結合](../vsto/combining-vba-and-document-level-customizations.md)
- [チュートリアル: Visual C&#35; プロジェクトで VBA からコードを呼び出す](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [方法: Visual Basic プロジェクトでコードを VBA に公開する](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
