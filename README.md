# socket-queue
A Framework to build Distributed Socket Clusters and Workers. Ex: Distributed worker Pool
Supports persistence via DB Integration can be also in Memory or Loosy

## Usage
Thread 1
```js
import Queue from 'socket-queue' 

const worker = new Queue()

const job = worker.createJob({x: 2, y: 3})
job.save();
job.on('succeeded', (result) => {
  console.log(`Received result for job ${job.id}: ${result}`);
});

// Process jobs from as many servers or processes as you like
worker.process(function (job, done) {
  console.log(`Processing job ${job.id}`);
  return done(null, job.data.x + job.data.y);
});

worker.destroy(function (err) {
  if (!err) {
    console.log('Queue was destroyed');
  }
});

worker.destroy()
  .then(() => console.log('Queue was destroyed'));

```
