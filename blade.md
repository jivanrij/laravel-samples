### Blade code samples

Note: There are some nice Laravel packages that take care of rendering form elements and stuff like that.

#### Form | Basic form
```blade
{{-- The $model needs to have the same name as the parameter in the route file. Else use route('your.route', ['model' => $model]) --}}
{{-- Put can also be: post, delete, get & patch --}}
<form action="{{route('your.route', compact($model))}}" method="POST" id="form-id">
    @csrf
    @method('put')
    {{-- add the fields here --}
</form>
```

#### Form | Select field edit examples
```blade
<div class="{{$errors->has('model_field') ? 'error_class' : '' }}">
    <label for="model_field">Label text</label>
    <select name="model_field" id="model_field">
        <option value="null" disabled selected>Nothing</option>
        @foreach(\Model::all() as $modelItem)
            <option value="{{$modelItem->id}}" @if(old('model_field', $model->model_field ?? '') == $modelItem->id) selected="selected" @endif>{{$modelItem->title}}</option>
        @endforeach
    </select>
    @error('model_field')
        <div class="error">{{$message}}</div>
    @enderror
</div>
```

#### Form | Text field edit examples
```blade
<div class="{{$errors->has('model_field') ? 'error_class' : '' }}">
    <label for="model_field">Label text</label>
    <input type="text" name="model_field" id="model_field" value="{{old('model_field', $model->model_field ?? '')}}">
    @error('model_field')
        <div class="error">{{$message}}</div>
    @enderror
</div>
```

#### Form | Checkbox field edit examples
```blade
<div class="{{$errors->has('model_field') ? 'error_class' : '' }}">
    <input class="checkbox" id="model_field" name="model_field" type="checkbox" value="1" {{ ((boolean) !is_null(Session::get('errors')) ? old('model_field') : $model->model_field) ? 'checked="checked"' : '' }} >
    @error('model_field')
        <div class="error">{{$message}}</div>
    @enderror
</div>
```





