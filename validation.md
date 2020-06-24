### Validation


```php
    // Makes example_field required if other_field has a specific value
    public function rules()
    {
        return [
            'example_field' => 'required_if:other_field,has_this_value',
            'other_field' => 'required'
        ]
    }
```
