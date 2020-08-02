### Eloquent | Examples


#### Relations

A post can belong to many tags, belongs to one user and has many comments refering to it. 
```php
// post.user_id

// post_tag.post_id
// post_tag.tag_id

// comment.post_id

class Post extends Model {
    public function tags()
    {
        return $this->belongsToMany(Tags::class);
    }
    public function user()
    {
        return $this->belongsTo(User::class);
    }
    public function comments()
    {
        return $this->hasMany(Comment::class);
    }
}
```

A phone belongs to a user.
```php
// phone.user_id
class Phone extends Model {
    public function user()
    {
        return $this->belongsTo(User::class);
    }
}
```

A comment belongs to a post.
```php
// comment.post_id
class Comment extends Model {
    public function post()
    {
        return $this->belongsTo(Post::class);
    }
}
```

A user has many posts and has one phone.
```php
// phone.user_id
// post.user_id
class User extends Model {
    public function posts()
    {
        return $this->hasMany(Post::class);
    }
    public function phone()
    {
        return $this->hasOne(Phone::class);
    }
}
```

A tag belongs to many posts
```php
// post_tag.post_id
// post_tag.tag_id
class Tags extends Model {
    public function posts()
    {
        return $this->belongsToMany(Post::class);
    }
}
```

#### Managing relations

##### hasOne
```php
// User hasOne existing phone
$user->phone()->save($phoneModel);

// User hasOne new Phone that will be created
$user->phone()->create($arrayOfPhoneFields);
```
##### hasMany
```php
// User hasMany existing posts
$user->posts()->saveMany([$postModel]);

// User hasMany new posts that will be created
$user->posts()->createMany([$arrayOfPostFields, $arrayOfPostFields]);
```
##### belongsTo
```php
// Post belongsTo user
$post->user()->associate($userModel);
```
##### belongsToMany
```php
// Post belongsToMany tags 2, 3 & 4, but will belongsToMany with 1,2 & 3 through sync
$post->tags()->sync([1,2,3])

// Tag belongsToMany existing Post
$user->phone()->save($phoneModel);

// Tag belongsToMany new Post that will be created
$user->phone()->create($arrayOfPhoneFields);

// Tag belongsToMany existing Post
$user->posts()->saveMany([$postModel]);

// Tag belongsToMany new Post that will be created
$user->posts()->createMany([$arrayOfPostFields, $arrayOfPostFields]);

// Tag belongsToMany existing Post
$user->posts()->attach($postModel);
```