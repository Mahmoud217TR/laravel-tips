## أوامر Artisan

⬆️ [العودة إلى القائمة الرئيسية](README.md#laravel-tips) ➡️ [السابق (البريد)](mail.md) ⬅️ [التالي (المصانع)](factories.md)

- [مدخلات أوامر Artisan](#artisan-command-parameters)
- [تنفيذ تعبير (Closure) بعد تشغيل الأمر بدون أخطاء أو إذا كانت هناك أخطاء](#execute-a-closure-after-command-runs-without-errors-or-has-any-errors)
- [تنفيذ أوامر Artisan في بيئة محددة](#run-artisan-commands-on-specific-environments)
- [وضع الصيانة](#maintenance-mode)
- [المساعدة بأوامر Artisan](#artisan-command-help)
- [نسخة لارافيل بدقة](#exact-laravel-version)
- [شغل أوامر Artisan من أي مكان](#launch-artisan-command-from-anywhere)
- [اخفاء الأوامر المخصصة](#hide-your-custom-command)
- [الدالة Skip](#skip-method)

---


<h3 id="artisan-command-parameters">
مدخلات أوامر Artisan
</h3>

عند انشاء أوامر Artisan، يمكنك طلب الدخل بطرق متعددة:

`$this->confirm()`
`$this->anticipate()`
`$this->choice()`

```php
// Yes or no?
if ($this->confirm('Do you wish to continue?')) {
    //
}

// Open question with auto-complete options
$name = $this->anticipate('What is your name?', ['Taylor', 'Dayle']);

// One of the listed options with default index
$name = $this->choice('What is your name?', ['Taylor', 'Dayle'], $defaultIndex);
```

---


<h3 id="execute-a-closure-after-command-runs-without-errors-or-has-any-errors">
تنفيذ تعبير (Closure) بعد تشغيل الأمر بدون أخطاء أو إذا كانت هناك أخطاء
</h3>

باستخدام مجدول لارافيل (Laravel scheduler) يمكنك تنفيذ تعبير (Closure) عند تنفيذ أمر Artisan بدون أخطاء باستخدام الدالة `onSuccess` وأيضاً عند حدوث مشكلة باستخدام الدالة `onFailure`.

```php
protected function schedule(Schedule $schedule)
{
    $schedule->command('newsletter:send')
        ->mondays()
        ->onSuccess(fn () => resolve(SendNewsletterSlackNotification::class)->handle(true))
        ->onFailure(fn () => resolve(SendNewsletterSlackNotification::class)->handle(false));
}
```

النصيحة مقدمة من [@wendell_adriel](https://twitter.com/wendell_adriel)

---


<h3 id="run-artisan-commands-on-specific-environments">
تنفيذ أوامر Artisan في بيئة محددة
</h3>

يمكنك التحكم في مجدول لارافيل (Laravel scheduled). قم بتحديد البيئة التي يعمل عليها بأريحية.

```php
$schedule->command('reports:send')
    ->daily()
    ->environments(['production', 'staging']);
```

النصيحة مقدمة من [@LaraShout](https://twitter.com/LaraShout)

---


<h3 id="maintenance-mode">
وضع الصيانة
</h3>

اذا كنت تريد تفعيل وضع الصيانة في تطبيقك، نفذ الأمر التالي:

```bash
php artisan down
```
عندها سيرى الناس الصفحة الافتراضية للـ 503.

يمكنك في نسخة لارافيل 8 والنسخ الأحدث:

- المسار الذي يتم تحويل المستخدمين له.
- الواجهة التي يجب أن تعرض.
- العبارة السرية لتجاوز وضع الصيانة.
- إعادة تحميل الصفحة كل X ثانية.


```bash
php artisan down --redirect="/" --render="errors::503" --secret="1630542a-246b-4b66-afa1-dd72a4c43515" --retry=60
```

للنسخة الأقدم من لارافيل 8:

- الرسالة التي ستعرض
- إعادة تحميل الصفحة كل X ثانية.
- السماح بالوصول لعنوان IP معين.

```bash
php artisan down --message="Upgrading Database" --retry=60 --allow=127.0.0.1
```

عند الانتهاء من الصيانة:

```bash
php artisan up
```

---


<h3 id="artisan-command-help">
المساعدة بأوامر Artisan
</h3>

لتفقد الخيارات في أمر Artisan، قم بتشغيل الأمر مع الخيار `help` كمثال عند كتابة:
```shell
php artisan make:model --help
```

ستظهر لك الخيارات:

```
Options:
  -a, --all             Generate a migration, seeder, factory, policy, resource controller, and form request classes for the model
  -c, --controller      Create a new controller for the model
  -f, --factory         Create a new factory for the model
      --force           Create the class even if the model already exists
  -m, --migration       Create a new migration file for the model
      --morph-pivot     Indicates if the generated model should be a custom polymorphic intermediate table model
      --policy          Create a new policy for the model
  -s, --seed            Create a new seeder for the model
  -p, --pivot           Indicates if the generated model should be a custom intermediate table model
  -r, --resource        Indicates if the generated controller should be a resource controller
      --api             Indicates if the generated controller should be an API resource controller
  -R, --requests        Create new form request classes and use them in the resource controller
      --test            Generate an accompanying PHPUnit test for the Model
      --pest            Generate an accompanying Pest test for the Model
  -h, --help            Display help for the given command. When no command is given display help for the list command
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi|--no-ansi  Force (or disable --no-ansi) ANSI output
  -n, --no-interaction  Do not ask any interactive question
      --env[=ENV]       The environment the command should run under
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
```

---


<h3 id="exact-laravel-version">
نسخة لارافيل بدقة
</h3>

يمكنك تحديد نسخة لارافيل بالتفصيل باستعمال الأمر:

```shell
php artisan --version
```

---


<h3 id="launch-artisan-command-from-anywhere">
شغل أوامر Artisan من أي مكان
</h3>

يمكن تشغيل أمر Artisan من أي مكان في تطبيقك ومع مدخلات، باستخدام دالة call في واجهة Artisan:

```php
Route::get('/foo', function () {
    $exitCode = Artisan::call('email:send', [
        'user' => 1, '--queue' => 'default'
    ]);

    //
});
```

---


<h3 id="hide-your-custom-command">
اخفاء الأوامر المخصصة
</h3>

اذا كنت لا تريد أن تظهر أمراً في لائحة أوامر Artisan ضع الخاصية `hidden` بالقيمة `true`

```php
class SendMail extends Command
{
    protected $signature = 'send:mail';
    protected $hidden = true;
}
```

لن يظهر الأمر `send:mail` في لائحة الأوامر عند كتابة `php artisan`.

النصيحة مقدمة من [@sky_0xs](https://twitter.com/sky_0xs/status/1487921500023832579)

---


<h3 id="skip-method">
الدالة Skip
</h3>
الدالة Skip في مجدول لارافيل (Laravel scheduler) تمكنك تجاهل تنفيذ أمر.
```php
$schedule->command('emails:send')->daily()->skip(function () {
    return Calendar::isHoliday();
});
```

> تعليق من المترجم: سيتم تنفيذ الأمر بشكل يومي ويتجاهل أيام العطل المعادة من التعبير المنفذ (بالتالي الدالة skip تساعد على تجاهل الأيام أو الفترات في مجدول لارافيل)

النصيحة مقدمة من [@cosmeescobedo](https://twitter.com/cosmeescobedo/status/1494503181438492675)
