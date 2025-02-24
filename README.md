<div dir="rtl">

##  لارافيل يتحدث العربي - Laravel Speaks Arabic

[![Latest Version on Packagist](https://img.shields.io/packagist/v/adnane/laravel-speaks-arabic.svg?style=flat-square)](https://packagist.org/packages/adnane/laravel-speaks-arabic)
[![MIT Licensed](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Total Downloads](https://img.shields.io/packagist/dt/adnane/laravel-speaks-arabic.svg?style=flat-square)](https://packagist.org/packages/adnane/laravel-speaks-arabic)

**حزمة خفيفة الوزن تسهل التعامل مع المفاهيم العربية في لارافيل، بإستخدام مجموعة من الفئات، الأساليب والتوابع لجعل لارافل يتحدث العربي! مفاهيم من مثل السلاسل النصية العربي والتواريخ الهجرية وغيرها**

**مثال**

<div dir="ltr">

```php 
@toWords(12078437); 
// اثنا عشر مليون و ثمان و سبعون ألف و أربع مئة و سبع و ثلاثون
```

</div>


## التثبيت

1. التثبيت عن طريق مدير الحزم composer

<div dir="ltr">

```
composer require adnane/laravel-speaks-arabic
```

</div>

2. قم بإضافة مزود خدمة الحزمة الى مصفوفة providers في ملف `config\app.php` كالتالي:

<div dir="ltr">

```php 
'providers' => [ 
    Adnane\Arabic\ArabicServiceProvider::class,
]
```

</div>
 
## كيفية الاستعمال
- بعد التأكد من تثبيت الحزمة على نحو صحيح، سيمكنك تضمين الفئة الرئيسية ```Adnane\Arabic\Arabic``` واستعمال توابعها بشكل عادي

> قم بتغيير ```method``` إلى التابع المراد كـ: ```Arabic::toWords(643646)``` أو كـ: ```arabic()->toWords(643646)```

<div dir="ltr">

```php 
use Adnane\Arabic\Arabic;
Arabic::method($params)

// او مباشرة عن طريق الدالة المساعدة
arabic()::method($params)
```

</div>

## التوابع المتوفرة

**1.التعامل مع الأعداد**

<div dir="ltr">

```php 
/**
 * اعادة كتابة الاعداد كتابة لفظية انطلاقا من كتابة رمزية
 * يسمى أيضا "تفقيط"
 * 
 * @return string 
*/
Arabic::toWords(int $integer)

/**
 * اعادة كتابة الاعداد كتابة رمزية انطلاقا من كتابة لفظية
 * هو عكس العملية السابقة
 * 
 * @return int 
*/
Arabic::fromWords(string $str) 

/**
 * جلب العدد الترتيبي انطلاقا من كتابة رمزية لعدد ما 
 * مثال: أول، ثان، ثالث 
 * 
 * @return string 
*/
Arabic::toOrdinal(int $int) 

/**
 * اعادة كتابة الارقام الموجودة في سلسلة نصية ما 
 * كأرقام هندية (۰ - ۱ - ۲ - ۳ - ٤ - ٥ - ٦ - ٧ - ۸ - ۹)
 * 
 * @return string 
*/
Arabic::toIndianNums(string $str) 
```

</div>

**2.التعامل مع التواريخ والتواقيت**

<div dir="ltr">

```php 
/**
 * تحويل تاريخ مكتوب بالتقويم الميلادي 
 * الى تاريخ مكتوب بالتقويم الهجري
 * مكتوبا بصيغة معينة
 * 
 * (الصيغ المدعومة : f , s , n )
 * @return string 
*/
Arabic::toHijri(string $format = 'f' ,string $date)

/**
 * تحويل تاريخ مكتوب بالتقوم الهجري
 * الى تاريخ مكتوب بالتقويم الميلادي
 * 
 * @return string 
*/
Arabic::fromHijri(string $date /*Y/m/d*/);

/**
 * جلب فرق التوقيت بين وقتين او تاريخين. 
 * تمرير المعامل details بالقيمة true 
 * سيقوم باعادة فرق تفصيلي بين هاذين التوقيتين 
 * 
 * @return string 
*/
Arabic::toRelative(string $date ,string $date2 = null ,boolean $detailed = false);

/**
 * جلب توقيت ما انطلاقا من فرق مرفق 
 * مثال: 
 * Arabic::fromRelative('زد سنة') 
 * @return string 
*/
Arabic::fromRelative(string $relative);

```

</div>

**3. التعامل مع السلاسل النصية**

<div dir="ltr">

```php 
/**
 * ازالة التشكيل من سلسلة نصية ما
 *  
 * @return string 
*/
Arabic::removeHarakat(string $str)

/**
 * اعادة كتابة سلسلة نصية ما مكتوبة باللغة الانجليزية 
 * الى المرافق لها بلوحة مفاتيح عربية
 * يمكن استعمال هاته الوظيفة في تحسين عمليات البحث داخل الموقع
 * 
 * @return string 
*/
Arabic::toKeyboardInput(string $str)

/**
 * اعادة كتابة سلسلة نصية عربية ما 
 * بحروف انجليزية
 * يمكن استعمال هاته الوظيفة في انشاء روابط صديقة البحث 
 * @return string 
*/
Arabic::toSpelled(string $str)

/**
 * المكافئ للدالة str_word_count في PHP 
 * من المهم جدا ملاحظة ان دالة ال PHP 
 * str_word_count
 * لا تدعم اللغى العربية 
 * ولذلك ان هاته الوظيفة تعتبرا بديلا عنها في اللغة العريبة
 * @return int 
*/
Arabic::countWords(string $str);

/**
 * التحقق من ما ان كانت سلسلة نصية ما تحوي على الأقل حرفا عربيا واحدا
 * @return boolean 
*/
Arabic::containsAr(string $str);
```

</div>

## أمثلة عن عدة استعمالات

<div dir="ltr">

```php
Arabic::toWords(56)
//  ست وخمسون

Arabic::fromWords("ثمان مئة و خمسة")
//  805

Arabic::toOrdinal(12)
//  الثاني عشر

Arabic::toIndianNums("ولد عليه الصلاة في 12 ربيع الأول")
//  ولد عليه الصلاة في ۱۲ ربيع الاول

Arabic::toHijri('f' ,'2021/12/12')
//  الثامن من جمادى الأولى من السنة الهجرية ألف و أربع مئة و ثلاث و أربعون

Arabic::fromHijri('1442/01/08')
// 8/27/2020

Arabic::toRelative('2010/01/10')
//  منذ أحد عشر سنة

Arabic::toRelative('2010/01/10' ,'2008/01/10')
//  ثلاث سنين 

Arabic::toRelative('2010/01/10' ,'2008/01/10' ,true)
// [ "y" => 3 , "m" => 39 ,"w" => 156 , "d" => 1096 ,"h" => 26304 ,"mn" => 1578240 ,"s" => 94694400 ] 

Arabic::fromRelative('زد سنة')
// 2022/03/28

Arabic::fromRelative('قل ست اشهر')
//  2020/09/28

Arabic::removeHarakat('لا حسَدَ إلَّا في اثنتيْنِ: رجلٌ آتاهُ اللهُ مالًا، فسلَّطَهُ على هلَكتِه في الحقِّ، ورجلٌ آتاهُ اللهُ الحِكمةَ، فهوَ يقضِي بِها، ويُعلِّمُها')
//  لا حسد إلا في اثنتين: رجل آتاه الله مالا، فسلطه على هلكته في الحق، ورجل آتاه الله الحكمة، فهو يقضي بها، ويعلمها

Arabic::toKeyboardInput('dl;k hsjulhg ihji hg]hgm td jpsdk ulgdhj hgfpe fl,ru!')
// يمكن استعمال هاته الدالة في تحسين عمليات البحث بموقع!

Arabic::toSpelled("قد تساعد هاته الدالة في عمل slugs أو تحسين عمليات البحث")
// qd tsaaad haath āldaalt fii aml slugs āoo thsiin amliiāt ālbhth

Arabic::countWords("هاته الدالة هي المكافئة لاخرى بالبي اتش بي غير ان هاته لا تتجاهل ترميز اليو تي اف ايت")
// 18

Arabic::containsAr("this method checks if a given string contains arabic words or charachters , for example : if we mentioned لارفيل يتحدث عربي it will return true!") 
// true
```

</div>

## الاستعمال في ملفات blade 
> قم بتغيير ```method``` إلى التابع المراد كـ: ```Arabic::toWords(643646)``` أو كـ: ```arabic()->toWords(643646)```

<div dir="ltr">

```php 
{{ Arabic::method($input) }}

// أو 

{{ arabic()->method($input) }}
```

</div>

كما سيمكنك استعمال متغيرات القالب التالية لشيفرة أنظف

<div dir="ltr">

```php 
@toWords(4367)
@toOrdinal(564)
@toIndianNums(ولد عليه الصلاة في 12 ربيع الأول) 
@toHijri(2020/12/12)
@toRelative(2019/12/01)
@removeHarakat(فهوَ يقضِي بِها، ويُعلِّمُها)
```

</div>

## المساهمة

**لا تتردد في المساهمة أو مساعدتنا في جعل Laravel يتحدث اللغة العربية بشكل أفضل من خلال فتح مناقشة أو إضافة بعض الطرق الإضافية أو إصلاح خطأ أو المساعدة في تحسين بعض الأساليب!**

</div>

# ```Laravel Speaks Arabic```

**"Laravel Speaks Arabic" is a light weight ,open-source laravel package . It facilitates dealing with arabic concepts in Laravel Framework using a set of classes and methods to make laravel speaks arabic! concepts like , Hijri Dates & Arabic strings and so on ..**

**code example**

```php 
use Adnane\Arabic\Arabic;

echo Arabic::toWords(12078437); // اثنا عشر مليون و ثمان و سبعون ألف و أربع مئة و سبع و ثلاثون

```
# ```installation```

1.install via composer 
```
composer require adnane/laravel-speaks-arabic
```

2.Laravel Speaks Arabic's Provider will be automaticly added to the providers array in ```config\app.php``` , as you can manually add it 

```php 
'providers' => [ 
    Adnane\Arabic\ArabicServiceProvider::class,
]
```

> you may define an alias in ```config\app.php``` in the aliases array for easy calls
```php 
'Arabic' => Adnane\Arabic\Arabic::class,
```

# ```use in blade files```
> change ```method``` to needed method like ```Arabic::toWords(643646)``` or ```arabic()->toWords(643646)```

```php 
{{ Arabic::method($input) }}
// make sure you define an alias first
```
or
```php 
{{ arabic()->method($input) }}
```
 
# ```How to use``` 
>Methods Can Be Called in Severeal Ways . statically, non-statically or using a helper or an imported class.

> change ```method``` to needed method like ```Arabic::toWords(643646)``` or ```arabic()->toWords(643646)```

**1.using a helper**
```php 
arabic()->method($params)
// or
arabic()::method($params)
```
**2.using an imported class**
```php 
use Adnane\Arabic\Arabic;
// or by using an alias 
use Arabic;


Arabic::method($params)
```


# ```Methods```

**1.Working with numbers & integers**
```php 
/**
 * get the arabic words representation of a given int , called also تفقيط 
 * @return string 
*/
Arabic::toWords(int $integer)

/**
 * get the numeric representation of a given string , reverse of previous method 
 * @return int 
*/
Arabic::fromWords(string $str) 

/**
 * get the ordinal form of a given int
 * @return string 
*/
Arabic::toOrdinal(int $int) 

/**
 * rewrite numbers in a containing string to be like ۱٧۳۱۸
 * @return string 
*/
Arabic::toIndianNums(string $str) 
```

**2.Working with dates & times**

```php 
/**
 * convert a given date to hijri takwim date in a given format (format : f , s , n )
 * @return string 
*/
Arabic::toHijri(string $format = 'f' ,string $date)

/**
 * convert a given hijri hijri to gregorian normal date 
 * @return string 
*/
Arabic::fromHijri(string $date /*Y/m/d*/);

/**
 * Get the relative time between two given dates 
 * @return string 
*/
Arabic::toRelative(string $date ,string $date2 = null ,boolean $detailed = false);

/**
 * Get the date from a given relative time 
 * @return string 
*/
Arabic::fromRelative(string $relative);

```
**3.Working with Strings & longTexts**

```php 
/**
 * get rid of The vowel diacritics in Arabic  
 * @return string 
*/
Arabic::removeHarakat(string $str)

/**
 * rewrite strings and texts to match the keyboard reveresed in english 
 * this method can be really helpful when it comes to making search procces better 
 * @return string 
*/
Arabic::toKeyboardInput(string $str)

/**
 * rewrite strings and texts to be written and spelled in english letters 
 * this mehotd can be really helpful when it comes to making seo friendly url's or arabic slugs 
 * @return string 
*/
Arabic::toSpelled(string $str)

/**
 * equivilant of str_word_count in non utf8 strings & longTexts such as arabic  
 * @return int 
*/
Arabic::countWords(string $str);

/**
 * check if a given string contains arabic charachters 
 * @return boolean 
*/
Arabic::containsAr(string $str);
```

# ```Examples Of Different Uses```
```php
Arabic::toWords(56)
//  ست وخمسون

Arabic::fromWords("ثمان مئة و خمسة")
//  805

Arabic::toOrdinal(12)
//  الثاني عشر

Arabic::toIndianNums("ولد عليه الصلاة في 12 ربيع الأول")
//  ولد عليه الصلاة في ۱۲ ربيع الاول

Arabic::toHijri('f' ,'2021/12/12')
//  الثامن من جمادى الأولى من السنة الهجرية ألف و أربع مئة و ثلاث و أربعون

Arabic::fromHijri('1442/01/08')
// 8/27/2020

Arabic::toRelative('2010/01/10')
//  منذ أحد عشر سنة

Arabic::toRelative('2010/01/10' ,'2008/01/10')
//  ثلاث سنين 

Arabic::toRelative('2010/01/10' ,'2008/01/10' ,true)
// [ "y" => 3 , "m" => 39 ,"w" => 156 , "d" => 1096 ,"h" => 26304 ,"mn" => 1578240 ,"s" => 94694400 ] 

Arabic::fromRelative('زد سنة')
// 2022/03/28

Arabic::fromRelative('قل ست اشهر')
//  2020/09/28

Arabic::removeHarakat('لا حسَدَ إلَّا في اثنتيْنِ: رجلٌ آتاهُ اللهُ مالًا، فسلَّطَهُ على هلَكتِه في الحقِّ، ورجلٌ آتاهُ اللهُ الحِكمةَ، فهوَ يقضِي بِها، ويُعلِّمُها')
//  لا حسد إلا في اثنتين: رجل آتاه الله مالا، فسلطه على هلكته في الحق، ورجل آتاه الله الحكمة، فهو يقضي بها، ويعلمها

Arabic::toKeyboardInput('dl;k hsjulhg ihji hg]hgm td jpsdk ulgdhj hgfpe fl,ru!')
// يمكن استعمال هاته الدالة في تحسين عمليات البحث بموقع!

Arabic::toSpelled("قد تساعد هاته الدالة في عمل slugs أو تحسين عمليات البحث")
// qd tsaaad haath āldaalt fii aml slugs āoo thsiin amliiāt ālbhth

Arabic::countWords("هاته الدالة هي المكافئة لاخرى بالبي اتش بي غير ان هاته لا تتجاهل ترميز اليو تي اف ايت")
// 18

Arabic::containsAr("this method checks if a given string contains arabic words or charachters , for example : if we mentioned لارفيل يتحدث عربي it will return true!") 
// true
```

# ```Important Notes```
**This package is still under development ,as it was recently created, please feel free to contribute or help us making laravel speaks arabic better by opening a discuss , fixing a bug or helping in improving some methods!**

**it's highly recommended you follow the written code manner**
1. Create new PHP class in [/src/Ar/](/ar/)
2. You may need to add some data in [/Ar/data/YourFolder/](/Ar/data/YourFolder/) 
2. define your method & related instance in ```$methods property``` in [/src/Arabic.php](/src/Arabic.php) !

That's it!
