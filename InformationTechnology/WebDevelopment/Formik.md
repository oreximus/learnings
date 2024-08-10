## Formik Library Notes and Code Snippets:

- Replacement for: onChange, onBlur, value in the form,
  instead of doing this:

```
<Formik
  initialValues={{ name: '' }}
  onSubmit={(values) => console.log(values)}
>
  {({ handleChange, handleBlur, values }) => (
    <form>
      <input
        type="text"
        name="name"
        onChange={handleChange}
        onBlur={handleBlur}
        value={values.name}
      />
    </form>
  )}
</Formik>
```

do this:

```
<Formik
  initialValues={{ name: '' }}
  onSubmit={(values) => console.log(values)}
>
  {(formik) => (
    <form>
      <input
        type="text"
        {...formik.getFieldProps('name')}
      />
    </form>
  )}
</Formik>
```
