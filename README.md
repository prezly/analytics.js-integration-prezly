# analytics.js-integration-prezly

Custom Prezly integration for [Analytics.js][].

## Building

Running `npm run build` is going to create two files:
- `integration.js` To be included via bower or similar tools when creating a bigger bundle
- `integration.min.js` To be hosted on CDN and embeded via script tags

**IMPORTANT**
`PrezlyIntegration` variable is going to be defined on the `window` object once the scripts have been included.

## Usage

Following script can illustrate how to include and register the `PrezlyIntegration` presuming that **commercial** `analytics.js` has been loaded:

```js
analytics.ready(function () {
    if(PrezlyIntegration) {
        var integration = new PrezlyIntegration({
            apiHost: "//press.prezly.dev/segment",
            apiCallPayload: {
                room: meta_room || {}
            }
        });
        this.add(integration);
        integration.analytics = this;
        integration.once('ready', this.ready);
        integration.initialize();
    }

    analytics.page(); // Would send a request to http://press.prezly.dev/segment/p
    analytics.track('An event'); // Would send a request to http://press.prezly.dev/segment/t
});
```

For usage with **non-commercial** analytics.js check the [analytics.js fork](https://github.com/prezly-forks/analytics.js) which includes `PrezlyIntegration` and builds analytics.js.

## License

Released under the [MIT license](LICENSE).

[Analytics.js]: https://segment.com/docs/libraries/analytics.js/
