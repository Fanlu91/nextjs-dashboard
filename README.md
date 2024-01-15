## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## Notes

https://nextjs.org/learn/dashboard-app

```less
npm i
npm run dev
```

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
