# chatgpt-search

Turn Firefox search into a ChatGPT search so you don't have to read Google AI mode 🤭

## Why this exists

There is already a Firefox extension that does this.

The implementation is very small, but the extension still requires access to `chatgpt.com`. That means installing it also means trusting the developer and any future updates they publish.

For functionality this simple, I preferred to keep the implementation local and auditable.

## What it does

Firefox sends address-bar searches to:

```text
https://chatgpt.com/?q={searchTerms}&hints=search&ref=ext
```

The extension also sets:

```js
document.documentElement.dataset.searchExtension = "1";
```

on ChatGPT pages.

## What it does not do

- no analytics
- no remote code
- no third-party dependencies
- no history permission
- no cookie permission
- no access to unrelated websites

The content script only runs on `chatgpt.com`.

## Run it yourself

Clone the repo:

```bash
git clone https://github.com/YOUR_USERNAME/chatgpt-search.git
cd chatgpt-search
```

Open Firefox and go to:

```text
about:debugging#/runtime/this-firefox
```

Click **Load Temporary Add-on** and select:

```text
manifest.json
```

Firefox will load the extension for the current session.

To verify the page marker is active, open ChatGPT, open DevTools, and run:

```js
document.documentElement.dataset.searchExtension
```

It should return:

```text
"1"
```

Then type a search into the Firefox address bar and confirm it opens ChatGPT with the query in `?q=`.

## Permanent install

Temporary extensions are removed when Firefox restarts.

For a permanent install, package and sign the extension through Mozilla Add-ons, then install the signed `.xpi` in Firefox.

Install Mozilla's extension tooling:

```bash
npm install --global web-ext
```

From the repo root:

```bash
web-ext build
```

This creates the packaged extension under:

```text
web-ext-artifacts/
```

For permanent installation in standard Firefox, the extension must be signed by Mozilla.

Submit it through Mozilla Add-ons:

https://addons.mozilla.org/developers/

Choose **Submit a New Add-on**, upload the packaged extension, and select self-distribution if you only want a signed `.xpi` rather than a public listing.

Once Mozilla signs it, download the signed `.xpi`.

In Firefox, open:

```text
about:addons
```

Then:

**Extensions → gear icon → Install Add-on From File**

Select the signed `.xpi`.

Firefox will then keep the extension installed across restarts.
