# adapter-lambda for SvelteKit

An adapter to build a [SvelteKit](https://kit.svelte.dev/) app into a lambda ready for deployment with lambda proxy via the Serverless framework or CDK.

## Installation
```
npm install --save-dev @yarbsemaj/adapter-lambda
```
## Usage

In your `svelte.config.js` configure the adapter as below;

```js
import serverless from '@yarbsemaj/adapter-lambda';
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';

/** @type {import('@sveltejs/kit').Config} */
const config = {
	preprocess: vitePreprocess(),

	kit: {
		adapter: serverless() //See Below for optional arguments
	}
};

export default config;
```

### For serverless
Copy `serverless.yml` from the root of this repo to the root of your project, make sure to change the service name.

After building your app run `sls deploy` to deploy code to AWS using the build tool [serverless](https://www.serverless.com/).

An example project using serverless can be found [here](https://github.com/yarbsemaj/sveltekit-serverless-starter).

### For CDK
Copy `SvelteKitSite.ts` from the root of this repo into your project and add it to a CDK stack.

Deploy your stack using `cdk deploy --all`

An example project using cdk can be found [here](https://github.com/yarbsemaj/sveltekit-cdk-starter).

### Tada 🎉
No matter how you deploy, your app can then be accessed via the CloudFront distribution created as a part of the stack.

## Options
| Argument            | Description                                | Type    | Default |
| ------------------- | ------------------------------------------ | ------- | ------- |
| **out**             | the output directory of build files        | string  | build   |
| **esbuildOverride** | overrides for the [default esbuild options](https://github.com/yarbsemaj/sveltekit-adapter-lambda/blob/master/index.js#L50)  | [esbuild Build Options](https://github.com/evanw/esbuild/blob/fc37c2fa9de2ad77476a6d4a8f1516196b90187e/lib/shared/types.ts#L110) | {}     |

## Static Assets and precompiled pages
To server static assets and precompiled pages, this adapter makes use of S3. In order to route traffic to the correct destination a Lambda@edge function is used to perform an origin rewrite to redirect traffic to the S3 Bucket.

## Infrastructure Diagram
![Infra](https://github.com/yarbsemaj/sveltekit-adapter-lambda/blob/master/docs/assets/diagram.png?raw=true)


## Help! I'm getting an error while building or serving my app.
Please raise an issue on [Github](https://github.com/yarbsemaj/sveltekit-adapter-lambda/issues), and I will be happy to issue a fix.

## Versions
| Adapter Version | Sveltekit Version |
| --------------- | ----------------- |
| 1.1.x - 1.2.x   | 1.22.0 (Official) |
| 1.x.x           | 1.0.0 (Official)  |
| 0.12.x          | 1.0.0-next.433    |
| 0.11.x          | 1.0.0-next.401    |
| 0.10.x          | 1.0.0-next.380    |
| 0.9.x           | 1.0.0-next.348    |
| 0.6.x - 0.8.x   | 1.0.0-next.301    |
| 0.5.x           | 1.0.0-next.286    |
| 0.3.x - 0.4.x   | 1.0.0-next.286    |
| 0.2.x           | 1.0.0-next.239    |
| 0.1.x           | 1.0.0-next.169    |
