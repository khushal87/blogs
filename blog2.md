Authentication🔒 in frontend applications is always a daunting task for a beginner in ReactJS 🤔. One has to know the core concepts of ReactJS and well as how browser local storage, session storage etc. works in order to successfully implement the entire workflow behind authentication. Implementing it using Redux even adds more difficulty to the same. So, we will see how we can implement the same using the React Context API. Those who have no idea about what Context API is, we will look at the concept clearly on this article.

Note: There will be a series of 2-3 articles to give to the entire explaination on how this works.

Link to previous article -  [Part 1](https://khushal87.hashnode.dev/implementing-authentication-in-react-using-react-context-api-part-1-react-context-api) 

In the previous article, we learned the basics of React Context API such as how we initialize it, provide it to the component hierarchy and how we use it in a class based components. 

Now the point is that how do we use it in a **Function component** 🤔?

Using function based component has several advantages as it allows using hooks, which we cannot use in a traditional class based component. Moreover, Function based approach comes out to be a boon for **Context API**. Also, we have a better performance in case of functional components compared to class based approach.

Well, let us see how? 🤗
In a traditional Stateful(class based) component, we can only use a single context under `contextType` which sometimes is not really friendly as we need multiple contexts at times for our state logic.

Eg. : Suppose, we have two contexts, one for *Auth*(used for storing user Auth info) and one for storing and providing
*Client*'s data and we want to use them in a same component. What would be the scenario then? 

Using stateful component won't help here, as we could use only one context at a time. 
Though this is possible within the `render` function of the component using multiple `Context Consumer`. But this is not possible anywhere within the component.

You can find the Class based implementation [here](https://khushal87.hashnode.dev/implementing-authentication-in-react-using-react-context-api-part-1-react-context-api).

Now, Function based component gives us a flexibility of using both of them anywhere within the component.

Let us see how we use Context in a functional component.

### Function based Approach
```
import { useState } from 'react';
import { useAuthContext } from '../Context/AuthContext';

function LoginScreen(props){
    const [mobile_number,setMobileNumber] = useState("");
    const [password,setPassword] = useState("");
    const {setToken , setData} = useAuthContext();

    const onSubmitHandler = (event) => {
        event.preventDefault();

        const params = {
            mobile_number: mobile_number,
            password: password
        }
        Axios.post(`/user/login`, params)
            .then((response) => {
                if (res.status === 200) {
                    setData(response.data.data);
                    setToken(response.data.token);
                }
            })
            .catch((err) => {
                console.log(error)
                Alert.alert(error.response.data.message);
            })
    }

    return (
        <div className="login">
            <input
                type="text"
                placeholder="Enter Mobile Number"
                value={mobile_number}
                onChange={(event) => {
                    setMobileNumber(event.target.value)
                }}
            />
            <input
                type="password"
                placeholder="Enter Password"
                value={password}
                onChange={(event) => {
                   setPassword(event.target.value)
                }}
            />
            <button
                type="submit"
                onClick={onSubmitHandler}>
                Login
            </button>
        </div>
    )
}
``` 

The difference mainly lies on how we use it. In the stateful component, we used `contextType` to use it globally within the component but here we take use of the
custom **Hook** `useAuthContext` which we created while initialization of the context. This way of implementing a component provides us the flexibility of using multiple hooks within a same component and thereby multiple `Context` in a same component.

Note: To understand how we implemented the *hook* for usage, refer to my previous blog.

In the code, we destructured the values of the context, simply through the `hook` as you see here in this snippet:
```
const {setToken , setData} = useAuthContext();
```
Now, we can use the destructured functions and data within our component. If we want to use multiple contexts, the approach would be entirely same. 

Note: We also have the traditional way of consuming the context as was discussed in the previous blog using `AuthContext.Consumer`. This only allows using the Context within the `return` statement. 

Comment down, which approach do you like to use on your projects. 😄😄

Kudos! Now, we are strong with the concept of **React Context API **. In the next blog we will see its application in Authentication. 😉😉

### Follow and support me -
Github 👨‍💻 -  [khushal87](https://github.com/khushal87) 

LinkedIn 👨‍💻 - [Khushal Agarwal](https://www.linkedin.com/in/khushal-agarwal-547370166/)

Portfolio - [Link](https://khushal87.github.io/Portfolio)
