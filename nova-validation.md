### Nova | Validation

#### Resource | Validation | Combination of FK fields must be unique  
```php

// A machine has a type and a color, both key's to other tables. The combination must be unique in the machine table.

BelongsTo::make('Color')
    ->creationRules([
        Rule::unique('machine', 'color_id')
            ->where('color_id', $request->input('color'))
    ])
    ->updateRules([
        Rule::unique('machine', 'color_id')
            ->where('color_id', $request->input('color'))
            ->ignore($request->resourceId)
    ]),
BelongsTo::make('Type')
    ->creationRules([
        Rule::unique('machine', 'type_id')
            ->where('type_id', $request->input('type'))
    ])
    ->updateRules([
        Rule::unique('machine', 'type_id')
            ->where('type_id', $request->input('type'))
            ->ignore($request->resourceId)
    ]),
```