#### Eloquent | Examples


### Relations


A post can belong to many tags, belongs to one user and has many comments refering to it. 
```php
// post.user_id

// post_tag.post_id
// post_tag.tag_id

// comment.post_id

class Post {
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
class Phone {
    public function user()
    {
        return $this->belongsTo(User::class);
    }
}
```

A comment belongs to a post.
```php
// comment.post_id
class Comment {
    public function post()
    {
        return $this->belongsTo(Post::class);
    }
}
```

A user had many posts and has one phone.
```php
// phone.user_id
// post.user_id
class User {
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
class Tags {
    public function posts()
    {
        return $this->belongsToMany(Post::class);
    }
}
```