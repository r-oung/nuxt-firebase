# Nuxt 3 Minimal Starter

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Prerequisites

Create a Firebase project and enable [Functions](https://firebase.google.com/docs/functions) and [Hosting](https://firebase.google.com/docs/hosting).

## Setup

Create a new Nuxt project, see [Nuxt installation](https://nuxt.com/docs/getting-started/installation).

```bash
npx nuxi@latest init nuxt-firebase
```

Add the following configurations to `nuxt.config.ts`, see [Nuxt Firebase deploy instructions](https://nuxt.com/deploy/firebase):

```javascript
export default defineNuxtConfig({
  nitro: {
    firebase: {
      gen: 2,
    },
    preset: "firebase",
  },
});
```

Install the latest version of Firebase CLI.

```bash
npm install -g firebase-tools@latest
```

Install the `firebase-functions` package.

```bash
npm install firebase-functions
```

Initialize your Firebase Project

```bash
firebase login
firebase init hosting
```

You will be prompted to answer the following questions:
? What do you want to use as your public directory? public
? Configure as a single-page app (rewrite all urls to /index.html)? No
? Set up automatic builds and deploys with GitHub? No

Remove the following files from your `public` directory:

- 404.html
- index.html

Add the following to your `firebase.json` to enable server rendering in Cloud Functions. Don't forget to insert your Firebase project ID:

```json
{
  "functions": {
    "source": ".output/server",
    "codebase": "nuxt"
  },
  "hosting": [
    {
      "site": "<your_project_id>",
      "public": ".output/public",
      "cleanUrls": true,
      "rewrites": [
        {
          "source": "**",
          "function": "server"
        }
      ]
    }
  ]
}
```

## Local Preview

```bash
npm run build
firebase emulators:start
```

## Build and Deploy

```bash
npm run build
firebase deploy
```
