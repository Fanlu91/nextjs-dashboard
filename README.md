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

### Route Groups

In the `app` directory, nested folders are normally mapped to URL paths. 

Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses `()`, the name won't be included in the URL path. So `/dashboard/(overview)/page.tsx` becomes `/dashboard`.

you can create a different layout for each group by adding a `layout.js` file inside their folders.

The naming of route groups has no special significance other than for organization. 







