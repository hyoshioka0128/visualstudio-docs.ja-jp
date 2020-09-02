---
title: グリフコントロール (ソース管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b0960209b67c8d2f111296840119807d95bb2e2d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538422"
---
# <a name="glyph-control-source-control-vspackage"></a>グリフ管理 (ソース管理 VSPackage)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理 Vspackage で使用できる詳細な統合の一部は、ソース管理下の項目の状態を示す独自のグリフを表示する機能です。  
  
## <a name="levels-of-glyph-control"></a>グリフコントロールのレベル  
 状態グリフは、 **ソリューションエクスプローラー** や **クラスビュー**などで表示されたときの項目の現在の状態を示すアイコンです。 ソース管理 VSPackage は、2つのレベルのグリフコントロールを実行できます。 このオプションは、IDE によって提供される定義済みのグリフセットに対して、グリフの選択を制限し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] たり、表示されるグリフのカスタムセットを定義したりすることができます。  
  
### <a name="default-set-of-glyphs"></a>既定のグリフセット  
 **ソリューションエクスプローラー**の項目に関連付けられている状態グリフを確認するために、プロジェクトはを使用してソース管理から状態グリフを要求し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A> ます。 ソース管理 VSPackage は、IDE によって提供される定義済みのグリフに限定されたグリフの選択を保持することができます。 この場合、VSPackage は、vsshell .idl に定義されているグリフ列挙体を表す値の配列を返します。 詳細については、「」を参照してください <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon> 。これは、IDE によって設定された定義済みのグリフセットで、"チェックイン" グリフの南京錠、"チェックアウト" グリフとしてのチェックマークなどです。  
  
### <a name="custom-set-of-glyphs"></a>グリフのカスタムセット  
 ソース管理 VSPackage は、インストール時に一意の "ルックアンドフィール" で独自のグリフを使用できます。 新しいソース管理 VSPackage がアクティブになると、以前のソース管理 VSPackage がまだ読み込まれていても非アクティブであっても、独自のグリフの使用を開始できるようになります。 このモードでは、ソース管理 VSPackage は既存のアイコンを使用して、選択されている場合にとの一貫性を維持することができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>サービスはインターフェイスをサポートしてい <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> ます。これは、VSPackage が必要に応じて実装でき、IDE によって要求されます。 IDE が要求を行ったときに、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、現在登録されているソース管理 VSPackage からこのインターフェイスを取得しようとします。 インターフェイスが登録されている VSPackage に存在する場合、IDE のカスタムグリフの要求は成功します。それ以外の場合、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE では既定のグリフセットが使用されます。  
  
 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] さまざまなソース管理状態を示すイメージの一覧を取得するために、によって使用されます。 ソース管理 VSPackage は、カスタムグリフのイメージリストへのハンドルを IDE に返します。 IDE はこの時点でイメージリストのコピーを作成し、後で表示するグリフを選択するために使用します。 新しいインターフェイスがサポートされていない場合、または `IVsSccGlyphs::GetCustomGlyphList` メソッドが E_NOTIMPL を返した場合、IDE はによって提供されるグリフの既定のリストからグリフを取得し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>   
 <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
