**Authentication**🔒 in frontend applications is always a daunting task for a beginner in ReactJS 🤔. One has to know the core concepts of ReactJS and well as how  browser local storage, session storage etc. works in order to successfully implement the entire workflow behind authentication. Implementing it using Redux even adds more difficulty to the same. So, we will see how we can implement the same using the **React Context API**. Those who have no idea about what Context API is, we will look at the concept clearly on this **article**. 

**Note:** There will be a series of 2-3 articles to give to the entire explaination on how this works.

# React Context API

To start with, lets look at what Facebook says about it in there official docs: 

> Context provides a way to pass data through the component tree without having to pass props down manually at every level.
 
So, it is clear from the quote, that context API makes the data flow easier in applications. This can be used in small applications, or for using small functionalities like authentication, providing theme etc. in large applications.

Now, lets start with its working.

## Step 1 - Initialization
```
import React, { useContext } from 'react';

//Auth Context
export const AuthContext = React.createContext({
    token: null,
    setToken: (data) => { },
    data: null,
    setData: (data) => { },
})

//Use Auth Context
export function useAuthContext() {
    return useContext(AuthContext);
}

```
A context is created using the concept, similar to this snippet of code. We pre-define our data and function which the context would serve in the application inside the `createContext` handler for its usage in other components and using this we serve the data when we need it.

## Step 2 - Providing the context to the component tree
This is merely simple task, we first have to initialize the data we want to pass on in the context to our local state. Make sure we do it to a component at a lower level then that of its children i.e, where we want to actually use the context.

#### Function based Approach
```
import { AuthContext } from '../Context/AuthContext';

function App() {
    const [token, setToken] = useState(null);
    const [data, setData] = useState({});

    return (
        <AuthContext.Provider
            value={{
                token: token,
                data: data,
                setToken: setToken,
                setData: setData,
            }}
        >
          <ChildComponents />
       </AuthContext.Provider>
    );
}
```

#### Class based Approach
```
import { AuthContext } from '../Context/AuthContext';

class App extends Component {
    constructor(props){
        super(props);
        this.state = {
            token : null,
            data : null
        }
    }

    setToken = (data)=>{
        this.setState({ token : data });
    }

    setData = (data) =>{
        this.setState({ data : data });
    }

    render() {
        return (
            <AuthContext.Provider value = {{
                data : this.state.data,
                token : this.state.token,
                setToken : this.setToken,
                setData : this.setData
            }}>
                <ChildComponents />
            </AuthContext.Provider>
        )
    }
}
```

It is clear from the code snippet that we first initialize our local state of data which we pass on as value to the `AuthContext.Provider`.

***Note:** We need to make sure that name of key inside the Context provider is same as that used during the initialization of the context.

React allows manipulation of the data inside functions if we want according to our business logic. This can be done by writing our own custom functions and then passing it in the Context provider `value` prop. 

Now last, but not the least.
## Step 3 - Usage of Context 

There are two ways of using the context in a React component and the approach varies differently for a class based and function based components.

First lets discuss the way we use it in class based component. 👉 

We have two ways of the same in a class based component, `contextType` and `Context Consumer`. The way I recommend and use myself is `contextType`. This way of using the context enables usage of the context everywhere in the component after the component is rendered. 

> React will find the closest Context Provider above and use its value.

```
import { AuthContext } from '../Context/AuthContext';

class LoginScreen extends Component {
    static contextType = AuthContext;
    constructor(props){
        super(props);
        this.state = {
            mobile_number:"",
            password:""
        }
    }

    onSubmitHandler = (event) => {
        event.preventDefault();
        const { setToken, setData } = this.context;

        const params = {
            mobile_number: this.state.mobile_number,
            password: this.state.password
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

    render() {
        return (
            <div className="login">
                <input
                    type="text"
                    placeholder="Enter Mobile Number"
                    value={this.state.mobile_number}
                    onChange={(event) => {
                        this.setState({mobile_number:event.target.value})
                    }}
                />
                <input
                    type="password"
                    placeholder="Enter Password"
                    value={this.state.password}
                    onChange={(event) => {
                        this.setState({password:event.target.value})
                    }}
                />
                <button
                    type="submit"
                    onClick={this.onSubmitHandler}>
                    Login
                </button>
            </div>
        )
    }
}
```

It is clear from the code when the `button` is clicked, the `onSubmitHandler` is executed and then the login API is called and after this we capture the response token and data in our context using the `this.context`. This makes the parent state capture the token and data and store inside the state of the component where the context was provided. Now this value can be used anywhere in our application, may it be for authentication i.e, by checking if the token is stored (using `this.context.token`) and logging in the user conditionally or displaying the data of the user any where.  🤗

***Note:** To display the data we use `this.context.data.name`(example) etc. 

The second approach used in the class based components is this:- 

```
import { AuthContext } from '../Context/AuthContext';

class DisplayScreen extends Component {  
    render() {
        return (
            <AuthContext.Consumer>
                {value => (
                    <div className="name">{value.name}</div>
                )}
            </AuthContext.Consumer>
        )
    }
}
```

This method has only one downfall i.e, it cannot be used anywhere within the class as we could do using the `contextType`.

P.S: The article is getting longer. we will see the functional approach of the same and authentication in the next article soon. Tune in for the same till then. Thank you ✌. I hope this was helpful, we will see more of it soon 😁

 [Medium Url](https://khushal87.medium.com/implementing-authentication-in-react-using-react-context-api-part-1-react-context-api-6af552b72931) 


### Follow and support me -
Github 👨‍💻 -  [khushal87](https://github.com/khushal87) 

LinkedIn 👨‍💻 - [Khushal Agarwal](https://www.linkedin.com/in/khushal-agarwal-547370166/)

Portfolio - [Link](https://khushal87.github.io/Portfolio)
