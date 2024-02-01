## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.



https://nextjs.org/learn/dashboard-app

```less
npm i
npm run dev
```

## UI

### Tailwind to style elements by adding class names

[Tailwind](https://tailwindcss.com/) is a CSS framework that speeds up the development process by allowing you to quickly write [utility classes](https://tailwindcss.com/docs/utility-first) directly in your TSX markup.

### breakpoint with hidden/block

**Tailwind's Responsive Design System**: Tailwind uses a mobile-first approach. It provides various breakpoints (like `sm`, `md`, `lg`, `xl`, `2xl`) that correspond to different minimum screen widths. These breakpoints are used with utility classes to apply styles conditionally based on the screen size.[Nested routing](https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages#nested-routing)

**The `hidden` Class**: This is a utility class in Tailwind CSS that sets the `display` property of an element to `none`, effectively hiding it. When used alone, `hidden` will hide the element on all screen sizes.

**Combining `hidden` with Breakpoints**: When you combine `hidden` with a breakpoint, it changes the behavior based on the screen size. For example, `md:block` means that the element will use `display: block` (become visible) on medium (`md`) screens and larger, but will remain hidden on smaller screens.

**The `block` and `md:hidden` Classes**: The `block` class sets the `display` property to `block`, making the element visible. When combined with `md:hidden`, it means the element will be visible on small screens but will be hidden on medium screens and larger.

### cls library to toggle class names

[`clsx`](https://www.npmjs.com/package/clsx) is a library that lets you toggle class names easily.

- Suppose that you want to create an `InvoiceStatus` component which accepts `status`. The status can be `'pending'` or `'paid'`.
- If it's `'paid'`, you want the color to be green. If it's `'pending'`, you want the color to be gray.

```less
import clsx from 'clsx';

export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```

### file-system routing & colocation

how you can create different pages in Next.js: create a new route segment using a folder, and add a `page` file inside it.

Next.js uses file-system routing where **folders** are used to create nested routes. Each folder represents a **route segment** that maps to a **URL segment**.`page.tsx` is a special Next.js file that exports a React component, and it's required for the route to be accessible.

By having a special name for `page` files, Next.js allows you to [colocate](https://nextjs.org/docs/app/building-your-application/routing#colocation) UI components, test files, and other related code with your routes. Only the content inside the `page` file will be publicly accessible.



## Fetch data

In Next.js, you can create API endpoints using [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers).



### Using Server Components to fetch data

Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use `async/await` syntax without reaching out for `useEffect`, `useState` or data fetching libraries.

在React中，`useEffect` 和 `useState` 是React Hooks，它们提供了在函数组件中处理副作用（side effects）和状态（state）的能力。

1. **useState**: 这个Hook使你能在函数组件中添加和管理内部状态。在类组件中，状态是通过`this.state`和`this.setState`来管理的，而在函数组件中，你可以通过`useState`来实现相同的功能。

   ```javascript
   const [count, setCount] = useState(0);
   ```

   这里，`count`是当前状态的值，而`setCount`是一个更新这个状态的函数。

2. **useEffect**: 这个Hook用于在函数组件中执行副作用操作，如数据获取、订阅或手动更改DOM。它类似于类组件中的`componentDidMount`、`componentDidUpdate`和`componentWillUnmount`生命周期方法的组合。

   ```javascript
   useEffect(() => {
     // 副作用逻辑
   }, [dependencies]);
   ```

   在这个例子中，副作用会在依赖项`dependencies`改变时执行。

在传统的React（包括Next.js）应用中，数据获取通常在组件的副作用中处理，这就需要`useEffect`和`useState`。例如，你可能会在`useEffect`中发起一个异步请求，然后将结果存储在通过`useState`创建的状态中。

而在使用Server Components的情况下，数据获取可以直接在组件中通过异步函数完成，无需使用`useEffect`或`useState`。这简化了数据获取的逻辑，因为你可以直接在组件中等待异步操作的结果，而不是将其分散到不同的Hooks中。这样做可以减少组件的复杂性，使代码更易于理解和维护。



### Rendering

Static Rendering

- Faster Websites, cdn
- Reduced Server Load
- better SEO

Dynamic Rendering

- Real-Time Data
- User-Specific Content 
- Request Time Information

With dynamic rendering, **your application is only as fast as your slowest data fetch.**

### Streaming 

By streaming, you can prevent slow data requests from blocking your whole page. 

There are two ways you implement streaming in Next.js:

1. At the page level, with the `loading.tsx` file.
2. For specific components, with `<Suspense>`.

### Route Groups

In the `app` directory, nested folders are normally mapped to URL paths. 

Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses `()`, the name won't be included in the URL path. So `/dashboard/(overview)/page.tsx` becomes `/dashboard`.

you can create a different layout for each group by adding a `layout.js` file inside their folders.

The naming of route groups has no special significance other than for organization. 

### Suspense 

Suspense allows you to defer rendering parts of your application until some condition is met (e.g. data is loaded).

You can wrap your dynamic components in Suspense. Then, pass it a fallback component to show while the dynamic component loads.



## Search and Pagination

benefits of implementing  search with URL params

- Bookmarkable and Shareable URLs
- Server-Side Rendering and Initial Load
- Analytics and Tracking



# From ChatGPT

## use

import { useSearchParams } from 'next/navigation'; 这里 use代表什么含义？ 我看到很多类似的用法，什么会带上use前缀？在next或者react里，还有没有类似用法的词



在 Next.js 和 React 的世界中，以 `use` 开头的函数通常是指**钩子（Hooks）**。这是一种特殊的函数，它们让你能够“钩入”React 的功能。例如，`useState` 和 `useEffect` 是 React 中最常用的内置钩子。

`useSearchParams` 是一个用于处理 URL 搜索参数的钩子。在 Next.js 中，它类似于 React Router 的钩子，允许你在函数组件中读取和操作 URL 的查询参数。

这里的 `use` 前缀遵循了 React 钩子的命名惯例。React 的团队选择这种命名方式是为了帮助开发者区分钩子和普通的 JavaScript 函数。这种命名也有助于 React 在内部正确地处理钩子的行为。

在 React 和 Next.js 中，你会遇到许多这样的钩子，例如：

1. **useState**: 用于在函数组件中添加状态。
2. **useEffect**: 用于处理副作用，如数据获取、订阅或手动更改 React 组件树之外的 DOM。
3. **useContext**: 用于访问 React 的上下文（Context）系统。
4. **useRef**: 用于持久化引用 DOM 元素或其他数据。
5. **useReducer**: 用于处理更复杂的组件状态逻辑。
6. **useCallback**: 用于记忆化回调函数。
7. **useMemo**: 用于记忆化计算结果。

这些钩子大大增强了函数组件的能力，让你能以更声明式的方式编写组件，同时保持组件逻辑的整洁和可维护性。



在 Next.js 和 React 的生态系统中，除了以 `use` 开头的钩子（Hooks）外，还有一些其他常见的命名模式和前缀。这些命名模式在代码的可读性和组织结构方面起到了关键作用。以下是一些例子：

1. **get** 前缀：通常用于表示获取数据或执行计算的函数。例如，在 Next.js 中，`getStaticProps` 和 `getServerSideProps` 是用于数据获取的函数。

2. **is** 前缀：通常用于返回布尔值的函数，这些函数通常用来检查某种状态或条件。例如，`isLoading` 可能表示某个异步操作是否正在进行。

3. **on** 前缀：常用于事件处理函数。例如，`onClick` 用于处理点击事件。

4. **render** 前缀：有时用于组件或函数，这些组件或函数专门用于渲染界面部分。例如，`renderItem` 可能用于渲染列表的每个元素。

5. **with** 前缀：通常用于高阶组件（HOCs）。例如，`withRouter` 是一个高阶组件，它将路由相关的 props 注入到一个组件中。

6. **handle** 前缀：通常用于处理用户交互或某些事件的函数。例如，`handleSubmit` 用于处理表单提交。

这些前缀不仅限于 Next.js 或 React，它们在整个 JavaScript 和前端开发领域都非常普遍。使用这些命名惯例可以帮助其他开发者更容易理解你的代码逻辑，同时也使得代码的意图更加明确。



## component

在Next.js中，组件可以根据运行环境被划分为**客户端组件**（Client Components）和**服务器端组件**（Server Components）。这种设计思想与Vue不同，在Vue中通常不区分组件的运行环境，而是通过生命周期钩子和特定的服务器端渲染指令来处理服务器端和客户端的逻辑。

### 服务器端组件（Server Components）

服务器端组件是在服务器上运行的React组件，它们在构建时或请求时执行，生成静态HTML或JSON来发送给客户端。服务器端组件的主要优点是能够直接访问服务器资源（如数据库），并且可以在发送给客户端之前完成数据获取和渲染的工作，从而提升性能和SEO优化。

服务器端组件的特点：
- **无客户端的JavaScript：** 这些组件不会发送JavaScript到客户端，因此不会影响页面加载时间。
- **数据获取：** 可以直接在组件内部进行数据获取，而无需额外的客户端数据获取逻辑。
- **访问服务器资源：** 可以安全地访问服务器资源，如数据库或内部API，而无需通过API路由公开这些资源。
- **条件性客户端代码：** 可以根据需要将一部分逻辑保留在客户端执行，以实现动态交互。

### 客户端组件（Client Components）

客户端组件是在浏览器中运行的React组件，它们完全依赖于客户端的JavaScript来实现交互性。这类组件适用于需要与用户进行丰富交互的页面部分，比如表单处理、动画、或是与用户输入密切相关的功能。

客户端组件的特点：
- **完全交互性：** 依赖客户端JavaScript来实现动态交互。
- **客户端状态管理：** 可以使用如React状态管理或其他状态管理库来处理状态。
- **动态内容：** 适用于内容需要根据用户操作动态变化的场景。

### 使用场景

- **服务器端组件**：适用于静态内容展示、SEO优化页面、服务器端数据处理等场景。
- **客户端组件**：适用于需要丰富用户交互、客户端状态管理、动态内容更新等场景。

### 结合Vue的经验

如果你有Vue的经验，可以将Next.js的服务器端组件看作是类似于Vue中的服务端渲染（SSR）组件，但它们在架构上更加灵活，允许你更细致地控制哪些部分在服务器上渲染，哪些部分在客户端渲染。客户端组件则类似于Vue中常规的单文件组件（SFC），依赖于客户端JavaScript来实现交互性。

了解这些概念后，你可以根据应用的需求，结合服务器端和客户端组件的优点，设计出既快速又交互性强的Web应用。

在Next.js中，根据组件的类型（客户端组件或服务器端组件），获取后端数据库中数据的方法会有所不同。这里我会分别介绍如何在两种组件中获取数据。

### 服务器端组件获取数据

在服务器端组件中，你可以直接在组件内部使用数据库查询来获取数据。这是因为服务器端组件在服务器上运行，可以直接访问服务器资源，包括数据库。你可以在组件的服务器端逻辑中进行数据库查询，并将查询结果作为props传递给组件渲染。

这种方法的优点是可以在页面构建时（SSG）或请求时（SSR）获取最新的数据，而且不会暴露数据库访问逻辑给客户端，保持了安全性。

#### 示例

假设你正在使用Next.js的服务器端渲染功能（SSR）来获取数据，你可以在页面组件中使用`getServerSideProps`函数来获取数据库数据：

```jsx
// pages/posts.js
import { getServerSideProps } from 'next'

export async function getServerSideProps(context) {
  const data = await fetchDataFromDatabase(); // 假设这是从数据库获取数据的函数
  return {
    props: { data }, // 将数据作为props传递给组件
  }
}

export default function Posts({ data }) {
  return (
    // 使用数据渲染组件
    <div>{data.map(post => <div key={post.id}>{post.title}</div>)}</div>
  )
}
```

### 客户端组件获取数据

对于客户端组件，数据获取通常是通过客户端API请求来实现的。你可以在组件内使用诸如`fetch`或Axios这样的HTTP客户端来请求一个API端点，该端点负责与数据库交互并返回数据。

客户端数据获取通常在组件的生命周期钩子中进行，如在React的`useEffect`钩子中，确保在组件加载时获取数据，并在数据到达时更新组件状态。

#### 示例

```jsx
// components/ClientSidePosts.js
import React, { useState, useEffect } from 'react';

function ClientSidePosts() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    fetch('/api/posts')
      .then(response => response.json())
      .then(data => setPosts(data))
  }, []); // 空依赖数组表示这个effect只在组件挂载时运行一次

  return (
    <div>
      {posts.map(post => <div key={post.id}>{post.title}</div>)}
    </div>
  );
}

export default ClientSidePosts;
```

在这个示例中，客户端组件通过调用`/api/posts`端点来获取数据。这个端点需要你在`pages/api`目录下创建相应的API路由，该路由处理数据库查询并返回数据。

### 结论

选择服务器端组件还是客户端组件获取数据，取决于你的具体需求，比如是否需要SEO、数据的实时性要求、以及用户交互的复杂度等。服务器端组件更适合静态内容和SEO优化，而客户端组件适合动态交互和实时数据更新的场景。



