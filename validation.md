### Validation



```
// Makes a password optional, but when used, it need to be the same as the password_confirmation field
'password' => 'nullable|required_with:password_confirmation|confirmed', // optional if you want an error on the confirmation field
'password_confirmation' => 'required_with:password'
```

```
// Makes example_field required if other_field has a specific value
'example_field' => 'required_if:other_field,has_this_value',
'other_field' => 'required'
```
