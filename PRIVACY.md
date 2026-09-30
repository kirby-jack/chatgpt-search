# Privacy policy

This extension makes ChatGPT the default Firefox search engine when the user approves the change.

When you submit an address-bar search, Firefox sends the search terms directly to `https://chatgpt.com/` in the URL's `q` parameter, together with `hints=search` and `ref=ext`. Search terms are therefore disclosed to OpenAI. OpenAI's handling of those terms is governed by its [privacy policy](https://openai.com/policies/privacy-policy/).

The extension runs a single content-script statement on HTTPS pages at `chatgpt.com` and its subdomains. It sets `document.documentElement.dataset.searchExtension` to `"1"`, allowing the website to recognize that the extension is installed.

The extension does not read or store conversations, store search terms, collect analytics, or make network requests from its JavaScript. It sends no data to the extension's developer. Firefox and ChatGPT may retain search information through their own normal operation.

The complete source is available at [kirby-jack/chatgpt-search](https://github.com/kirby-jack/chatgpt-search). Questions can be raised through the repository's [issue tracker](https://github.com/kirby-jack/chatgpt-search/issues).
