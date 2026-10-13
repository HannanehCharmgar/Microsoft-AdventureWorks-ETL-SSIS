# پروژه‌ی ETL با SSIS بر پایه‌ی Microsoft AdventureWorks

این پروژه با هدف یادگیری و پیاده‌سازی فرایند **ETL** با استفاده از **SQL Server Integration Services (SSIS)** و دیتابیس‌های نمونه‌ی AdventureWorks مایکروسافت طراحی شده است.



## معرفی پروژه

هدف این پروژه، استخراج داده‌ها از دیتابیس عملیاتی AdventureWorks، انجام تبدیل‌های موردنیاز و بارگذاری داده‌ها در انبار داده‌ی AdventureWorks است.

تمرکز اصلی پروژه بر یادگیری عملی فرایندهای ETL، کار با داده‌های رابطه‌ای، مفاهیم مدل‌سازی ابعادی و پیاده‌سازی فرایند انتقال داده با استفاده از SSIS است.

## اهداف پروژه

- بررسی ساختار و ارتباط بین جداول دیتابیس عملیاتی AdventureWorks
- انتخاب جداول مرتبط با فرایند فروش اینترنتی برای طراحی فرایند ETL
- طراحی و پیاده‌سازی پکیج‌های ETL با استفاده از SSIS
- انتقال داده‌ها به جداول مناسب در انبار داده
- بررسی صحت و سازگاری داده‌ها بین مبدأ و مقصد
- آزمایش فرایند ETL با افزودن داده‌ی جدید به منبع و بررسی انتقال آن به انبار داده

## ابزارها و فناوری‌های مورد استفاده

- **Microsoft SQL Server:** مدیریت و ذخیره‌سازی داده‌ها
- **SQL Server Management Studio (SSMS):** بررسی دیتابیس‌ها و اجرای Queryهای SQL
- **SQL Server Integration Services (SSIS):** طراحی و اجرای فرایندهای ETL
- **Visual Studio:** توسعه‌ی پکیج‌های SSIS
- **Git و GitHub:** مدیریت نسخه‌ها و مستندسازی پروژه

## منابع داده

در این پروژه از دو دیتابیس نمونه‌ی مایکروسافت استفاده می‌شود:

| نام دیتابیس | کاربرد |
|---|---|
| `AdventureWorks2025` | دیتابیس عملیاتی و منبع داده (OLTP) |
| `AdventureWorksDW2025` | دیتابیس انبار داده و مقصد انتقال (Data Warehouse) |

این دیتابیس‌ها محیطی مناسب برای تمرین استخراج، تبدیل و بارگذاری داده‌ها و آشنایی با مدل‌سازی ابعادی فراهم می‌کنند.

## مراحل کلی فرایند ETL

فرایند موردنظر شامل مراحل اصلی زیر است:

1. **استخراج (Extract):** دریافت داده‌ها از جداول منتخب دیتابیس مبدأ.
2. **تبدیل (Transform):** انجام تبدیل‌های موردنیاز و آماده‌سازی داده‌ها برای بارگذاری در مقصد.
3. **بارگذاری (Load):** انتقال داده‌های آماده‌شده به جداول متناظر در انبار داده.
4. **اعتبارسنجی (Validate):** بررسی تعداد رکوردها، سازگاری داده‌ها و صحت عملکرد بارگذاری داده‌های جدید.

## محدوده‌ی پروژه

تمرکز پروژه بر حوزه‌ی فروش اینترنتی و موجودیت‌های مرتبط با آن است؛ از جمله:

- مشتریان (Customers)
- محصولات (Products)
- دسته‌بندی محصولات (Product Categories)
- جغرافیا (Geography)
- مناطق فروش (Sales Territories)
- اطلاعات فروش اینترنتی (Internet Sales)

در این پروژه، مشتریان (`DimCustomer`)، محصولات (`DimProduct`)، دسته‌بندی و زیردسته‌های محصولات (`DimProductCategory` و `DimProductSubcategory`)، جغرافیا (`DimGeography`) و مناطق فروش (`DimSalesTerritory`) از نوع **Dimension** هستند و اطلاعات فروش اینترنتی در جدول `FactInternetSales` از نوع **Fact** ذخیره می‌شود.  
مدل انبار داده بر اساس **Star Schema (شمای ستاره‌ای)** طراحی شده است؛ به این صورت که جدول Fact از طریق کلیدهای خارجی به جدول‌های Dimension مرتبط می‌شود.
## شمای کلی پروژه

                   
flowchart TB
    C["DimCustomer"]
    P["DimProduct"]
    T["DimSalesTerritory"]

    subgraph CENTER[" "]
        direction LR
        D["DimDate"]
        F["FactInternetSales<br/>────────────<br/>SalesOrderNumber<br/>SalesOrderLineNumber<br/>OrderQuantity<br/>SalesAmount"]
        PR["DimPromotion"]
    end

    CU["DimCurrency"]

    C --- F
    P --- F
    T --- F
    D --- F
    PR --- F
    CU --- F

    style F fill:#D9F2E6,stroke:#16805D,stroke-width:3px,color:#123B2D
    style C fill:#EAF1FF,stroke:#4776C5,color:#172D50
    style P fill:#EAF1FF,stroke:#4776C5,color:#172D50
    style T fill:#EAF1FF,stroke:#4776C5,color:#172D50
    style D fill:#EAF1FF,stroke:#4776C5,color:#172D50
    style PR fill:#EAF1FF,stroke:#4776C5,color:#172D50
    style CU fill:#EAF1FF,stroke:#4776C5,color:#172D50
    style CENTER fill:transparent,stroke:transparent

                       
## مهارت‌های مورد تمرین

- طراحی و پیاده‌سازی فرایندهای ETL با SSIS
- نوشتن Queryهای SQL و تحلیل داده‌های رابطه‌ای
- شناخت تفاوت OLTP و انبار داده
- آشنایی با روابط جداول Fact و Dimension
- اعتبارسنجی داده‌ها و بارگذاری افزایشی (Incremental Load)
- عیب‌یابی و آزمایش فرایندهای انتقال داده

## وضعیت پروژه

**در حال انجام (In Progress)**

این پروژه به‌عنوان یک تمرین عملی برای توسعه‌ی مهارت‌ها در زمینه‌ی SQL Server، ابزار SSIS و طراحی انبار داده در حال توسعه است.

## منبع داده

دیتابیس‌های AdventureWorks نمونه‌داده‌هایی هستند که توسط مایکروسافت برای اهداف آموزشی و توسعه ارائه شده‌اند. داده‌های این پروژه از این مجموعه‌ی نمونه استفاده می‌کنند و به‌عنوان داده‌ی اصلی تولیدشده توسط نویسنده معرفی نمی‌شوند.
