```
npm install react-hook-form yup @hookform/resolver/yup
```

## read the command to implement

#first import all thing in form.js

```
import { useForm } from "react-hook-form";
import { yupResolver } from "@hookform/resolvers/yup";
import * as yup from "yup";
```

#second create schema

```
const schema = yup.object().shape({
  firstName: yup.string().required("First Name should be required please"),
  lastName: yup.string().required(),
  email: yup.string().email().required(),
  age: yup.number().positive().integer().required(),
  password: yup.string().min(4).max(15).required(),
  confirmPassword: yup.string().oneOf([yup.ref("password"), null]),
});
```

#third create form functions and input schema to yup resolver

```
function Form() {
  const { register, handleSubmit, errors } = useForm({
    resolver: yupResolver(schema),
  });
```

#four create a submit function to get the input data

```
  const submitForm = (data) => {
    console.log(data);
  };
```

#five add ref to each input field with register in input

```
<input
            type="text"
            name="lastName"
            placeholder="Last Name..."
            ref={register}
          />
```

#six add handleSubmit to the form wit submit functions

```
<form onSubmit={handleSubmit(submitForm)}>
```

#seven add error message (important notice. confirmPassword does not show the error message so in this case we have to use custom message)

```
<p> {errors.confirmPassword && "Passwords Should Match!"} </p>
```

#### in the submitForm function we have out input data value we can use them now to add or submit to our database from the function. we can also add them in useState and use them anywhere.
