# @telegraf-hardened/fetch 🛡️  

A production-ready, zero-dependency (almost) native fetch wrapper for Node.js 18+. It bridges the gap between the modern Web Fetch API and the need for complex proxying (SOCKS4/5, HTTP/HTTPS) using high-performance undici dispatchers. Follows the standard Fetch API signature, with an additional (optional) timeout property in the init object to override the default.

## Features

- Native Fetch API: No more Axios or node-fetch. Uses the built-in Node.js engine.

- SOCKS4/5 Support: Full support for SOCKS proxies, including authentication.

- HTTP/HTTPS Proxying: Via undici's ProxyAgent.

- Automatic Timeout: Simple timeout option integrated with AbortSignal.

- TypeScript First: Written in TS with full type definitions.

## Installation

```Bash
npm install @telegraf-hardened/fetch
```

## Usage

- Simple Request with Proxy (SOCKS5 / TOR):

```TypeScript
import { FetchClient } from '@telegraf-hardened/fetch'

// Initialize the client with a proxy
const client = new FetchClient({
    proxy: 'socks5://user:password@china-proxy.com:1080',
    timeout: 5000 // 5 seconds global timeout
});

// Get the hardened fetch function
const hardenedFetch = client.fetch;

async function run() {
    try {
        const response = await hardenedFetch('https://api.ipify.org?format=json');
        const data = await response.json();
        console.log('Your Proxy IP:', data.ip);
    } catch (err) {
        console.error('Fetch failed:', err.message);
    }
}

run();
```

- HTTP/HTTPS Proxy:

```TypeScript
const client = new FetchClient({
    proxy: 'http://1.2.3.4:8080'
});

const response = await client.fetch('https://google.com');
API Reference
new FetchClient(options)
options.proxy: (Optional) Proxy URL string (e.g., socks5://..., http://...).

options.timeout: (Optional) Default timeout in milliseconds for all requests.

client.fetch(url, init)
```

License
MIT © siakinnik
