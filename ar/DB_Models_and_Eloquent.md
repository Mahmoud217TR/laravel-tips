## DB Models and Eloquent

⬆️ [العودة للقائمة الرئيسية](README.md#laravel-tips) ⬅️ [التالي (Models Relations)](Models_Relations.md)
- [إعادة استخدام أو نسخ استعلام](#reuse-or-clone-query)
- [طرق استعلامات Eloquent الخاصة بالتاريخ](#eloquent-where-date-methods)
- [التزايد والتناقص](#increments-and-decrements)
- [إزالة الحقول الزمنية](#no-timestamp-columns)
- [استعادة عدة سجلات من الحذف المؤقت](#soft-deletes-multiple-restore)
- [تحديد أغمدة مع الطريقة all](#model-all-columns)
- [العثور على نتيجة أو 404](#to-fail-or-not-to-fail)
- [تغيير اسم العامود](#column-name-change)
- [تعديل شكل نتائج الاستعلام](#map-query-results)
- [تغيير أسماء الحقول الزمنية](#change-default-timestamp-fields)
- [ ترتيب سريع حسب زمن الانشاء](#quick-order-by-created_at)
- [قيمة تلقائية للحقول عند الانشاء](#automatic-column-value-when-creating-records)
- [الحسابات في الاستعلامات الخام تكون أسرع](#db-raw-query-calculations-run-faster)
- [أكثر من مجال (scope) واحد](#more-than-one-scope)
- [لا حاجة لتحويل الصيغ عند استعمال Carbon](#no-need-to-convert-carbon)
- [تجميع النتائج باستخدام أول حرف من الاسم](#grouping-by-first-letter)
- [منع تغيير قيمة العامود](#never-update-the-column)
- [الحصول على عدة سجلات باستخدام Find](#find-many)
- [الحصول على أعمدة محددة باستخدام Find](#find-many-and-return-specific-columns)
- [البحث باستخدام المفتاح الأساسي](#find-by-key)
- [استخدم uuid بدلاً من الزيادة التلقائية](#use-uuid-instead-of-auto-increment)
- [التحديد الجزئي (Sub-Selects) بأسلوب لارافيل](#sub-selects-in-laravel-way)
- [إخفاء بعض الأعمدة](#hide-some-columns)
- [التقاط أخطاء SQL](#exact-db-error)
- [الإزالة المؤقتة (Soft-Delete) باستخدام باني الاستعلامات](#soft-deletes-with-query-builder)
- [تنفيذ استعلامات SQL ](#good-old-sql-query)
- [استعمل DB Transactions](#use-db-transactions)
- [التحديث أو الإنشاء](#update-or-create)
- [ازالة المفتاح من الكاش عند الحفظ](#forget-cache-on-save)
- [تغيير صيغة حقلي created_at و updated_a](#change-format-of-created_at-and-updated_at)
- [تخزين المصفوفات بصيغة JSON](#storing-array-type-into-json)
- [استنساخ النموذج](#make-a-copy-of-the-model)
- [تخفيف الذاكرة](#reduce-memory)
- [التنفيذ القسري للاستعلام مع تجاهل fillable و guarded](#force-query-without-fillableguarded)
- [بنى علائقية بثلاث مستويات](#3-level-structure-of-parent-children)
- [إظهار صفحة 404 عند اخفاق عملية البحث](#check-if-record-exists-or-show-404)
- [تنفيذ أوامر عند اخفاق عملية البحث](#perform-any-action-on-failure)
- [الإنهاء في حال فشل الشرط](#abort-if-condition-failed)
- [انجاز خطوات إضافية قبل الحذف](#perform-any-extra-steps-before-deleting-model)
- [ملئ عمود تلقائياً أثناء الادخال](#fill-a-column-automatically-while-you-persist-data-to-the-database)
- [Extra information about the query](#extra-information-about-the-query)
- [Using the doesntExist() method in Laravel](#using-the-doesntexist-method-in-laravel)
- [Trait that you want to add to a few Models to call their boot() method automatically](#trait-that-you-want-to-add-to-a-few-models-to-call-their-boot-method-automatically)
- [There are two common ways of determining if a table is empty in Laravel](#there-are-two-common-ways-of-determining-if-a-table-is-empty-in-laravel)
- [How to prevent “property of non-object” error](#how-to-prevent-property-of-non-object-error)
- [Get original attributes after mutating an Eloquent record](#get-original-attributes-after-mutating-an-eloquent-record)
- [A simple way to seed a database](#a-simple-way-to-seed-a-database)
- [The crossJoinSub method of the query constructor](#the-crossJoinSub-method-of-the-query-constructor)
- [Order by Pivot Fields](#order-by-pivot-fields)
- [Belongs to Many Pivot table naming](#belongs-to-many-pivot-table-naming)
- [Find a single record from a database](#find-a-single-record-from-a-database)
- [Automatic records chunking](#automatic-records-chunking)
- [Updating the model without dispatching events](#updating-the-model-without-dispatching-events)
- [Periodic cleaning of models from obsolete records](#periodic-cleaning-of-models-from-obsolete-records)
- [Immutable dates and casting to them](#immutable-dates-and-casting-to-them)
- [The findOrFail method also accepts a list of ids](#the-findorfail-method-also-accepts-a-list-of-ids)
- [Prunable trait to automatically remove models from your database](#prunable-trait-to-automatically-remove-models-from-your-database)
- [withAggregate method](#withaggregate-method)
- [Date convention](#date-convention)
- [Eloquent multiple upserts](#eloquent-multiple-upserts)
- [Retrieve the Query Builder after filtering the results](#retrieve-the-query-builder-after-filtering-the-results)
- [Custom casts](#custom-casts)
- [Order based on a related model's average or count](#order-based-on-a-related-models-average-or-count)
- [Return transactions result](#return-transactions-result)
- [Remove several global scopes from query](#remove-several-global-scopes-from-query)
- [Order JSON column attribute](#order-JSON-column-attribute)
- [Get single column's value from the first result](#get-single-columns-value-from-the-first-result)
- [Check if altered value changed key](#check-if-altered-value-changed-key)
- [New way to define accessor and mutator](#new-way-to-define-accessor-and-mutator)
- [Another way to do accessors and mutators](#another-way-to-do-accessors-and-mutators)
- [When searching for the first record, you can perform some actions](#when-searching-for-the-first-record-you-can-perform-some-actions)
- [Directly convert created_at date to human readable format](#directly-convert-created_at-date-to-human-readable-format)
- [Ordering by an Eloquent Accessor](#ordering-by-an-eloquent-accessor)
- [Check for specific model was created or found](#check-for-specific-model-was-created-or-found)
- [Laravel Scout with database driver](#laravel-scout-with-database-driver)
- [Make use of the value method on the query builder](#make-use-of-the-value-method-on-the-query-builder)
- [Pass array to where method](#pass-array-to-where-method)
- [Return the primary keys from models collection](#return-the-primary-keys-from-models-collection)
- [Force Laravel to use eager loading](#force-laravel-to-use-eager-loading)
- [Make all your models mass assignable](#make-all-your-models-mass-assignable)
- [Hiding columns in select all statements](#hiding-columns-in-select-all-statements)
- [JSON Where Clauses](#json-where-clauses)
- [Get all the column names for a table](#get-all-the-column-names-for-a-table)
- [Compare the values of two columns](#compare-the-values-of-two-columns)
- [Accessor Caching](#accessor-caching)
- [New scalar() method](#new-scalar-method)
- [Select specific columns](#select-specific-columns)
- [Chain conditional clauses to the query without writing if-else statements](#chain-conditional-clauses-to-the-query-without-writing-if-else-statements)

<a name="reuse-or-clone-query"></a>
### إعادة استخدام أو نسخ استعلام

في العادة عندما نحتاج لتطبيق عدة استعلامات على استعلام مفلتر (filtered query).
فغالباً ما نقوم باستخدام الطريقة `()query`.

لنقم بكتابة استعلام للحصول على المنتجات النشطة (active) وغير النشطة (inactive) التي تم انشائها اليوم.


```php

$query = Product::query();


$today = request()->q_date ?? today();
if($today){
    $query->where('created_at', $today);
}

// الآن لنستعلم عن المنتجات النشطة وغير النشطة
$active_products = $query->where('status', 1)->get(); // $query في هذا السطر قمنا بالتعديل على المتحول 
$inactive_products = $query->where('status', 0)->get(); // بالتالي هنا لن يتم الحصول على أي منتجات غير نشطة
```
لكن، بعد الحصول على المنتجات النشطة `active products$` سيتم تغيير قيمة المتحول ` query$`. بالتالي عند الاستعلام عن المنتجات غير النشطة لن يحتوي `inactive_products$` على أي منتجات من المتحول ` query$` وسيعيد مجموعة (collection) فارغة في كل مرة.
السبب، أنه في كل مرة نبحث عن منتجات غير نشطة باستعلام يعيد المنتجات النشطة فقط.

لنحل هذه المشكلة يمكننا الاستعلام عدة مرات عبر إعادة استخدام الغرض ` query$`. بالتالي سنحتاج لنسخ الغرض ` query$` قبل أن يتم تعديلها بالشكل الآتي: 


```php
$active_products = $query->clone()->where('status', 1)->get(); // $query لن يتم تعديل الغرض
$inactive_products = $query->clone()->where('status', 0)->get(); // $query بالتالي سنحصل على المنتجات غير النشطة بواسطة الغرض

```

<a name="eloquent-where-date-methods"></a>
### طرق استعلامات Eloquent الخاصة بالتاريخ

باستعلامات Eloquent، يمكنك الحصول على النتائج باستخدام طرق التاريخ التالية: 

 `()whereDay()`, `whereMonth()`, `whereYear()`, `whereDate()`,  `whereTime`.

```php
$products = Product::whereDate('created_at', '2018-01-31')->get();
$products = Product::whereMonth('created_at', '12')->get();
$products = Product::whereDay('created_at', '31')->get();
$products = Product::whereYear('created_at', date('Y'))->get();
$products = Product::whereTime('created_at', '=', '14:13:58')->get();
```

<a name="increments-and-decrements"></a>
### التزايد والتناقص

اذا أردت زيادة قيمة في عامود بجدول ضمن قاعدة البيانات. فقط قم باستخدام التابع `()increment`. أما في حال كنت تريده أن تنقص القيمة فقم باستخدام التابع `()decrement`.

بشكل افتراضي يكون مقدار التناقص أو التزايد 1، لكن يمكن تعديله عبر تمرير قيمة كوسيط ثانٍ مثل القيمة 50.


```php
Post::find($post_id)->increment('view_count');
User::find($user_id)->increment('points', 50);

Post::find($post_id)->decrement('view_count')
```

<a name="no-timestamp-columns"></a>
### إزالة الحقول الزمنية

في حال كون جدول قاعدة البيانات الخاص بالنموذج لا يحتوي على حقول زمنية (`created_at` و `updated_at`) يمكنك التصريح للنموذج بعدم استخدامهم عبر اسناد `timestamps = false$`. 


```php
class Company extends Model
{
    public $timestamps = false;
}
```

<a name="soft-deletes-multiple-restore"></a>
### استعادة عدة سجلات من الحذف المؤقت

عندما تستعمل الحذف المؤقت (soft-delete)، يمكنك استعادة عدة سجلات دفعة واحدة.


```php
Post::onlyTrashed()->where('author_id', 1)->restore();
```

<a name="model-all-columns"></a>
### تحديد مجموعة أعمدة مع الطريقة all

عند استدعاء الطريقة `()Model::all` على نموذج يمكنك تحديد الأعمدة المطلوبة فقط عبر تمريرها كوسيط للطريقة.


```php
$users = User::all(['id', 'name', 'email']);
```

<a name="to-fail-or-not-to-fail"></a>
### العثور على نتيجة أو 404

بالإضافة للطريقة `()findOrFail` يوجد أيضاً طريقة Eloquent وهي `()firstOrFail` اللتان تعيدان صفحة لم يتم العثور على المطلوب 404 في حال لم يتم اعادة أي سجل بالاستعلام.


```php
$user = User::where('email', 'povilas@laraveldaily.com')->firstOrFail();
```


<a name="column-name-change"></a>
### تغيير اسم العامود

في باني الاستعلامات (Eloquent Query Builder) يمكنك تحديد اسم جديد لعامود عند الاستعلام عن سجل تماماً كما في استعلام SQL العادي.


```php
$users = DB::table('users')->select('name', 'email as user_email')->get();
```

<a name="map-query-results"></a>
### تعديل شكل نتائج الاستعلام
يمكنك تعديل شكل نتائج استعلام Eloquent باستخدام التابع `()map` الخاص بالمجموعات (Collections). 


```php
$users = User::where('role_id', 1)->get()->map(function (User $user) {
    $user->some_column = some_function($user);
    return $user;
});
```

<a name="change-default-timestamp-fields"></a>
### تغيير أسماء الحقول الزمنية

في حال كنت تتعامل مع قاعدة بيانات غير تابعة لـLaravel وكانت أسماء الحقول الزمنية مختلفة، يمكنك لحسن الحظ تحديد الأسماء الخاصة بالحقول الزمنية:


```php
class Role extends Model
{
    const CREATED_AT = 'create_time';
    const UPDATED_AT = 'update_time';
}
```

<a name="quick-order-by-created_at"></a>
###  ترتيب سريع حسب زمن الانشاء

بدلاً من استخدام الأسلوب التقليدي القديم:
```php
User::orderBy('created_at', 'desc')->get();
```

يمكنك الحصول على نفس النتيجة بشكل أسرع:
```php
User::latest()->get();
```

بشكل افتراضي تقوم الطريقة `()latest` بالترتيب اعتماداً على العامود `created_at`.

يوجد نظير لهذه الطريقة ايضاً حيث يقوم بالترتيب اعتماداً على نفس العامود ولكن تصاعدياً وهي الطريقة `()oldest`.
```php
User::oldest()->get();
```
كما يمكنك تحديد الترتيب بنائاً على عامود مختلف يمكنك تمرريه كوسيط للطريقة، فعلى سبيل المثال للحصول على أخر مستخدم تم تحديثه (الترتيب على عامود `updated_at`): 

```php
$lastUpdatedUser = User::latest('updated_at')->first();
```

<a name="automatic-column-value-when-creating-records"></a>
### قيمة تلقائية للحقول عند الانشاء

اذا كنت تريد انشاء حقل يتم وضع قيمته تلقائياً عند انشاء سجل جديد، قم باضافة آلية الحصول على القيمة داخل الطريقة `()boot` في النموذج. 

على سبيل المثال، اذا أردت أن يتم اسناد الحقل `position` تلقائياً عند انشاء سجل جديد بحيث تكون قيمته`Country::max('position') + 1` نقوم بما يلي: 


```php
class Country extends Model {
    protected static function boot()
    {
        parent::boot();

        Country::creating(function($model) {
            $model->position = Country::max('position') + 1;
        });
    }
}
```

<a name="db-raw-query-calculations-run-faster"></a>
### الحسابات في الاستعلامات الخام تكون أسرع

استعمل استعلامات خام (raw queries) للقيام بحسابات مباشرة على قاعدة البيانات، غالباً ما تكون النتيجة أسرع.
يمكنك استعمال الطريقة `()whereRaw` لكتابة الاستعلام الخام.

كمثال اذا أردت الحصول على المستخدمين الذين كانو نشطين بعد 30 يوماً من تسجيلهم يمكنك ذلك بالشكل الآتي:

```php
User::where('active', 1)
    ->whereRaw('TIMESTAMPDIFF(DAY, created_at, updated_at) > ?', 30)
    ->get();
```

<a name="more-than-one-scope"></a>
### أكثر من مجال (scope) واحد

يمكنك دمج أكثر من مجال (scope) كسلسلة للحصول على نتيجة استعلام أفضل:

في ملف النموذج (Model):
```php
public function scopeActive($query) {
    return $query->where('active', 1);
}

public function scopeRegisteredWithinDays($query, $days) {
    return $query->where('created_at', '>=', now()->subDays($days));
}
```

في ملف المتحكم (Controller):
```php
$users = User::registeredWithinDays(30)->active()->get();
```

<a name="no-need-to-convert-carbon"></a>
### لا حاجة لتحويل الصيغ عند استعمال Carbon 

اذا كنت تقوم باستعلام باستخدام الطريقة `()whereDate` باستخدام التابع `()now` الخاص بـ Carbon، سيتم تلقائياً تحويل نتيجة التابع `()now` إلى النمط string دون الحاجة لاستخدام التابع `()toDateString`. 


```php
// بدلاً من هذه الطريقة
$todayUsers = User::whereDate('created_at', now()->toDateString())->get();
//  فقط قم باستخدامه بشكل مباشر
$todayUsers = User::whereDate('created_at', now())->get();
```

<a name="grouping-by-first-letter"></a>
### تجميع النتائج باستخدام أول حرف من الاسم

يمكنك تجميع نتائج استعلام Eloquent بأي شرط مخصص، فعلى سبيل المثال يمكنك تجميع المستخدمين بنائاً على أول حرف بأسمائهم بالأسلوب الآتي: 

```php
$users = User::all()->groupBy(function($item) {
    return $item->name[0];
});
```

<a name="never-update-the-column"></a>
### منع تغيير قيمة العامود

في حال كنت تود جعل أحد الأعمدة غير قابل للتغير بعد أن يتم ادخاله عند الانشاء يمكنك القيام بذلك بالاسلوب الآتي:


```php
class User extends Model
{
    public function setEmailAttribute($value)
    {
        if ($this->email) {
            return;
        }

        $this->attributes['email'] = $value;
    }
}
```

<a name="find-many"></a>
### الحصول على عدة سجلات باستخدام Find

يمكن للطريقة `()find` الحصول على عدة نتائج غبر تمرير عدة وسطاء: 


```php
// سيتم إعادة نتيجة واحدة
$user = User::find(1);
// سيتم إعادة مجموعة من النتائج
$users = User::find([1,2,3]);
```
```php
return Product::whereIn('id', $this->productIDs)->get();
// يمكنك القيام بذلك عوضاً عن  الطريقة السابقة
return Product::find($this->productIDs)
```

 تم تقديم الحيلة بواسطة  [tahiriqbalnajam@](https://twitter.com/tahiriqbalnajam/status/1436120403655671817)

يمكنك استخدام الطريقة `whereIntegerInRaw` مع نمط integer عوضاً عن `whereIn` لأنها **أسرع**. 

```php
Product::whereIn('id', range(1, 50))->get();
// بأسلوب أسرع
Product::whereIntegerInRaw('id', range(1, 50))->get();
```

 تم تقديم الحيلة بواسطة [sachinkiranti@](https://raisachin.com.np)


<a name="find-many-and-return-specific-columns"></a>
### الحصول على أعمدة محددة باستخدام Find 

كما يمكن للطريقة `()find` إعادة بعض الحقول فقط عبر تمرير أسماء الحقول كوسيط ثانٍ: 

```php
// سيتم إعادة اسم المستخدم والبريد الالكتروني للسجل 1
$user = User::find(1, ['first_name', 'email']);
// سيتم إعادة اسم المستخدم والبريد الاكتروني للمستخدمين 1 و 2 و3
$users = User::find([1,2,3], ['first_name', 'email']);
```
 تم تقديم الحيلة بواسطة [tahiriqbalnajam@](https://github.com/tahiriqbalnajam)


<a name="find-by-key"></a>
### البحث باستخدام المفتاح الأساسي

يمكنك أيضاً استعادة عدة سجلات عن طريق المفتاح الأساسي (primary key) في جدول فاعدة البيانات باستخدام الطريقة `()whereKey` (غالباً ما يكون المفتاح الأساسي للجدول هو `id`): 


```php
$users = User::whereKey([1,2,3])->get();
```

<a name="use-uuid-instead-of-auto-increment"></a>
### استخدم uuid بدلاً من الزيادة التلقائية

هل تفضل عدم استخدام الزيادة التلقائية في حقل id في لارافيل؟ يمكنك استخدام uuid عوضاً عنها

في ملف Migration:
```php
Schema::create('users', function (Blueprint $table) {
    // $table->increments('id');
    $table->uuid('id')->unique();
});
```

في ملف Model:
```php
class User extends Model
{
    public $incrementing = false;
    protected $keyType = 'string';

    protected static function boot()
    {
        parent::boot();

        User::creating(function ($model) {
            $model->setId();
        });
    }

    public function setId()
    {
        $this->attributes['id'] = Str::uuid();
    }
}
```

<a name="sub-selects-in-laravel-way"></a>
### التحديد الجزئي (Sub-Selects) بأسلوب لارافيل

من إصدار لارافيل 6 فما فوق يمكنك استخدام الطريقة `()addSelect` في استعلامات Eloquent لاداء حسابات اضافية لعمود مضاف. 


```php
return Destination::addSelect(['last_flight' => Flight::select('name')
    ->whereColumn('destination_id', 'destinations.id')
    ->orderBy('arrived_at', 'desc')
    ->limit(1)
])->get();
```

<a name="hide-some-columns"></a>
### إخفاء بعض الأعمدة

اذا أردت اخفاء بعض الأعمدة عند الاستعلام فأحد أسرع الطرق هي استعمال الطريقة `()makeHidden<-`على المجموعة (Collection) الناتجة: 


```php
$users = User::all()->makeHidden(['email_verified_at', 'deleted_at']);
```

<a name="exact-db-error"></a>
### التقاط أخطاء SQL

اذا أردت التقاط الاستثناءات الخاصة باستعلامات Eloquent يمكنك استخدام الصف `QueryException` بدلاً من صف الاستثناءات الافتراضي، ستصبح قادراً على التقاط الاستثناءات الخاصة بأخطاء SQL. 


```php
try {
    // Eloquent/SQL استعلام
} catch (\Illuminate\Database\QueryException $e) {
    if ($e->getCode() === '23000') { // (integrity constraint violation) انتهاك لقيد السلامة 
        return back()->withError('Invalid data');
    }
}
```

<a name="soft-deletes-with-query-builder"></a>
### الإزالة المؤقتة (Soft-Delete) باستخدام باني الاستعلامات

لا تنسى أن االاستعلام باستخدام Eloquent سيقوم تلقائياً باستبعاد السجلات المحذوفة مؤقتاً، أما في حالة باني الاستعلامات (Query Builder) فلن يقوم باستبعاد السجلات المحذوفة مؤقتاً. 


```php
// سيتم استبعاد السجلات المحذوفة مؤقتاً
$users = User::all();

// لن يتم استبعاد السجلات المحذوفة مؤقتاً
$users = User::withTrashed()->get();

// أيضاً لن يتم استبعاد السجلات المحذوفة مؤقتاً
$users = DB::table('users')->get();
```

<a name="good-old-sql-query"></a>
### تنفيذ استعلامات SQL 

اذا كنت تود تنفيذ استعلام SQL بسيط بدون استعادة أي نتيجة (مثل تنفيذ تعديل مخطط قاعدة البيانات) يمكنك استخدام `()DB::statement`.


```php
DB::statement('DROP TABLE users');
DB::statement('ALTER TABLE projects AUTO_INCREMENT=123');
```

<a name="use-db-transactions"></a>
### استعمل DB Transactions

اذا كنت تطبق عمليتين على قاعدة البيانات، وفي حال قامت الثانية باحداث خطأ، فمن المفترض أن تقوم بالتراجع عن التغيير الحاصل في العملية الأولى.

لهذا الغرض أنصح باستخدام `DB::transaction` فهي سهلة الاستعمال في لارافيل: 


```php
DB::transaction(function () {
    DB::table('users')->update(['votes' => 1]);

    DB::table('posts')->delete();
});
```

<a name="update-or-create"></a>
### التحديث أو الإنشاء 

اذا كنت تحتاج لتحديث سجل في حال وجوده، أو انشاءه في حال عدم وجوده يمكنك القيام بذلك باستخدام الطريقة `()updateOrCreate`: 


```php
// بدلاً من هذا الأسلوب
$flight = Flight::where('departure', 'Oakland')
    ->where('destination', 'San Diego')
    ->first();
if ($flight) {
    $flight->update(['price' => 99, 'discounted' => 1]);
} else {
	$flight = Flight::create([
	    'departure' => 'Oakland',
	    'destination' => 'San Diego',
	    'price' => 99,
	    'discounted' => 1
	]);
}
// يمكنك القيام بنفس العملية السابقة بطريقة أسهل
$flight = Flight::updateOrCreate(
    ['departure' => 'Oakland', 'destination' => 'San Diego'],
    ['price' => 99, 'discounted' => 1]
);
```

<a name="forget-cache-on-save"></a>
### ازالة المفتاح من الكاش عند الحفظ
اذا كان لديك مفتاح في الكاش (cache)، وليكن `posts` على سبيل المثال، يقوم باعطاء مجموعة (collection) وكنت تريد ازالة هذا المفتاح عند أي تخزين أو تحديث جديد يمكنك استعمال التابع الستاتيكي `saved` على النموذج الخاص بك كما يلي: 


```php
class Post extends Model
{
    // قم بإزالة المفتاح من الكاش عند أي تخزين أو تحديث
    public static function boot()
    {
        parent::boot();
        static::saved(function () {
           Cache::forget('posts');
        });
    }
}
```
تم تقديم هذه الحيلة بواسطة [pratiksh404@](https://github.com/pratiksh404)


<a name="change-format-of-created_at-and-updated_at"></a>
### تغيير صيغة حقلي created_at و updated_at

لتغيير صيغة الحقل `created_at` يمكنك اضافة طريقة في ملف النموذج بالشكل الآتي: 


```php
public function getCreatedAtFormattedAttribute()
{
   return $this->created_at->format('H:i d_M Y');
}
```
وبعدها يمكنك استخدام الصيغة بالشكل `entry->created_at_formatted$`، حيث سيتم إعادة قيمة `created_at` بالشكل `2020 Aug`ـ`23 04:19` على سبيل المثال.


كما يمكنك تغيير صيغة حقل `updated_at` بنفس الطريقة:
```php
public function getUpdatedAtFormattedAttribute()
{
   return $this->updated_at->format('H:i d_M Y');
}
```
وبعدها يمكنك استخدام الصيغة بالشكل `entry->updated_at_formatted$`، حيث سيتم إعادة قيمة `updated_at` بالشكل `2020 Aug`ـ`23 04:19` على سبيل المثال.

تم تقديم هذه الحيلة بواسطة [syofyanzuhad@](https://github.com/syofyanzuhad)


<a name="storing-array-type-into-json"></a>
### تخزين المصفوفات بصيغة JSON 

اذا كنت تمتلك حقل دخل يأخذ مصفوفة ويجب عليك تخزينه بصيغة JSON، يمكنك استخدام الخاصية `casts$` في النموذج الخاص بذلك الحقل.

على سبيل المثال الحقل `images` هنا هو متحول من نمط JSON: 


```php
protected $casts = [
    'images' => 'array',
];
```

بهذه الحالة سيتم تخزينه على شكل JSON ولكن عند طلبه سيتم تحويله لمصفوفة. 

تم تقديم هذه الحيلة بواسطة [pratiksh404@](https://github.com/pratiksh404)


<a name="make-a-copy-of-the-model"></a>
### استنساخ النموذج

اذا كان لديك نموذجين متشابهين (مثل: عنوان الدفع billing address، وعنوان الشحن shipping address) ويجب عليك نسخ احداهما للآخر، يمكنك استخدام الطريقة `()replicate` مع تغيير بعض الخواص بعدها. 


المثال من [توثيق لارافيل](https://laravel.com/docs/8.x/eloquent#replicating-models):

```php
$shipping = Address::create([
    'type' => 'shipping',
    'line_1' => '123 Example Street',
    'city' => 'Victorville',
    'state' => 'CA',
    'postcode' => '90001',
]);

$billing = $shipping->replicate()->fill([
    'type' => 'billing'
]);

$billing->save();
```


<a name="reduce-memory"></a>
### تخفيف الذاكرة

في بعض الأحيان قد تحتاج لتحميل كمية كبيرة من البيانات للذاكرة، على سبيل المثال:

```php
$orders = Order::all();
```

لكن هذه العملية قد تكون بطيئة في حال كنا نملك بيانات كبيرة الحجم، وذلك لأن لارافيل تقوم بتجهيزها ككائنات من نمط النموذج.
في مثل هذه الحالات قم باستخدام التابع اليدوي `()toBase` :


```php
$orders = Order::toBase()->get();
// StdClass مجموعة من نمط $orders سيعيد المتحول
```
باستخدام هذا الأسلوب سيتم استعادة البيانات من قاعدة البيانات، ولكن لن يتم تهيئتها ككائنات من نمط النموذج.
تذكر بأن هذا الأسلوب غالباً هو فكرة جيدة لتمرير مصفوفة من الحقول للطريقة get كي تمنع جلب كل الحقول من قاعدة البيانات.


<a name="force-query-without-fillableguarded"></a>
### التنفيذ القسري  للاستعلام مع تجاهل fillable و guarded

اذا قمت بانشاء مشروع لارافيل نمطي كبداية لمطورين اخرين، فلن تتحكم بما سيقومون بوضعه لاحقاً في الخاصية `fillable$` أو الخاصية `guarded$` الخاصة بالنماذج، يمكنك عندها استخدام الطريقة `()forceFill`. 



```php
$team->update(['name' => $request->name])
```

ماذا لو لم تكن الخاصية `name` ضمن `fillable$`؟ أو لو لم يكن هناك لا `fillable$` ولا `guarded$` على الإطلاق؟؟ 

الحل باستخدام الطريقة `()forceFill`: 
```php
$team->forceFill(['name' => $request->name])
```
بهذا الأسلوب سيتم تجاهل `fillable$` لهذا الاستعلام فقط وسيتم تنفيذه قسرياً. 


<a name="3-level-structure-of-parent-children"></a>
### بنى علائقية بثلاث مستويات

في حال كنت تمتلك بنية علائقية بثلاث مستويات، (مثل: التصنيفات في متجر الكتروني) وكنت تود عرض عدد المنتجات في المستوى الثالث (التصنيفات الجزئية) يمكنك استخدام ` with('yyy.yyy')` ومن ثم استخدام `()withCount`. 


في ملف المتحكم Controller:


```php
class HomeController extend Controller
{
    public function index()
    {
        $categories = Category::query()
            ->whereNull('category_id')
            ->with(['subcategories.subcategories' => function($query) {
                $query->withCount('products');
            }])->get();
    }
}
```

في ملف النموذج Model:

```php
class Category extends Model
{
    public function subcategories()
    {
        return $this->hasMany(Category::class);
    }
    
    public function products()
    {
    return $this->hasMany(Product::class);
    }
}
```

في ملف الواجهة:

```blade
<ul>
    @foreach($categories as $category)
        <li>
            {{ $category->name }}
            @if ($category->subcategories)
                <ul>
                @foreach($category->subcategories as $subcategory)
                    <li>
                        {{ $subcategory->name }}
                        @if ($subcategory->subcategories)
                            <ul>
                                @foreach ($subcategory->subcategories as $subcategory)
                                    <li>{{ $subcategory->name }} ({{ $subcategory->product_count }})</li>
                                @endforeach
                            </ul>
                        @endif
                    </li>
                @endforeach
                </ul>
            @endif
        </li>
    @endforeach           
</ul>
```


<a name="check-if-record-exists-or-show-404"></a>
### إظهار صفحة 404 عند اخفاق عملية البحث

عليك فقط القيام باستخدام الطريقة `()findOrFail` عوضاً عن الطريقة `()find`.

الأسلوب التقليدي القديم والطويل:

```php
$product = Product::find($id);
if (!$product) {
    abort(404);
}
$product->update($productDataArray);
```
الأسلوب الأفضل والأقصر باستخدام الطريقة `()findOrFail`:
```php
$product = Product::findOrFail($id); // shows 404 if not found
$product->update($productDataArray);
```


<a name="perform-any-action-on-failure"></a>
### تنفيذ أوامر عند اخفاق عملية البحث

عند البحث عن سجل، قد تود تنفيذ مجموعة تعليمات في حال لم يتم العثور عليه.
بالإضافة للطريقة `()firstOrFail<-` التي تقوم برمي استثناء 404، يمكنك تنفيذ أي مجموعة من التعليمات باستخدام الطريقة `()firstOr<-`:

```php
$model = Flight::where('legs', '>', 3)->firstOr(function () {
    //  مجموعة التعليمات التي تود تنفيذها في حالة عدم العثور على السجل
})
```


<a name="abort-if-condition-failed"></a>
### الإنهاء في حال فشل الشرط

الإنهاء العمليات (abort) في حال فشل اختبار شرط ما يمكنك استعمال التابع `()abort_if` بدلاً من هذا الأسلوب: 


```php
$product = Product::findOrFail($id);
if($product->user_id != auth()->user()->id){
    abort(403);
}
```
الأسلوب الأقصر باستخدام التابع `()abort_if`:

```php
/* abort_if(CONDITION, ERROR_CODE) */
$product = Product::findOrFail($id);
abort_if ($product->user_id != auth()->user()->id, 403)
```

<a name="perform-any-extra-steps-before-deleting-model"></a>
### انجاز خطوات إضافية قبل الحذف

يمكنك استخدام الطريقة `()Model::delete` في الطريقة `delete` عند التجاوز (overridde) للقيام ببعض الخطوات الإضافية قبل الحذف. 

```php
// App\Models\User.php في ملف

public function delete(){

	//الخطوات الإضافية المراد تنفيذها قبل الحذف
	
	//بعدها نقوم بتنفيذ عملية الحذف
	Model::delete();
}
```

تم تقديم هذه الحيلة بواسطة [back2Lobby@](https://github.com/back2Lobby)


<a name="fill-a-column-automatically-while-you-persist-data-to-the-database"></a>
### ملئ عمود تلقائياً أثناء الادخال

اذا كنت تود ملئ أحد الأعمدة تلقائياً أثناء عملية الادخال لقاعدة البيانات (مثل: slug) يمكنك استخدام الـ Observer الخاص بالنموذج عوضاً عن كتابتها بشكل يدوي بكل مرة. 


```php
use Illuminate\Support\Str;

class Article extends Model
{
    ...
    protected static function boot()
    {
        parent:boot();
        
        static::saving(function ($model) {
            $model->slug = Str::slug($model->title);
        });
    }
}
```

تم تقديم هذه الحيلة بواسطة [sky_0xs@](https://twitter.com/sky_0xs/status/1432390722280427521)


### Extra information about the query
You can call the `explain()` method on queries to know extra information about the query.
```php
Book::where('name', 'Ruskin Bond')->explain()->dd();
```

```php
Illuminate\Support\Collection {#5344
    all: [
        {#15407
            +"id": 1,
            +"select_type": "SIMPLE",
            +"table": "books",
            +"partitions": null,
            +"type": "ALL",
            +"possible_keys": null,
            +"key": null,
            +"key_len": null,
            +"ref": null,
            +"rows": 9,
            +"filtered": 11.11111164093,
            +"Extra": "Using where",
        },
    ],
}
```

Tip given by [@amit_merchant](https://twitter.com/amit_merchant/status/1432277631320223744)

### Using the doesntExist() method in Laravel
```php
// This works
if ( 0 === $model->where('status', 'pending')->count() ) {
}

// But since I don't care about the count, just that there isn't one
// Laravel's exists() method is cleaner.
if ( ! $model->where('status', 'pending')->exists() ) {
}

// But I find the ! in the statement above easily missed. The
// doesntExist() method makes this statement even clearer.
if ( $model->where('status', 'pending')->doesntExist() ) {
}
```

Tip given by [@ShawnHooper](https://twitter.com/ShawnHooper/status/1435686220542234626)

### Trait that you want to add to a few Models to call their boot() method automatically
If you have a Trait that you want to add to a few Models to call their `boot()` method automatically, you can call Trait's method as boot[TraitName]
```php
class Transaction extends  Model
{
    use MultiTenantModelTrait;
}
```

```php
class Task extends  Model
{
    use MultiTenantModelTrait;
}
```

```php
trait MultiTenantModelTrait
{
    // This method's name is boot[TraitName]
    // It will be auto-called as boot() of Transaction/Task
    public static function bootMultiTenantModelTrait()
    {
        static::creating(function ($model) {
            if (!$isAdmin) {
                $isAdmin->created_by_id = auth()->id();
            }
        })
    }
}
```

### There are two common ways of determining if a table is empty in Laravel
There are two common ways of determining if a table is empty in Laravel. Calling `exists()` or `count()` directly on the model!<br>
One returns a strict true/false boolean, the other returns an integer which you can use as a falsy in conditionals.
```php
public function index()
{
    if (\App\Models\User::exists()) {
        // returns boolean true or false if the table has any saved rows
    }
    
    if (\App\Models\User::count()) {
        // returns the count of rows in the table
    }
}
```

Tip given by [@aschmelyun](https://twitter.com/aschmelyun/status/1440641525998764041)

### How to prevent “property of non-object” error
```php
// BelongsTo Default Models
// Let's say you have Post belonging to Author and then Blade code:
$post->author->name;

// Of course, you can prevent it like this:
$post->author->name ?? ''
// or
@$post->author->name

// But you can do it on Eloquent relationship level:
// this relation will return an empty App\Author model if no author is attached to the post
public function author() {
    return $this->belongsTo('App\Author')->withDefault();
}
// or
public function author() {
    return $this->belongsTo('App\Author')->withDefault([
        'name' => 'Guest Author'
    ]);
}
```

Tip given by [@coderahuljat](https://twitter.com/coderahuljat/status/1440556610837876741)

### Get original attributes after mutating an Eloquent record
Get original attributes after mutating an Eloquent record you can get the original attributes by calling getOriginal()
```php
$user = App\User::first();
$user->name; // John
$user->name = "Peter"; // Peter
$user->getOriginal('name'); // John
$user->getOriginal(); // Original $user record
```

Tip given by [@devThaer](https://twitter.com/devThaer/status/1442133797223403521)

### A simple way to seed a database
A simple way to seed a database in Laravel with a .sql dump file
```php
DB::unprepared(
    file_get_contents(__DIR__ . './dump.sql')
);
```
Tip given by [@w3Nicolas](https://twitter.com/w3Nicolas/status/1447902369388249091)

### The crossJoinSub method of the query constructor
Using the CROSS JOIN subquery
```php
use Illuminate\Support\Facades\DB;

$totalQuery = DB::table('orders')->selectRaw('SUM(price) as total');

DB::table('orders')
    ->select('*')
    ->crossJoinSub($totalQuery, 'overall')
    ->selectRaw('(price / overall.total) * 100 AS percent_of_total')
    ->get();
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### Belongs to Many Pivot table naming

To determine the table name of the relationship's intermediate table, Eloquent will join the two related model names in alphabetical order. 

This would mean a join between `Post` and `Tag` could be added like this:

```php
class Post extends Model
{
    public $table = 'posts';

    public function tags()
    {
        return $this->belongsToMany(Tag::class);
    }
}
```
However, you are free to override this convention, and you would need to specify the join table in the second argument.

```php
class Post extends Model
{
    public $table = 'posts';

    public function tags()
    {
        return $this->belongsToMany(Tag::class, 'posts_tags');
    }
}
```
If you wish to be explicit about the primary keys you can also supply these as third and fourth arguments.
```php
class Post extends Model
{
    public $table = 'posts';

    public function tags()
    {
        return $this->belongsToMany(Tag::class, 'post_tag', 'post_id', 'tag_id');
    }
}
```
Tip given by [@iammikek](https://twitter.com/iammikek)

### Order by Pivot Fields
`BelongsToMany::orderByPivot()` allows you to directly sort the results of a BelongsToMany relationship query.
```php
class Tag extends Model
{
    public $table = 'tags';
}

class Post extends Model
{
    public $table = 'posts';

    public function tags()
    {
        return $this->belongsToMany(Tag::class, 'post_tag', 'post_id', 'tag_id')
            ->using(PostTagPivot::class)
            ->withTimestamps()
            ->withPivot('flag');
    }
}

class PostTagPivot extends Pivot
{
    protected $table = 'post_tag';
}

// Somewhere in the Controller
public function getPostTags($id)
{
    return Post::findOrFail($id)->tags()->orderByPivot('flag', 'desc')->get();
}
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### Find a single record from a database
The `sole()` method will return only one record that matches the criteria. If no such entry is found, then a `NoRecordsFoundException` will be thrown. If multiple records are found, then a `MultipleRecordsFoundException` will be thrown.
```php
DB::table('products')->where('ref', '#123')->sole();
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### Automatic records chunking
Similar to `each()` method, but easier to use. Automatically splits the result into parts (chunks).
```php
return User::orderBy('name')->chunkMap(fn ($user) => [
    'id' => $user->id,
    'name' => $user->name,
]), 25);
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### Updating the model without dispatching events
Sometimes you need to update the model without sending any events. We can now do this with the `updateQuietly()` method, which under the hood uses the `saveQuietly()` method.
```php
$flight->updateQuietly(['departed' => false]);
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### Periodic cleaning of models from obsolete records
To periodically clean models of obsolete records. With this trait, Laravel will do this automatically, only you need to adjust the frequency of the `model:prune` command in the Kernel class.
```php
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Prunable;
class Flight extends Model
{
    use Prunable;
    /**
     * Get the prunable model query.
     *
     * @return \Illuminate\Database\Eloquent\Builder
     */
    public function prunable()
    {
        return static::where('created_at', '<=', now()->subMonth());
    }
}
```
Also, in the pruning method, you can set the actions that must be performed before deleting the model:
```php
protected function pruning()
{
    // Removing additional resources,
    // associated with the model. For example, files.

    Storage::disk('s3')->delete($this->filename);
}
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### Immutable dates and casting to them
Laravel 8.53 introduces the `immutable_date` and `immutable_datetime` castes that convert dates to `Immutable`.

Cast to CarbonImmutable instead of a regular Carbon instance.
```php
class User extends Model
{
    public $casts = [
        'date_field'     => 'immutable_date',
        'datetime_field' => 'immutable_datetime',
    ];
}
```

Tip given by [@PascalBaljet](https://twitter.com/pascalbaljet)

### The findOrFail method also accepts a list of ids
The findOrFail method also accepts a list of ids. If any of these ids are not found, then it "fails".<br>
Nice if you need to retrieve a specific set of models and don't want to have to check that the count you got was the count you expected

```php
User::create(['id' => 1]);
User::create(['id' => 2);
User::create(['id' => 3]);

// Retrives the user...
$user = User::findOrFail(1);

// Throws a 404 because the user doesn't exist...
User::findOrFail(99);

// Retrives all 3 users...
$users = User::findOrFail([1, 2, 3]);

// Throws because it is unable to find *all* of the users
User::findOrFail([1, 2, 3, 99]);
```

Tip given by [@timacdonald87](https://twitter.com/timacdonald87/status/1457499557684604930)

### Prunable trait to automatically remove models from your database
New in Laravel 8.50: You can use the Prunable trait to automatically remove models from your database. For example, you can permanently remove soft deleted models after a few days.

```php
class File extends Model
{
    use SoftDeletes;
    
    // Add Prunable trait
    use Prunable;
    
    public function prunable()
    {
        // Files matching this query will be pruned
        return static::query()->where('deleted_at', '<=', now()->subDays(14));
    }
    
    protected function pruning()
    {
        // Remove the file from s3 before deleting the model
        Storage::disk('s3')->delete($this->filename);
    }
}

// Add PruneCommand to your schedule (app/Console/Kernel.php)
$schedule->command(PruneCommand::class)->daily();
```

Tip by [@Philo01](https://twitter.com/Philo01/status/1457626443782008834)

### withAggregate method
Under the hood, the withAvg/withCount/withSum and other methods in Eloquent use the 'withAggregate' method. You can use this method to add a subselect based on a relationship

```php
// Eloquent Model
class Post extends Model
{
    public function user()
    {
        return $this->belongsTo(User::class);
    }
}

// Instead of eager loading all users...
$posts = Post::with('user')->get();

// You can add a subselect to only retrieve the user's name...
$posts = Post::withAggregate('user', 'name')->get();

// This will add a 'user_name' attribute to the Post instance:
$posts->first()->user_name;
```

Tip given by [@pascalbaljet](https://twitter.com/pascalbaljet/status/1457702666352594947)

### Date convention
Using the `something_at` convention instead of just a boolean in Laravel models gives you visibility into when a flag was changed – like when a product went live.

```php
// Migration
Schema::table('products', function (Blueprint $table) {
    $table->datetime('live_at')->nullable();
});

// In your model
public function live()
{
    return !is_null($this->live_at);
}

// Also in your model
protected $dates = [
    'live_at'
];
```

Tip given by [@alexjgarrett](https://twitter.com/alexjgarrett/status/1459174062132019212)

### Eloquent multiple upserts
The upsert() method will insert or update multiple records.

- First array: the values to insert or update
- Second: unique identifier columns used in the select statement
- Third: columns that you want to update if the record exists

```php
Flight::upsert([
    ['departure' => 'Oakland', 'destination' => 'San Diego', 'price' => 99],
    ['departure' => 'Chicago', 'destination' => 'New York', 'price' => 150],
], ['departure', 'destination'], ['price']);
```

Tip given by [@mmartin_joo](https://twitter.com/mmartin_joo/status/1461591319516647426)

### Retrieve the Query Builder after filtering the results
To retrieve the Query Builder after filtering the results: you can use `->toQuery()`.<br>
The method internally use the first model of the collection and a `whereKey` comparison on the Collection models.
```php
// Retrieve all logged_in users
$loggedInUsers = User::where('logged_in', true)->get();

// Filter them using a Collection method or php filtering
$nthUsers = $loggedInUsers->nth(3);

// You can't do this on the collection
$nthUsers->update(/* ... */);

// But you can retrieve the Builder using ->toQuery()
if ($nthUsers->isNotEmpty()) {
    $nthUsers->toQuery()->update(/* ... */);
}
```

Tip given by [@RBilloir](https://twitter.com/RBilloir/status/1462529494917566465)

### Custom casts
You can create custom casts to have Laravel automatically format your Eloquent model data. Here's an example that capitalises a user's name when it is retrieved or changed.
```php
class CapitalizeWordsCast implements CastsAttributes
{
    public function get($model, string $key, $value, array $attributes)
    {
        return ucwords($value);
    }
    
    public function set($model, string $key, $value, array $attributes)
    {
        return ucwords($value);
    }
}

class User extends Model
{
    protected $casts = [
        'name'  => CapitalizeWordsCast::class,
        'email' => 'string',
    ]; 
}
```

Tip given by [@mattkingshott](https://twitter.com/mattkingshott/status/1462828232206659586)

### Order based on a related model's average or count
Did you ever need to order based on a related model's average or count?<br>
It's easy with Eloquent!
```php
public function bestBooks()
{
    Book::query()
        ->withAvg('ratings as average_rating', 'rating')
        ->orderByDesc('average_rating');
}
```

Tip given by [@mmartin_joo](https://twitter.com/mmartin_joo/status/1466769691385335815)

### Return transactions result
If you have a DB transaction and want to return its result, there are at least two ways, see the example
```php
// 1. You can pass the parameter by reference
$invoice = NULL;
DB::transaction(function () use (&$invoice) {
    $invoice = Invoice::create(...);
    $invoice->items()->attach(...);
})

// 2. Or shorter: just return trasaction result
$invoice = DB::transaction(function () {
    $invoice = Invoice::create(...);
    $invoice->items()->attach(...);
    
    return $invoice;
});
```

### Remove several global scopes from query
When using Eloquent Global Scopes, you not only can use MULTIPLE scopes, but also remove certain scopes when you don't need them, by providing the array to `withoutGlobalScopes()`<br>
[Link to docs](https://laravel.com/docs/8.x/eloquent#removing-global-scopes)

```php
// Remove all of the global scopes...
User::withoutGlobalScopes()->get();

// Remove some of the global scopes...
User::withoutGlobalScopes([
    FirstScope::class, SecondScope::class
])->get();
```

### Order JSON column attribute
With Eloquent you can order results by a JSON column attribute
```php
// JSON column example:
// bikes.settings = {"is_retired": false}
$bikes = Bike::where('athlete_id', $this->athleteId)
        ->orderBy('name')
        ->orderByDesc('settings->is_retired')
        ->get();
```

Tip given by [@brbcoding](https://twitter.com/brbcoding/status/1473353537983856643)

### Get single column's value from the first result
You can use `value()` method to get single column's value from the first result of a query

```php
// Instead of
Integration::where('name', 'foo')->first()->active;

// You can use
Integration::where('name', 'foo')->value('active');

// or this to throw an exception if no records found
Integration::where('name', 'foo')->valueOrFail('active')';
```

Tip given by [@justsanjit](https://twitter.com/justsanjit/status/1475572530215796744)

### Check if altered value changed key
Ever wanted to know if the changes you've made to a model have altered the value for a  key? No problem, simply reach for originalIsEquivalent.

```php
$user = User::first(); // ['name' => "John']

$user->name = 'John';

$user->originalIsEquivalent('name'); // true

$user->name = 'David'; // Set directly
$user->fill(['name' => 'David']); // Or set via fill

$user->originalIsEquivalent('name'); // false
```

Tip given by [@mattkingshott](https://twitter.com/mattkingshott/status/1475843987181379599)

### New way to define accessor and mutator

New way to define attribute accessors and mutators in Laravel 8.77:

```php
// Before, two-method approach
public function setTitleAttribute($value)
{
    $this->attributes['title'] = strtolower($value);
}
public function getTitleAttribute($value)
{
    return strtoupper($value);
}
 
// New approach
protected function title(): Attribute
{
    return new Attribute(
        get: fn ($value) => strtoupper($value),
        set: fn ($value) => strtolower($value),
}
```

Tip given by [@Teacoders](https://twitter.com/Teacoders/status/1473697808456851466)

### Another way to do accessors and mutators

In case you are going to use the same accessors and mutators in many models , You can use custom casts instead.

Just create a `class` that implements `CastsAttributes` interface. The class should have two methods, the first is `get` to specify how models should be retrieved from the database and the second is `set` to specify how the the value will be stored in the database.

```php
<?php

namespace App\Casts;

use Carbon\Carbon;
use Illuminate\Contracts\Database\Eloquent\CastsAttributes;

class TimestampsCast implements CastsAttributes
{
    public function get($model, string $key, $value, array $attributes)
    {
        return Carbon::parse($value)->diffForHumans();
    }

    public function set($model, string $key, $value, array $attributes)
    {
        return Carbon::parse($value)->format('Y-m-d h:i:s');
    }
}

```

Then you can implement the cast in the model class.

```php
<?php

namespace App\Models;

use Illuminate\Foundation\Auth\User as Authenticatable;
use App\Casts\TimestampsCast;
use Carbon\Carbon;


class User extends Authenticatable
{

    /**
     * The attributes that should be cast.
     *
     * @var array
     */
    protected $casts = [
        'updated_at' => TimestampsCast::class,
        'created_at' => TimestampsCast::class,
    ];
}

```
Tip given by [@AhmedRezk](https://github.com/AhmedRezk59)

### When searching for the first record, you can perform some actions
When searching for the first record, you want to perform some actions, when you don't find it. `firstOrFail()` throws a 404 Exception. <br>
You can use `firstOr(function() {})` instead. Laravel got your covered
```php
$book = Book::whereCount('authors')
            ->orderBy('authors_count', 'DESC')
            ->having('modules_count', '>', 10)
            ->firstOr(function() {
                // THe Sky is the Limit ...
                
                // You can perform any action here
            });
```

Tip given by [@bhaidar](https://twitter.com/bhaidar/status/1487757487566639113/)

### Directly convert created_at date to human readable format
Did you know you can directly convert created_at date to human readble format like 1 miniute ago, 1 month ago using diffForHumans() function. Laravel eloquent by default enables Carbon instance on created_at field.
```php
$post = Post::whereId($id)->first();
$result = $post->created_at->diffForHumans();

/* OUTPUT */
// 1 Minutes ago, 2 Week ago etc..as per created time
```

Tip given by [@vishal__2931](https://twitter.com/vishal__2931/status/1488369014980038662)

### Ordering by an Eloquent Accessor
Ordering by an Eloquent Accessor! Yes, that's doable. Instead of ordering by the accessor on the DB level, we order by the accessor on the returned Collection.
```php
class User extends Model
{
    // ...
    protected $appends = ['full_name'];
    
    public function getFullNameAttribute()
    {
        return $this->attribute['first_name'] . ' ' . $this->attributes['last_name'];
    }
    // ..
}
```

```php
class UserController extends Controller
{
    // ..
    public function index()
    {
        $users = User::all();
        
        // order by full_name desc
        $users->sortByDesc('full_name');
        
        // or
        
        // order by full_name asc
        $users->sortBy('full_name');
        
        // ..
    }
    // ..
}
```

`sortByDesc` and `sortBy` are methods on the Collection

Tip given by [@bhaidar](https://twitter.com/bhaidar/status/1490671693618053123)

### Check for specific model was created or found
If you want to check for specific model was created or found, use `wasRecentlyCreated` model attribute.
```php
$user = User::create([
    'name' => 'Oussama',
]);

// return boolean
return $user->wasRecentlyCreated;

// true for recently created
// false for found (already on you db)
```

Tip given by [@sky_0xs](https://twitter.com/sky_0xs/status/1491141790015320064)

### Laravel Scout with database driver
With laravel v9 you can use Laravel Scout (Search) with database driver. No more where likes!
```php
$companies = Company::search(request()->get('search'))->paginate(15);
```

Tip given by [@magarrent](https://twitter.com/magarrent/status/1493221422675767302)

### Make use of the value method on the query builder
Make use of the `value` method on the query builder to execute a more efficient query when you only need to retrieve a single column.
```php
// Before (fetches all columns on the row)
Statistic::where('user_id', 4)->first()->post_count;

// After (fetches only `post_count`)
Statistic::where('user_id', 4)->value('post_count');
```

Tip given by [@mattkingshott](https://twitter.com/mattkingshott/status/1493583444244410375)

### Pass array to where method
Laravel you can pass an array to the where method.
```php
// Instead of this
JobPost::where('company', 'laravel')
        ->where('job_type', 'full time')
        ->get();

// You can pass an array
JobPost::where(['company' => 'laravel',
                'job_type' => 'full time'])
        ->get();
```

Tip given by [@cosmeescobedo](https://twitter.com/cosmeescobedo/status/1495626752282234881)

### Return the primary keys from models collection
Did you know `modelsKeys()` eloquent collection method? It returns the primary keys from models collection.
```php
$users = User::active()->limit(3)->get();

$users->modelsKeys(); // [1, 2, 3]
```

Tip given by [@iamharis010](https://twitter.com/iamharis010/status/1495816807910891520)

### Force Laravel to use eager loading

If you want to prevent a lazy loading in your app, you only need to add following line to the `boot()` method in your `AppServiceProvider`

```php
Model::preventLazyLoading();
```
But, if you want to enable this feature only on your local development you can change above code on that:
```php
Model::preventLazyLoading(!app()->isProduction());
```
Tip given by [@CatS0up](https://github.com/CatS0up)

### Make all your models mass assignable

It is not a recommended approach for security reasons, but it is possible.

When you want do this, you don't need to set an empty `$guarded` array for every model, like this:

```php
protected $guarded = [];
```

You can do it from a single place, just add following line to the `boot()` method in your `AppServiceProvider`:

```php
Model::unguard();
```

Now, all your models are mass assignable.

Tip given by [@CatS0up](https://github.com/CatS0up)

### Hiding columns in select all statements

If you use Laravel v8.78 and MySQL 8.0.23 and onwards, you can define choosen columns as "invisible". Columns which are define as `invisible` will be hidden from the `select *` statements.

However, to do so, we must use a `invisible()` method in the migration, something like that:
```php
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

Schema::table('table', function (Blueprint $table) {
    $table->string('secret')->nullable()->invisible();
});
```

That's it! This will make chosen column hidden from `select *` statement.

Tip given by [@CatS0up](https://github.com/CatS0up)

### JSON Where Clauses
Laravel offers helpers to query JSON columns for databases that support them. <br>

Currently, MySQL 5.7+, PostgreSQL, SQL Server 2016, and SQLite 3.9.0 (using the JSON1 extension)

```php
// To query a json column you can use the -> operator
$users = User::query()
            ->where('preferences->dining->meal', 'salad')
            ->get();
// You can check if a JSON array contains a set of values
$users = User::query()
            ->whereJsonContains('options->languages', [
                'en', 'de'
               ])
            ->get();
// You can also query by the length a JSON array
$users = User::query()
            ->whereJsonLength('options->languages', '>', 1)
            ->get();
```

Tip given by [@cosmeescobedo](https://twitter.com/cosmeescobedo/status/1509663119311663124)

### Get all the column names for a table
```php
DB::getSchemaBuilder()->getColumnListing('users');
/*
returns [
    'id',
    'name',
    'email',
    'email_verified_at',
    'password',
    'remember_token',
    'created_at',
    'updated_at',
]; 
*/
```

Tip given by [@aaronlumsden](https://twitter.com/aaronlumsden/status/1511014229737881605)

### Compare the values of two columns
You can use `whereColumn` method to compare the values of two columns.

```php
return Task::whereColumn('created_at', 'updated_at')->get();
// pass a comparison operator
return Task::whereColumn('created_at', '>', 'updated_at')->get();
```

Tip given by [@iamgurmandeep](https://twitter.com/iamgurmandeep/status/1511673260353548294)

### Accessor Caching
As of Laravel 9.6, if you have a computationally intensive accessor, you can use the shouldCache method.

```php
public function hash(): Attribute
{
    return Attribute::make(
        get: fn($value) => bcrypt(gzuncompress($value)),
    )->shouldCache();
}
```

Tip given by [@cosmeescobedo](https://twitter.com/cosmeescobedo/status/1514304409563402244)

### New scalar() method
In Laravel 9.8.0, the `scalar()` method was added that allows you to retrieve the first column of the first row from the query result.

```php
// Before
DB::selectOne("SELECT COUNT(CASE WHEN food = 'burger' THEN 1 END) AS burgers FROM menu_items;")->burgers
// Now
DB::scalar("SELECT COUNT(CASE WHEN food = 'burger' THEN 1 END) FROM menu_items;")
```

Tip given by [@justsanjit](https://twitter.com/justsanjit/status/1514550185837408265)

### Select specific columns
To select specific columns on a model you can use the select method -- or you can pass an array directly to the get method!

```php
// Select specified columns from all employees
$employees = Employee::select(['name', 'title', 'email'])->get();
// Select specified columns from all employees
$employees = Employee::get(['name', 'title', 'email']);
```

Tip given by [@ecrmnn](https://twitter.com/ecrmnn/status/1516087672351203332)

### Chain conditional clauses to the query without writing if-else statements
The "when" helper in the query builder is🔥

You can chain conditional clauses to the query without writing if-else statements.

Makes your query very clear:

```php
class RatingSorter extends Sorter
{
    function execute(Builder $query)
    {
        $query
            ->selectRaw('AVG(product_ratings.rating) AS avg_rating')
            ->join('product_ratings', 'products.id', '=', 'product_ratings.product_id')
            ->groupBy('products.id');
            ->when(
                $this->direction === SortDirections::Desc,
                fn () => $query->orderByDesc('avg_rating')
                fn () => $query->orderBy('avg_rating'),
            );
        
        return $query;
    }
}
```

Tip given by [@mmartin_joo](https://twitter.com/mmartin_joo/status/1521461317940350976)