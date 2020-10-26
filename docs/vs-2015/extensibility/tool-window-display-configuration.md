---
title: ツールウィンドウの表示構成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, configuring
- tool windows, appearance
ms.assetid: 502a4926-bb83-473e-94e2-8e833c5f8b53
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1af78bd58c42cf1312e36621011802e908c9e919
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186396"
---
# <a name="tool-window-display-configuration"></a>ツール ウィンドウの表示構成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage がツールウィンドウを登録すると、既定の位置、サイズ、ドッキングスタイル、およびその他の可視性情報がオプションの値で指定されます。 ツールウィンドウの登録の詳細については、「[レジストリのツール](../extensibility/tool-windows-in-the-registry.md)ウィンドウ」を参照してください。  
  
## <a name="window-display-information"></a>ウィンドウの表示情報  
 ツールウィンドウの基本的な表示構成は、最大6つのオプション値で格納されます。  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        <Version>\  
          ToolWindows\  
            <Tool Window GUID>\  
              (Default)       = reg_sz: <Package GUID>Name            = reg_sz: <name of tool window>Float           = reg_sz: <position>Style           = reg_sz: <dock style>Window          = reg_sz: <window GUID>Orientation     = reg_sz: <orientation>DontForceCreate = reg_dword: 0x00000000  
```  
  
|名前|種類|Data|説明|  
|----------|----------|----------|-----------------|  
|名前|REG_SZ|"短い名前をここに入力してください"|ツールウィンドウを説明する短い名前。 レジストリ内の参照にのみ使用されます。|  
|Float|REG_SZ|"X1, Y1, X2, Y2"|4つのコンマ区切りの値。 X1, Y1 は、ツールウィンドウの左上隅の座標です。 X2、Y2 は右下隅の座標です。 すべての値は画面座標にあります。|  
|Style|REG_SZ|MDI<br /><br /> 点<br /><br /> 付け<br /><br /> 付<br /><br /> "Always Float"|ツールウィンドウの初期表示状態を指定するキーワード。<br /><br /> "MDI" = MDI ウィンドウと共にドッキングされます。<br /><br /> "Float" = 浮動小数点型です。<br /><br /> "リンク" = 別のウィンドウ (ウィンドウエントリで指定) にリンクされています。<br /><br /> "タブ付き" = 別のツールウィンドウと組み合わせて使用します。<br /><br /> "Always Float" = をドッキングすることはできません。<br /><br /> 詳細については、以下の「コメント」セクションを参照してください。|  
|ウィンドウ|REG_SZ|*\<GUID>*|ツールウィンドウをリンクまたはタブ表示できるウィンドウの GUID。 GUID は、独自のウィンドウまたは IDE 内のウィンドウのいずれかに属している場合があり [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。|  
|方向|REG_SZ|左側<br /><br /> 直角<br /><br /> 上端<br /><br /> 最終|以下のコメントセクションを参照してください。|  
|DontForceCreate|REG_DWORD|0 または 1|このエントリが存在し、その値がゼロでない場合、ウィンドウは読み込まれますが、すぐには表示されません。|  
  
### <a name="comments"></a>コメント  
 [方向] エントリは、タイトルバーがダブルクリックされたときにツールウィンドウをドッキングする位置を定義します。 位置は、ウィンドウエントリで指定されたウィンドウに対する相対位置です。 スタイルエントリが "リンク" に設定されている場合、向きエントリは "Left"、"Right"、"Top"、または "Bottom" のいずれかになります。 スタイルエントリが "タブ付き" の場合、[向き] エントリは "Left" または "Right" にすることができ、タブを追加する場所を指定します。 スタイルエントリが "Float" の場合、ツールウィンドウは最初にフローティングします。 タイトルバーをダブルクリックすると、向きとウィンドウのエントリが適用され、ウィンドウは "タブ付き" スタイルを使用します。 Style エントリが "Always Float" の場合、ツールウィンドウをドッキングすることはできません。 Style エントリが "MDI" の場合、ツールウィンドウは MDI 領域にリンクされ、ウィンドウエントリは無視されます。  
  
### <a name="example"></a>例  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        8.0Exp\  
          ToolWindows\  
            {A0C5197D-0AC7-4B63-97CD-8872A789D233}\  
              (Default)       = reg_sz: {DA9FB551-C724-11D0-AE1F-00A0C90FFFC3}  
              DontForceCreate = reg_dword: 0x00000000  
              Float           = reg_sz: 100,100,450,300  
              Name            = reg_sz: Bookmarks  
              Orientation     = reg_sz: Left  
              Style           = reg_sz: Tabbed  
              Window          = reg_sz: {34E76E81-EE4A-11D0-00A0C90FFFC3}  
```  
  
## <a name="tool-window-visibility"></a>ツールウィンドウの表示  
 オプションの可視性サブキーの値によって、ツールウィンドウの表示設定が決まります。 値の名前は、ウィンドウの可視性を必要とするコマンドの Guid を格納するために使用されます。 コマンドが実行されると、IDE はツールウィンドウが作成され、表示されることを保証します。  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        <Version>\  
          ToolWindows\  
            <Tool Window GUID>\  
              Visibility\  
                (Default) = reg_sz:  
                <GUID>    = reg_dword:  
                <GUID>    = reg_dword:  
                <GUID>    = reg_sz:  
```  
  
|名前|種類|Data|説明|  
|----------|----------|----------|-----------------|  
|(既定)|REG_SZ|なし|空のままにします。|  
|*\<GUID>*|REG_DWORD または REG_SZ|0または説明の文字列。|省略可能。 エントリの名前は、可視性を必要とするコマンドの GUID である必要があります。 値は、情報を示す文字列のみを保持します。 通常、この値は0に設定されてい `reg_dword` ます。|  
  
### <a name="example"></a>例  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        8.0Exp\  
          ToolWindows\  
            {EEFA5220-E298-11D0-8F78-00A0C9110057}\  
              Visibility\  
                (Default) = reg_sz:  
                {93694fa0-0397-11d1-9f4e-00a0c911004f} = reg_dword: 0x00000000  
                {9DA22B82-6211-11d2-9561-00600818403B} = reg_dword: 0x00000000  
                {adfc4e66-0397-11d1-9f4e-00a0c911004f} = reg_dword: 0x00000000  
```  
  
## <a name="see-also"></a>参照  
 [VSPackage の基本事項](../misc/vspackage-essentials.md)
