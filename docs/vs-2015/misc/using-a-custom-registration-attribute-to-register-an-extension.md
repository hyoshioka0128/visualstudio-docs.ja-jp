---
title: カスタム登録属性を使用した拡張機能の登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 98068fa7-bda1-4922-b3f6-28680de58c3d
caps.latest.revision: 3
manager: jillfra
ms.openlocfilehash: a619c5d418df3b9b85ab09cf9b907617ebd81b67
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62935785"
---
# <a name="using-a-custom-registration-attribute-to-register-an-extension"></a>カスタム登録属性を使用した拡張機能の登録
場合によっては、拡張機能の新しい登録属性を作成する必要があります。 登録属性を使用して、新しいレジストリキーを追加したり、既存のキーに新しい値を追加したりすることができます。 新しい属性はから派生する必要があり、 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> メソッドとメソッドをオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> ます。  
  
## <a name="creating-a-custom-attribute"></a>カスタム属性の作成  
 次のコードは、新しい登録属性を作成する方法を示しています。  
  
```  
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]  
    public class CustomRegistrationAttribute : RegistrationAttribute  
    {  
    }  
  
```  
  
 は、属性 <xref:System.AttributeUsageAttribute> クラスで、属性が関連するプログラム要素 (クラス、メソッドなど)、複数回使用できるかどうか、および継承できるかどうかを指定するために使用されます。  
  
### <a name="creating-a-registry-key"></a>レジストリキーの作成  
 次のコードでは、カスタム属性によって、登録されている VSPackage のキーの下に **カスタム** サブキーが作成されます。  
  
```  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + @"}\Custom");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
    }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveKey(@"Packages\" + context.ComponentType.GUID + @"}\Custom");  
}  
  
```  
  
### <a name="creating-a-new-value-under-an-existing-registry-key"></a>既存のレジストリキーの下に新しい値を作成する  
 既存のキーにカスタム値を追加できます。 次のコードは、VSPackage 登録キーに新しい値を追加する方法を示しています。  
  
```  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + "}");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
                }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveValue(@"Packages\" + context.ComponentType.GUID, "NewCustom");  
}  
  
```