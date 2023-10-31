[LICENSE]: https://github.com/rozhkovs/one-t/blob/HEAD/LICENSE
[AUTHOR]: https://github.com/rozhkovs

# 🥇 One Task (Test) 🥇
<p>
  <a href="https://github.com/rozhkovs/one-t/actions/workflows/tests.yml">
    <img src="https://github.com/rozhkovs/one-t/actions/workflows/tests.yml/badge.svg" alt="Rozhkov One Task tests" />
  </a>
  <a href="https://www.npmjs.com/package/@rozhkov/one-t">
    <img src="https://img.shields.io/npm/v/@rozhkov/one-t-test?color=brightgreen&label=npm%20package" alt="Current npm package version." />
  </a>
</p>

Sequential running of tasks with a cancellation token

## Installation
```shell
npm install one-task
# or
yarn add one-task
```

## Usage
```javascript
import oneTask from 'one-task';

const updateStateAsTransaction = async (cancellationToken) => {
  const rollback = async () => {/* restore state */};
  
  // asynchronous complex update
  
  if (cancellationToken.isCanceled) {
    await rollback();
    return;
  }
  
  // asynchronous complex update
}

const run = oneTask();
run(updateStateAsTransaction); // it will be called, but the token will be canceled
run(updateStateAsTransaction); // this task will be skipped
run(updateStateAsTransaction); // it will be run after completing the first task
```

## API
```typescript
interface ICancellationToken {
  readonly isCanceled: boolean;
}
type Task = (token: ICancellationToken) => Promise<void>;
type OneTask = (task: Task) => void;
```


## 👨‍💻 Author
[Sergey Rozhkov][AUTHOR]

## 📄 License

Rozhkov One Task is MIT licensed, as found in the [LICENSE] file.
