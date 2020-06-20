### Blade code samples

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

