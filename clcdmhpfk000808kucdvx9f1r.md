# React Context API Demystified: A Beginner's Guide

I started learning to use the MERN stack for building web applications a few days ago. After successfully hosting my first web app built with this stack, I couldn't help but notice that some of the most confusing parts of this stack for beginners have to do with the React JS part.

React state management, hooks, and the context API, are among the most confusing parts. Once, I found it confusing, and I believe that a lot more people do too. I checked the comments section of the YouTube videos I was using to learn, and the comments about these concepts justified my beliefs.

One of the ways, I get through such confusing concepts is to spend more time learning and practicing how to use them, but eventually, what really helps is when I try to teach them to other beginners. Therefore, this post is the means through which I will flesh out what I have learned about the React context API in a way that beginners will find very helpful.

Hence, if you find yourself in similar shoes, buckle up, because we are going to demystify it in this post.

## Why you need to know React Context

If you have knowledge of any programming language (which I presume you do because that's why you are reading this article), you will be familiar with the concepts of variables. You will also know that variables can be local or global. When developing an app, you may sometimes need a global variable that you can easily access in different parts of your program.

Let's say you are building a social media app. When a user logs into the app, you will surely want to keep some relevant user data at hand and use that to authenticate their access to various aspects of your app. For instance, you may have pages that only administrators can access. For that matter, when a user logs in, you will want to keep their role, preferably in a global variable, so that for each activity they perform on your app, you will want to check if they have the right to access them or not.

Did that make sense? If not, read it over again, but if it did, then let's go on.

In your React app, the way that you may want to approach it is by, passing that special data (user details) as props. This will enable a parent component to pass the values to their immediate children components.

Imagine the case of your social media app: how many components will you create in all, and how many of these will need to receive such props? Even though I have yet to build a social media app with React JS, I believe, there will be so many components that it becomes impractical to pass down props to every component.

If you try to pass the data as props, you will realize that you may have to pass it through a whole number of components and some of these components may not even have use for the props but just serve as a conduit to get the props to the ones that need them.

That practice is termed `prop drilling` and is considered a bad practice in developing React apps.

To avoid, prop drilling, one of the ways out is to use `React context`.

## What is the Context API and why is it useful?

According to the official [React JS documentation](https://reactjs.org/docs/context.html), `Context` provides a way to pass data through the component tree without having to pass props down manually at every level.

Hence, you can see a `React Context` as a **global variable** that makes specific data available to all components that are put within its reach. This can be particularly useful in situations where the props need to be passed through many components, or when the same prop is being passed to many components that are not directly related to one another.

As illustrated earlier, using `context` will prevent prop drilling, make it easier to manage shared values, and also reduce the complexity of the component tree.

Even though, using `context` may seem time-saving, but you should know that it isn't your go-to for every situation. There are cases where using `context` isn't the best because using `context` has the downside of making the reusability of components difficult.

## Creating and Using a Context

To create and use a `Context` in React, you need to do three main things:

* Defining a Context object
    
* Providing a Context value
    
* Consuming a Context value
    

You would start by creating a Context object, then create a Provider. After creating the provider, you would have to wrap all components or the component tree that requires the value passed to the Context within the Provider. The data to be shared should be passed as a value to the provider.

To consume the data in any of these components, you will create a context Consumer to enable you to access the values.

### Defining a Context object

To create or define a Context object in your React app, you will first need to import the `createContext` function from the `react` library. Then, you can use this function to create a new Context object like this:

```javascript
import { createContext } from 'react';
const ExampleContext = createContext();
```

The above code creates a `Context` object called `exampleContext.` The reason why we are using the `Context API` in the first place is to allow us to pass values around. Hence, the should be a way to pass the value around. We do that with a `Provider`.

### Providing a Context value

The easiest way to create a provider and make the passing of values around is to create a component for the context. You can then use this component as a parent to every component in the component tree that will need to consume the value in this provider (have access to the value).

Let's call our new component `ExampleContextProvider.` This component must define a function that returns a `Context.Provider` element, and pass the value that you want to provide as a prop to the component.

You can add this to the code we wrote earlier in a single file. This script will therefore be for creating the context and managing the data stored in it.

```javascript
import { createContext } from 'react';
const ExampleContext = createContext();

function ExampleContextProvider(props) {
    const fname = "Obed";
    const lname = "Ehoneah";
  return (
    <ExampleContext.Provider value={{ fname, lname }}>
      {props.children}
    </ExampleContext.Provider>
  );
}

export default ExampleContextProvider;
```

In the example above, we have created a component, which will be used as a parent component and wrapped around all children components that need the values stored in this Context.

I have hard-coded values (`fname` and `lname`) into the Provider component but this will usually not be the case. You will usually combine this with `React Hooks` to be able to dynamically change the values or keep them updated when it needs to be. I may discuss that in subsequent articles.

For now, let's keep our focus on how to use the data stored in the `Context`.

In the part of your App where you have a collection of components that may use the data stored in this `Context`, we will need to wrap all those components within the Provider component we created above.

A common example will be to wrap the all components that were put within the `App` component (which is usually the mother component for most React apps within the ContextProvider component.

By doing that, all the components inside the App components will now have access to the data stored in the `Context` that we created. Note that you can create as many `Contexts` as you may need and thus you are not restricted to a single one. This usually comes in handy when working with things like the current locale, theme, or data cache.

```javascript
import React from 'react';
import ExampleContextProvider from './ExampleContextProvider';

function App() {
  return (
    <ExampleContextProvider>
      <div>
            {/* All Other components go here */}
      </div>
    </ExampleContextProvider>
  );
}

export default App;
```

### Consuming a Context value

Getting access to the data inside a `Context` is termed `comsumption`. There are two main ways to consume Context values. You can do that by:

1. Using the `useContext` hook
    
2. Using the `Context.Consumer` element
    

#### Using the `useContext` hook

Here is an example where we consume the data by using the `useContext` hook.

```javascript
import React, { useContext } from 'react';

function UserInfo() {
  const user = useContext(ExampleContext);
  return (
    <div>
      <span>First Name: {user.fname}</span>
      <span>Last Name: {user.lname}</span>
    </div>
  );
}

export default UserInfo;
```

#### Using the `Context.Consumer` element

```javascript
import { ExampleContext } from './context';

function UserInfo() {
  return (
    <ExampleContext.Consumer>
      {(user) => (
        <div>
          <span>First Name: {user.fname}</span>
          <span>Last Name: {user.lname}</span>
        </div>
      )}
    </ExampleContext.Consumer>
  );
}

export default UserInfo;
```

## Conclusion

I believe this is just a scratch of the surface of what you can do with the React Context API. There are a lot more things like state management, etc but this should be a good starting point for you.

As I keep learning and discovering new things, I will continue to share them with you through this blog, my YouTube channel, and on Twitter as well. If you don't want to miss any of them or want to connect with me personally or support me in any way or form then take any or all of these 3 actions.

1. Subscribe to this [blog or follow the blog](http://hashnode.com/@ehoneahobed)
    
2. Subscribe to my [YouTube Channel](https://youtube.com/@ehoneahobed)
    
3. Follow me on [Twitter and send me a DM](https://ehoneahobed.com/twitter) (I long to hear from you)