---
machine_translated: true
machine_translated_rev: 72537a2d527c63c07aa5d2361a8829f3895cf2bd
---

# در بند {#prewhere-clause}

در اینجا بهینه سازی برای اعمال فیلتر موثر تر است. این به طور پیش فرض حتی اگر فعال باشد `PREWHERE` بند به صراحت مشخص نشده است. این به طور خودکار در حال حرکت بخشی از کار می کند [WHERE](where.md) شرط به مرحله قبل از کجا. نقش `PREWHERE` بند تنها برای کنترل این بهینه سازی اگر شما فکر می کنم که شما می دانید که چگونه به انجام این کار بهتر از پیش فرض اتفاق می افتد است.

با prewhere بهینه سازی در ابتدا تنها ستون لازم برای اجرای prewhere بیان بخوانید. سپس ستون های دیگر خوانده می شوند که برای اجرای بقیه پرس و جو مورد نیاز است اما تنها بلوک هایی که بیان قبل از هر کجا است “true” حداقل برای برخی از ردیف. اگر بلوک های زیادی وجود دارد که بیان قبل از کجا است “false” برای تمام سطر و جایی نیاز ستون کمتر از سایر بخش های پرس و جو, این اغلب اجازه می دهد تا به خواندن اطلاعات بسیار کمتر از دیسک برای اجرای پرس و جو.

## کنترل دستی {#controlling-prewhere-manually}

بند همان معنی به عنوان `WHERE` بند بند. تفاوت در این است که داده ها از جدول خوانده می شوند. هنگامی که دستی کنترل می شود `PREWHERE` برای شرایط فیلتراسیون که توسط اقلیتی از ستون ها در پرس و جو استفاده می شود, اما که فیلتراسیون داده های قوی. این باعث کاهش حجم داده ها به خواندن.

پرسوجو ممکن است همزمان مشخص شود `PREWHERE` و `WHERE`. در این مورد, `PREWHERE` مقدمها `WHERE`.

اگر `optimize_move_to_prewhere` تنظیم تنظیم شده است به 0, اکتشافی به طور خودکار حرکت بخش هایی از عبارات از `WHERE` به `PREWHERE` غیرفعال می شوند.

## محدودیت ها {#limitations}

`PREWHERE` تنها با جداول از پشتیبانی `*MergeTree` خانواده
