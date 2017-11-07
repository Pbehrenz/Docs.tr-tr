---
title: "ASP.NET Core Razor sayfalarının uygulamada bir modeli ekleme"
author: rick-anderson
description: "ASP.NET Core Razor sayfalarının uygulamada bir modeli ekleme"
keywords: "ASP.NET Core, Razor sayfalarının Razor, MVC"
ms.author: riande
manager: wpickett
ms.date: 07/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/model
ms.openlocfilehash: 195128f670223f15e1679c51fb6354c1aa527c01
ms.sourcegitcommit: 3ba32b2b6425ed94604cb0f681db0d5bb5f8ad58
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2017
---
# <a name="adding-a-model-to-a-razor-pages-app"></a>Bir model için bir Razor sayfalarının uygulama ekleme

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a>Bir veri modeli ekleme

Çözüm Gezgini'nde sağ **RazorPagesMovie** Proje > **Ekle** > **yeni klasör**. Klasör adı *modelleri*.

Sağ tıklayın *modelleri* klasör. Seçin **ekleme** > **sınıfı**. Sınıf adını **film** ve aşağıdaki özellikleri ekleyin:

[!INCLUDE[model 2](../../includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a>Bir veritabanı bağlantı dizesi Ekle

Bir bağlantı dizesi eklemek *appsettings.json* dosya.

[!code-json[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a>Veritabanı bağlamı kaydetme

Veritabanı bağlamı ile kayıt [bağımlılık ekleme](xref:fundamentals/dependency-injection) kapsayıcısında *haline* dosya.

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-6)]

Herhangi bir hata yoksa doğrulamak için projeyi oluşturun.

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a>İskele araç ekleyin ve başlangıç geçiş gerçekleştirme

Bu bölümde, Paket Yöneticisi Konsolu (PMC) için kullanın:

* Visual Studio web kod oluşturma paketi ekleyin. Bu paket, yapı iskelesi altyapısı çalıştırmak için gereklidir.
* İlk geçiş ekleyin.
* Veritabanı ile ilk geçiş güncelleştirin.

Gelen **Araçları** menüsünde, select **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.

  ![PMC menüsü](../first-mvc-app/adding-model/_static/pmc.png)

PMC aşağıdaki komutları girin:

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.0
Add-Migration Initial
Update-Database
```

`Install-Package` Komutu yapı iskelesi altyapısı çalıştırmak için gerekli araçları yükler.

`Add-Migration` Komutu ilk veritabanı şeması oluşturmak için kod oluşturur. Belirtilen model şeması dayalı `DbContext` (içinde *Models/MovieContext.cs* dosyası). `Initial` Bağımsız değişkeni geçişler adlandırmak için kullanılır. Herhangi bir ad kullanabilirsiniz, ancak kurala göre geçiş açıklayan bir ad seçin. Bkz: [geçişler giriş](xref:data/ef-mvc/migrations#introduction-to-migrations) daha fazla bilgi için.

`Update-Database` Komutu çalıştırır `Up` yönteminde *geçişleri /\<zaman damgası > _InitialCreate.cs* dosyası bir veritabanı oluşturur.

[!INCLUDE[model 4windows](../../includes/RP/model4Win.md)]

[!INCLUDE[model 4](../../includes/RP/model4.md)]

Sonraki öğretici yapı iskelesi tarafından oluşturulan dosyalar açıklanmaktadır.

>[!div class="step-by-step"]
[Önceki: Başlarken](xref:tutorials/razor-pages/razor-pages-start)
[sonraki: iskele kurulmuş Razor sayfaları](xref:tutorials/razor-pages/page)    