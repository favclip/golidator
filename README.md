# golidator

The programable validator.

## Description

Existing validator is not fully flexible.
We want to customize error object generation.
We want to modify value instead of raise error when validation failed.
We want it.

## Samples

see [usage](https://github.com/favclip/golidator/blob/master/usage_test.go)

### Basic usage

```
v := golidator.NewValidator()
err := v.Validate(obj)
```

### Use Custom Validator

```
v := golidator.NewValidator()
v.SetValidationFunc("req", func(t *validator.Target, param string) error {
    val := t.FieldValue
    if str := val.String(); str == "" {
        return fmt.Errorf("unexpected value: %s", str)
    }

    return nil
})
```

### Use Customized Error

```
v := &golidator.Validator{}
v.SetTag("validate")
v.SetValidationFunc("req", validator.ReqFactory(&validator.ReqErrorOption{
    ReqError: func(f reflect.StructField, actual interface{}) error {
        return fmt.Errorf("%s IS REQUIRED", f.Name)
    },
}))
```
