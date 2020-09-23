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
