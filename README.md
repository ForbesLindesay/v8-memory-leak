# V8 memory leak demonstrator

Based on narrowing down https://github.com/ramondeklein/pug-email-templates-memleak this is causing a leak in pug.

## How to use

To demonstrate the problem first start this example program:

```sh
node --inspect v8-memory-leak.js
```

This will start the program that calls the `Function` constructor every 100ms and discards the result.

Now start Chrome and navigate to [chrome://inspect](chrome://inspect). You should see our `v8-memory-leak.js` in the list of targets. Start inspecting it and generate the first snapshot dump ("Take heap snapshot")

Wait a few seconds and take another heap snapshot.

Select the second snapshot and select "Objects allocated between snapshot 1 and snapshot 2" instead of "All objects". This list should be empty, but isn't because there is a memory leak.

You can see a similar thing by running record allocation timeline. The bars should turn gray once the memory is freed up, but they remain blue.
