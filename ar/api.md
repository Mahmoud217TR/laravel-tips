## واجهة برمجة التطبيقات (API)

⬆️ [العودة إلى القائمة الرئيسية](README.md#laravel-tips) ➡️ [السابق (السجل والتصحيح)](log-and-debug.md) ⬅️ [التالي (أخرى)](other.md)

- [مصادر واجهة التطبيقات (API Resources) مع أو بدون "بيانات"؟ ](#api-resources-with-or-without-data)
- [العد الشرطي للعلاقات في مصادر واجهة برمجة التطبيقات (API Resources)](#conditional-relationship-counts-on-api-resources)
- [إعادة رد "Everything went ok"](#api-return-everything-went-ok)
- [تجنب مشكلة N+1 في استعلامات مصادر واجهة التطبيقات (API Resources)](#avoid-n1-queries-in-api-resources)
- [الحصول على Bearer Token من ترويسة التفويض (Authorization Header)](#get-bearer-token-from-authorization-header)
- [ترتيب نتائج واجهة التطبيقات (API)](#sorting-your-api-results)
- [تخصيص معالج الاستثناءات (Exception Handler) لواجهة برمجة التطبيقات (API Resources)](#customize-exception-handler-for-api)
- [إجبار الرد بتنسيق JSON لطلبات واجهة برمجة التطبيقات(API Requests)](#force-json-response-for-api-requests)
- [إصدارات واجهة برمجة التطبيقات (API Versioning).](#api-versioning)

---


<h3 id="api-resources-with-or-without-data">
مصادر واجهة التطبيقات (API Resources) مع أو بدون "بيانات"؟
</h3>

إذا كنت تستخدم مصادر واجهة برمجة التطبيقات (API Resources) لاسترجاع البيانات، فسيتم تغليفها تلقائيًا بالمعلومات. إذا كنت ترغب في إزالتها، قم بإضافة التعليمة التالية:

`JsonResource::withoutWrapping();`

في الملف:

`app/Providers/AppServiceProvider.php`.


```php
class AppServiceProvider extends ServiceProvider
{
    public function boot()
    {
        JsonResource::withoutWrapping();
    }
}
```

النصيحة مقدمة من [@phillipmwaniki](https://twitter.com/phillipmwaniki/status/1445230637544321029)

---


<h3 id="conditional-relationship-counts-on-api-resources">
العد الشرطي للعلاقات في مصادر واجهة برمجة التطبيقات (API Resources)
</h3>

يمكنك تضمين العد للعلاقة في الرد الخاص بالمصدر (Resources) بشكل شرطي باستخدام طريقة whenCounted. من خلال القيام بذلك، لن يتم تضمين السمة إذا كانت علاقة حساب العدد العلاقات غير مفقودة.

```php
public function toArray($request)
{
     return [
          'id' => $this->id,
          'name' => $this->name,
          'email' => $this->email,
          'posts_count' => $this->whenCounted('posts'),
          'created_at' => $this->created_at,
          'updated_at' => $this->updated_at,
     ];
}
```

النصيحة مقدمة من [@mvpopuk](https://twitter.com/mvpopuk/status/1570480977507504128)

---


<h3 id="api-return-everything-went-ok">
إعادة رد "Everything went ok"
</h3>


إذا كان لديك نقطة نهاية API تقوم ببعض العمليات لكنها ليست لديها استجابة، وتريد فقط إرجاع "Everything went ok"، فيمكنك إرجاع رمز الحالة 204 "بدون محتوى". في لارافيل، يمكنك القيام بذلك بسهولة عن طريق:

`return response()->noContent();`

```php
public function reorder(Request $request)
{
    foreach ($request->input('rows', []) as $row) {
        Country::find($row['id'])->update(['position' => $row['position']]);
    }

    return response()->noContent();
}
```

---


<h3 id="avoid-n1-queries-in-api-resources">
تجنب مشكلة N+1 في استعلامات مصادر واجهة التطبيقات (API Resources)
</h3>

يمكنك تجنب مشكلة N+1 في استعلامات مصادر واجهة التطبيقات عن طريق استعمال الطريقة:

`whenLoaded()`

سيتم إضافة القسم فقط إذا تم تحميله بالفعل في نموذج الموظف.

بدون الطريقة 

`whenLoaded()`

سيكون هناك دائمًا استعلام للقسم.
```php
class EmployeeResource extends JsonResource
{
    public function toArray($request): array
    {
        return [
            'id' => $this->uuid,
            'fullName' => $this->full_name,
            'email' => $this->email,
            'jobTitle' => $this->job_title,
            'department' => DepartmentResource::make($this->whenLoaded('department')),
        ];
    }
}
```

النصيحة مقدمة من [@mmartin_joo](https://twitter.com/mmartin_joo/status/1473987501501071362)


---


<h3 id="get-bearer-token-from-authorization-header">
الحصول على Bearer Token من ترويسة التفويض (Authorization Header)
</h3>

إن الدالة:

`bearerToken()`

مفيدة عند العمل على واجهات التطبيقات وترغب في الوصول إلى رمز الـBearer Token من رأس التفويض (Authorization header).

```php
// Don't parse API headers manually like this:
$tokenWithBearer = $request->header('Authorization');
$token = substr($tokenWithBearer, 7);

//Do this instead:
$token = $request->bearerToken();
```

النصيحة مقدمة من [@iamharis010](https://twitter.com/iamharis010/status/1488413755826327553)

---


<h3 id="sorting-your-api-results">
ترتيب نتائج واجهة التطبيقات (API)
</h3>


فرز واجهة برمجة التطبيقات (API) بعمود واحد، مع التحكم في الاتجاه.

```php
// Handles /dogs?sort=name and /dogs?sort=-name
Route::get('dogs', function (Request $request) {
    // Get the sort query parameter (or fall back to default sort "name")
    $sortColumn = $request->input('sort', 'name');

    // Set the sort direction based on whether the key starts with -
    // using Laravel's Str::startsWith() helper function
    $sortDirection = Str::startsWith($sortColumn, '-') ? 'desc' : 'asc';
    $sortColumn = ltrim($sortColumn, '-');

    return Dog::orderBy($sortColumn, $sortDirection)
        ->paginate(20);
});
```

نفعل نفس الأمر لعدة أعمدة، على سبيل المقال:

(?sort=name,-weight)

```php
// Handles ?sort=name,-weight
Route::get('dogs', function (Request $request) {
    // Grab the query parameter and turn it into an array exploded by ,
    $sorts = explode(',', $request->input('sort', ''));

    // Create a query
    $query = Dog::query();

    // Add the sorts one by one
    foreach ($sorts as $sortColumn) {
        $sortDirection = Str::startsWith($sortColumn, '-') ? 'desc' : 'asc';
        $sortColumn = ltrim($sortColumn, '-');

        $query->orderBy($sortColumn, $sortDirection);
    }

    // Return
    return $query->paginate(20);
});
```

---


<h3 id="customize-exception-handler-for-api">
تخصيص معالج الاستثناءات (Exception Handler) لواجهة برمجة التطبيقات (API Resources)
</h3>

#### لاصدار لارافيل 8 والإصدارات الأقدم:

توجد الطريقة

 `render()`

 في الصف
 
 `App\Exceptions`

```php
   public function render($request, Exception $exception)
    {
        if ($request->wantsJson() || $request->is('api/*')) {
            if ($exception instanceof ModelNotFoundException) {
                return response()->json(['message' => 'Item Not Found'], 404);
            }

            if ($exception instanceof AuthenticationException) {
                return response()->json(['message' => 'unAuthenticated'], 401);
            }

            if ($exception instanceof ValidationException) {
                return response()->json(['message' => 'UnprocessableEntity', 'errors' => []], 422);
            }

            if ($exception instanceof NotFoundHttpException) {
                return response()->json(['message' => 'The requested link does not exist'], 400);
            }
        }

        return parent::render($request, $exception);
    }
```

#### في الاصادرا 9 من لارافيل والاصدارات الأحدث:

توجد الدالة

`register()`

في الصف

`App\Exceptions`

```php
    public function register()
    {
        $this->renderable(function (ModelNotFoundException $e, $request) {
            if ($request->wantsJson() || $request->is('api/*')) {
                return response()->json(['message' => 'Item Not Found'], 404);
            }
        });

        $this->renderable(function (AuthenticationException $e, $request) {
            if ($request->wantsJson() || $request->is('api/*')) {
                return response()->json(['message' => 'unAuthenticated'], 401);
            }
        });
        $this->renderable(function (ValidationException $e, $request) {
            if ($request->wantsJson() || $request->is('api/*')) {
                return response()->json(['message' => 'UnprocessableEntity', 'errors' => []], 422);
            }
        });
        $this->renderable(function (NotFoundHttpException $e, $request) {
            if ($request->wantsJson() || $request->is('api/*')) {
                return response()->json(['message' => 'The requested link does not exist'], 400);
            }
        });
    }
```

النصيحة مقدمة من [Feras Elsharif](https://github.com/ferasbbm)

---


<h3 id="force-json-response-for-api-requests">
إجبار الرد بتنسيق JSON لطلبات واجهة برمجة التطبيقات(API Requests)
</h3>


إذا قمت ببناء واجهة برمجة تطبيقات (API) وواجهت خطأ عندما لا تحتوي الطلبات على الترويسة `Accept: application/JSON`، سيتم رد الخطأ بتنسيق HTML أو تحويل على مسارات واجهة البرمجة، لذا يمكننا تجنب ذلك من خلال إجبار جميع استجابات واجهة البرمجة لتكون بتنسيق JSON.

الخطوة الأولى انشاء برمجية وسيطة (Middleware) بالأمر التالي:

```console
php artisan make:middleware ForceJsonResponse
```

قم بكتابة الكود التالي في دالة Handle في ملف `App/Http/Middleware/ForceJsonResponse.php`

```php
public function handle($request, Closure $next)
{
    $request->headers->set('Accept', 'application/json');
    return $next($request);
}
```

ثانياً، قم بتسجيل البرمجية الوسيطة (Middleware) في الملف `app/Http/Kernel.php`
```php
protected $middlewareGroups = [
    'api' => [
        \App\Http\Middleware\ForceJsonResponse::class,
    ],
];
```

النصيحة مقدمة من [Feras Elsharif](https://github.com/ferasbbm)

---


<h3 id="api-versioning">
إصدارات واجهة برمجة التطبيقات (API Versioning).
</h3>

#### متى يجب إصدار النسخة؟

عند العمل على مشروع قد يكون لديه إصدارات متعددة في المستقبل أو تحتوي نقاط النهاية (Endpoints) على تغيير مؤثر مثل تغيير في تنسيق بيانات الرد، وترغب في ضمان إبقاء الإصدارات السابقة لواجهة البرمجة التطبيقية تعمل عند إجراء تغييرات على الكود.

#### تغيير ملفات المسار الافتراضي


الخطوة الأولى هي تغيير خريطة المسار في الملف `App\Providers\RouteServiceProvider`، لنبدأ:


#### للإصدار الثامن من لارافيل والإصدارات الأحدث:

قم بإضافة الخاصية `ApiNamespace`

```php
/**
 * @var string
 *
 */
protected string $ApiNamespace = 'App\Http\Controllers\Api';
```

ضمن الدالة `boot` قم بإضافة الكود التالي:

```php
$this->routes(function () {
     Route::prefix('api/v1')
        ->middleware('api')
        ->namespace($this->ApiNamespace.'\\V1')
        ->group(base_path('routes/API/v1.php'));
        }

    //for v2
     Route::prefix('api/v2')
            ->middleware('api')
            ->namespace($this->ApiNamespace.'\\V2')
            ->group(base_path('routes/API/v2.php'));
});
```

#### لإصدار لارافيل 7 والإصدارات الأقدم:

قم بإضافة الخاصية `ApiNamespace`

```php
/**
 * @var string
 *
 */
protected string $ApiNamespace = 'App\Http\Controllers\Api';
```

ضمن الدالة `map` قم بإضافة الكود التالي:

```php
// remove this $this->mapApiRoutes();
    $this->mapApiV1Routes();
    $this->mapApiV2Routes();
```

قم بإضافة الدوال التالية:

```php
  protected function mapApiV1Routes()
    {
        Route::prefix('api/v1')
            ->middleware('api')
            ->namespace($this->ApiNamespace.'\\V1')
            ->group(base_path('routes/Api/v1.php'));
    }

  protected function mapApiV2Routes()
    {
        Route::prefix('api/v2')
            ->middleware('api')
            ->namespace($this->ApiNamespace.'\\V2')
            ->group(base_path('routes/Api/v2.php'));
    }
```

#### تنسيق الإصدار في مجلد التحكم (Controller Folder Versioning)

```
Controllers
└── Api
    ├── V1
    │   └──AuthController.php
    └── V2
        └──AuthController.php
```

#### تنسيق ملف المسارات (Route File Versioning).

```
routes
└── Api
   │    └── v1.php
   │    └── v2.php
   └── web.php
```

النصيحة مقدمة من [Feras Elsharif](https://github.com/ferasbbm)
