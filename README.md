
# Module 10

Muhammad Brian Subekti 2306256444

## 1.2 Understanding how it works.

### The screenshot

![Program Output](img\First_img.png)

When I call `spawner.spawn(async { ... })`, the asynchronous task is merely enqueued for later execution rather than running immediately. The following synchronous call, `println!("Brian's Komputer: hey hey");`, executes right away, printing “hey hey” before the executor ever begins polling the spawned future. Only after dropping the spawner and invoking `executor.run()` does the executor pull tasks off its queue to start processing them.

Inside the executor’s loop, the future is polled for the first time, which prints “howdy!” and sets up a 2-second timer before returning `Poll::Pending`. When the timer fires, it re-queues the task, and on the second poll the future completes, printing “done!”. This two-stage polling model, combined with the initial synchronous print in `main`, yields the observed output sequence.


