# rularner.github.io

Landing site for a few small personal projects by Rusty Larner.

## SF Transit Watch

An Apple Watch app for San Francisco Muni arrival predictions, powered by the
[511.org](https://511.org/) transit API. The app runs on-device and talks to
511 directly using an API key you supply; nothing routes through this site
except the one-time key handoff described below.

If you have SF Transit Watch installed on your Apple Watch, you can register
your 511 API key by tapping a link of the form:

```
https://rularner.github.io/sftransitwatch/key?k=YOUR_511_KEY
```

watchOS opens the app directly via Universal Links and saves the key. If you
land on that URL in a regular browser instead, you'll see
[a short explainer page](./sftransitwatch/key/) with instructions for
forwarding the link to your watch.
