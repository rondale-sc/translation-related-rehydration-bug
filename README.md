# translation-related-rehydration-bug

This application is designed to reproduce a bug found in rehydration apps.

When using the `t` helper from Ember i18n whose key resolves to an empty string `""` glimmer will throw the following error:

```
Uncaught TypeError: Cannot read property 'parentNode' of null
    at RehydrateBuilder.remove (vendor.js:19840)
    at RehydrateBuilder.__closeBlock (vendor.js:19807)
    at RehydrateBuilder.popBlock (vendor.js:18263)
    at VM.exit (vendor.js:19416)
    at Object.evaluate (vendor.js:15864)
    at AppendOpcodes.evaluate (vendor.js:14781)
    at LowLevelVM.evaluateSyscall (vendor.js:18159)
    at LowLevelVM.evaluateInner (vendor.js:18131)
    at LowLevelVM.evaluateOuter (vendor.js:18123)
    at VM.next (vendor.js:19512)
```

The error only happens with the `RehydrateBuilder` when `EXPERIMENTAL_RENDER_MODE_SERIALIZE` is set.  To reproduce the bug:

- download this application
- `yarn install`
- `EXPERIMENTAL_RENDER_MODE_SERIALIZE=true ember s`
