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
        $value = '';

        if (in_array($key, $this->encryptable)) {
            if (parent::getAttribute($key)) {
                $value = Crypt::decrypt(parent::getAttribute($key));
            }
        }

        return $value;
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
