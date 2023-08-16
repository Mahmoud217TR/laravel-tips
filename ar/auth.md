## المصادقة (Auth)

⬆️ [العودة إلى القائمة الرئيسية](README.md#laravel-tips) ➡️ [المجموعات)](collections.md) ⬅️ [التالي (البريد)](mail.md)

- [تفقد عدة صلاحيات دفعة واحدة](#check-multiple-permissions-at-once)
- [التحقق من المستخدم مع عدة خيارات](#authenticate-users-with-more-options)
- [المزيد من الأحداث عند تسجيل مستخدم](#more-events-on-user-registration)
- [هل تعرف Auth::once()؟](#did-you-know-about-authonce)
- [تغيير رمز (API Token) عند تغيير كلمة المرور](#change-api-token-on-users-password-update)
- [تخطي الصلاحيات للمسؤول الخارق](#override-permissions-for-super-admin)

---


<h3 id="check-multiple-permissions-at-once">
تفقد عدة صلاحيات دفعة واحدة
</h3>

بالإضافة للمؤشر `@can` الخاصة بمحرك Blade، هل تعلم أنه بإمكانك تفقد عدة صلاحيات مرة واحدة باستخدام المؤشر `@canany`؟

```blade
@canany(['update', 'view', 'delete'], $post)
    // The current user can update, view, or delete the post
@elsecanany(['create'], \App\Post::class)
    // The current user can create a post
@endcanany
```
> ملاحظة من المترجم: يعمل المؤشر canany عند تحقق شرط واحد فقط من الشروط.

---


<h3 id="authenticate-users-with-more-options">
التحقق من المستخدم مع عدة خيارات
</h3>

اذا كنت تريد التحقق من المستخدمين الفعالين `activated` على سبيل المثال، بكل بساطة نمرر وسيط اضافي للدالة `Auth::attempt`.

لا حاجة لبرمجية وسيطة معقدة أو global scope.

```php
Auth::attempt(
    [
        ...$request->only('email', 'password'),
        fn ($query) => $query->whereNotNull('activated_at')
    ],
    $this->boolean('remember')
);
```

النصيحة مقدمة من [@LukeDowning19](https://twitter.com/LukeDowning19)

---


<h3 id="more-events-on-user-registration">
المزيد من الأحداث عند تسجيل مستخدم
</h3>

هل تريد تنفيذ عدة عمليات بعد تسجيل مستخدم جديد في التطبيق؟ توجه إلى الملف `app/Providers/EventServiceProvider.php` وقم بإضافة العديد من صفوف المتنصتات (Listeners) وبعدها قم بتطبيق الدالة `handle` مع غرض من الصف `event->user`.


```php
class EventServiceProvider extends ServiceProvider
{
    protected $listen = [
        Registered::class => [
            SendEmailVerificationNotification::class,

            // You can add any Listener class here
            // With handle() method inside of that class
        ],
    ];
```

---


<h3 id="did-you-know-about-authonce">
هل تعرف Auth::once()؟
</h3>


You can login with user only for ONE REQUEST, using method `Auth::once()`.
No sessions or cookies will be utilized, which means this method may be helpful when building a stateless API.

```php
if (Auth::once($credentials)) {
    //
}
```

<h3 id="change-api-token-on-users-password-update">
تغيير رمز (API Token) عند تغيير كلمة المرور
</h3>


من المناسب تغيير رمز (API Token) عند تغيير المستخدم لكلمة مروره.

في المودل الخاص بالمستخدم:

```php
protected function password(): Attribute
{
    return Attribute::make(
            set: function ($value, $attributes) {
                $value = $value;
                $attributes['api_token'] = Str::random(100);
            }
        );
}
```

---



<h3 id="override-permissions-for-super-admin">
تخطي الصلاحيات للمسؤول الخارق
</h3>

اذا كنت قد قمت بتعريف بوابات الحماية ولكن تريد تجاوز جميع الصلاحيات للمسؤول الخارق، واعطاءه كل الصلاحيات، يمكنك التجاوز باستخدام `Gate::before` في ملف `AuthServiceProvider.php`:


```php
// Intercept any Gate and check if it's super admin
Gate::before(function($user, $ability) {
    if ($user->is_super_admin == 1) {
        return true;
    }
});

// Or if you use some permissions package...
Gate::before(function($user, $ability) {
    if ($user->hasPermission('root')) {
        return true;
    }
});
```

اذا كنت تنفيذ أي شيئ في البوابة عند عدم وجود أي مستخدم، يجب عليك الاشارة إلى `$user` والسماح لقيمته بأن تكون `null`. على سبيل المثال ليكن لديك دور مسمى مجهول، فللمستخدمين الذين لم يقومو بتسجيل الدخول:


```php
Gate::before(function (?User $user, $ability) {
    if ($user === null) {
        $role = Role::findByName('Anonymous');
        return $role->hasPermissionTo($ability) ? true : null;
    }
    return $user->hasRole('Super Admin') ? true : null;
});
```

