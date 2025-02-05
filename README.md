# Chakra UI Next.js with Turbopack enabled

This project is a minimal reproduction of an issue when using Chakra UI and Next.js with Turbopack enabled.
With Turbopack enabled, an error message appears:

```javascript
Uncaught Error: Hydration failed because the server rendered HTML didn't match the client. As a result this tree will be regenerated on the client. This can happen if a SSR-ed Client Component used:

- A server/client branch `if (typeof window !== 'undefined')`.
- Variable input such as `Date.now()` or `Math.random()` which changes each time it's called.
- Date formatting in a user's locale which doesn't match the server.
- External changing data without sending a snapshot of it along with the HTML.
- Invalid HTML tag nesting.

It can also happen if the client has a browser extension installed which messes with the HTML before React loaded.
```

If you disable Turbopack and use Webpack, the error will disappear.

Is this issue caused by Next.js Turbopack or Chakra UI?

## Steps to run the project and reproduce the issue

Follow these steps to run the project locally and reproduce the issue:

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/MichaelvdVeer/repo-chakra-nextjs-with-turbopack
cd repo-chakra-nextjs-with-turbopack
```

### 2. Install Dependencies

Run the following command to install the required npm packages:

```bash
npm install
```

### 3. Make sure Turbopack is enabled in package.json

To enable Turbopack, use the --turbopack flag when running the Next.js development server:

```
{
  "scripts": {
    "dev": "next dev --turbopack",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

### 4. Start the Development Server

```bash
npm run dev
```

Check the console; a hydration error will appear.
Somethimes you may need to refresh multiple times to see the error appear.

### 5. Disable Turbopack

Remove the --turbopack flag in package.json:

```
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

### 6. Restart the Development Server

Check the console; the hydration error will disappear.
