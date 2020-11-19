### Test code samples for Laravel Nova

#### Test Resource Action
```php
    public function test_a_nova_action_that_changes_name_and_role_of_a_user()
    {
        // Let's use the User model in this demo
        $user = factory(User::class)->create(['role' => 'admin']);

        // Define the values of the fields you normally set in the action pop-up
        $valuesActionFields = ['new_role' => 'super-admin', 'name' => 'Marcus'];
        $fields = new ActionFields(collect($valuesActionFields), collect());
        
        // Run action on the model with the fields
        $novaAction = new MyNovaAction();
        $return = $novaAction->handle($fields, collect([$user]));

        $this->assertEquals('User has a new role and name.', $return['message'], 'The action MyNovaAction dit not return the expected message.');

        $this->assertEquals('super-admin', $user->role, 'The action MyNovaAction failed to set the new role on the user.');

        $this->assertEquals('Marcus', $user->name, 'The action MyNovaAction failed to set the new name on the user.');
    }
```
