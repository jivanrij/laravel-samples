### Encryption


#### Encrypting fields of a model

Add the following Trait to your application. This Trait encrypts and decrypts all the fields in the encryptable array you need to define in the model.

```php
namespace App\Traits;

use Illuminate\Support\Facades\Crypt;

trait Encryptable
{
    public function getAttribute($key)
    {
        if (in_array($key, $this->encryptable)) {
            if (parent::getAttribute($key)) {
                return Crypt::decrypt(parent::getAttribute($key));
            }
        }

        return parent::getAttribute($key);
    }

    public function setAttribute($key, $value)
    {
        if (in_array($key, $this->encryptable)) {
            $value = Crypt::encrypt($value);
        }

        return parent::setAttribute($key, $value);
    }
}
```

Add the following to your model

```php
class PersonalData extends Model
{
    use Encryptable;

    protected $encryptable = [
        'contact_person',
        'email',
        'name',
    ];
}
```

#### Encrypting users.email

You cannot store the encrypted email in a string field, therefor you need a text field. But for the users.email field you do need a unique. Migrations cannot put a unique on a text field. Therefor, remove the unique, and apply it separatly.
```php
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->text('email');
        });

        DB::unprepared('ALTER TABLE users ADD UNIQUE key users_email_unique (email(64))');
    }
```
