# Turborepo starter

This is an official starter Turborepo.

## Using this example

Run the following command:

```sh
npx create-turbo@latest
```

## What's inside?

This Turborepo includes the following packages/apps:

### Apps and Packages

- `docs`: a [Next.js](https://nextjs.org/) app
- `web`: another [Next.js](https://nextjs.org/) app
- `@repo/ui`: a stub React component library shared by both `web` and `docs` applications
- `@repo/eslint-config`: `eslint` configurations (includes `eslint-config-next` and `eslint-config-prettier`)
- `@repo/typescript-config`: `tsconfig.json`s used throughout the monorepo

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/).

### Utilities

This Turborepo has some additional tools already setup for you:

- [TypeScript](https://www.typescriptlang.org/) for static type checking
- [ESLint](https://eslint.org/) for code linting
- [Prettier](https://prettier.io) for code formatting

### Build

To build all apps and packages, run the following command:

```
cd havedevs
pnpm build
```

### Develop

To develop all apps and packages, run the following command:

```
cd havedevs
pnpm dev
```

### Remote Caching

> [!TIP]
> Vercel Remote Cache is free for all plans. Get started today at [vercel.com](https://vercel.com/signup?/signup?utm_source=remote-cache-sdk&utm_campaign=free_remote_cache).

Turborepo can use a technique known as [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching) to share cache artifacts across machines, enabling you to share build caches with your team and CI/CD pipelines.

By default, Turborepo will cache locally. To enable Remote Caching you will need an account with Vercel. If you don't have an account you can [create one](https://vercel.com/signup?utm_source=turborepo-examples), then enter the following commands:

```
cd havedevs
npx turbo login
```

This will authenticate the Turborepo CLI with your [Vercel account](https://vercel.com/docs/concepts/personal-accounts/overview).

Next, you can link your Turborepo to your Remote Cache by running the following command from the root of your Turborepo:

```
npx turbo link
```

Environment Variables
This project requires the use of environment variables to integrate with the News API.

Setup .env File
Before running the project, you need to set up a .env file at the root of your project. This file should include any required environment variables.

```
# .env
NEXT_PUBLIC_API_KEY=your-api-key-here
```

Usage of API Key
In the HomePage component, the NEXT_PUBLIC_API_KEY is used to access the News API, specifically when making requests for top headlines:

ts
const fetchArticles = async (page: number) => {
  setLoading(true);
  setProgress(0);
  simulateProgress();

  try {
    const response = await axios.get<NewsApiResponse>("/top-headlines", {
      params: {
        country: "us",
        category: "business",
        page,
        pageSize: articlesPerPage,
        apiKey: process.env.NEXT_PUBLIC_API_KEY, // Referencing the API key from the environment variable
      },
    });
    setArticles(response.data.articles);
    setTotalResults(response.data.totalResults);
    setLoading(false);
    setProgress(100);
  } catch (error: unknown) {
    setError(`Failed to fetch articles. ${error}`);
    setLoading(false);
    setProgress(0);
  }
};
Important Notes
Do not check your .env file into version control. Ensure it is added to your .gitignore file.
Replace your-api-key-here with the actual API key provided by the News API.

## Useful Links

Learn more about the power of Turborepo:

- [Tasks](https://turbo.build/repo/docs/core-concepts/monorepos/running-tasks)
- [Caching](https://turbo.build/repo/docs/core-concepts/caching)
- [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching)
- [Filtering](https://turbo.build/repo/docs/core-concepts/monorepos/filtering)
- [Configuration Options](https://turbo.build/repo/docs/reference/configuration)
- [CLI Usage](https://turbo.build/repo/docs/reference/command-line-reference)
