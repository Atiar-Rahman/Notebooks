# `Next js`

1. project setup
	1. project customization for typescript and JavaScript and `src` folder and directly app use type.
2. has two types router. 
	1. app router
	2. page router
3. `pre-requist knowledge`
	1. html
	2. `css`
	3. `js`
	4. react
4. project installation
5. project structure and organization
	1. folder ans file `convension`
	2. top level folders
	3. top level files
	4. routing files
		1. layout
		2. page
		3. loading
		4. not-found
		5. error
		6. global-error
		7. route
		8. template
		9. default
	5. nested route
	6. dynamic route
	7. route groups and private folder
	8. parallel and intercept route
	9. 
6. layout and pages
	1. creating a page
	2. creating a layout
	3. creating a nested route
	4. nesting layouts
	5. creating a dynamic segment
	6. rendering with search `params`
	7. Linking between pages(`useRouter hook advance router and Link Component use for link one page to another pages)
7. Linking and navigating
	1. `prefetching, streaming and client-slde rendering. ensuring navigation stays fast and responsive.
	2. `server rendering, prefetching, streaming, client side rendering or transitions`
	3. dynamic routes without `loading.tsx`
	4. dynamic segments without `generateStaticParams`
	5. slow networks(`useLinkStatus` hooks)
	6. Disabling `prefetching ` 
	7. Hydration not completed
8. Server and client component(by default pages and layouts are server component)
	1. client components when you need(`'use client'`)
		1. state and event handlers
		2. `lifecycle logic
		3. `browser only apis 
		4. custom hooks  are the client component
	2. server components when you need
		1. fetch data from databases or `apis` close to the source
		2. use `api keys, tokens and other secrets without exposing them to the client`
		3. reduce the amount of JavaScript sent to the browser
		
9. fetching data
	1. `fetch api`
	2. parallel data fetching(`Promise.all())
10. CSS 
	1. `next js provides several ways to style your application using CSS, including`
		1. tailwind CSS
		2. CSS module
		3. global CSS
		4. External `Stylesheets`
		5. sass
		6. `css in js
		7. 