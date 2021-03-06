<h1 align="center">
  <a href="https://redux-model.github.io/redux-model">
    Redux Model
  </a>
</h1>

[中文](./README.md)

Redux Model is created to enhance original redux framework, which has complex flow and lots of boilerplate.

Lots of famous state framework are designed for JS users. They totally follow design mode and hide everything you needn't see, it means you are difficult to combine these frameworks with typescript unless you inject `type interface` manually. Fortunately, Redux-Model is specially designed for typescript, feel free to inject once, use everywhere.

[![License](https://img.shields.io/github/license/redux-model/redux-model)](https://github.com/redux-model/redux-model/blob/master/LICENSE)
[![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/redux-model/redux-model/CI/master)](https://github.com/redux-model/redux-model/actions)
[![Codecov](https://img.shields.io/codecov/c/github/redux-model/redux-model)](https://codecov.io/gh/redux-model/redux-model)


# Features

* Highest coding efficiency
* Modify reducer by MVVM
* **👍Absolutely 100% static type checking with typescript**
* Provide http service, combine loading and throttle for each request action
* Support react/vue hooks
* Support persist

# Installation

### React or React-Native
```bash
npm install @redux-model/react redux react-redux
```

### Vue v3
```bash
npm install @redux-model/vue redux
```

### Taro v3
```bash
npm install @redux-model/taro redux react-redux
```

### Others
* For `taro < v3`, install @redux-model/taro@6.9.2 instead
* For `vue < v3`, install @redux-model/vue@6.9.2 instead

# Define Model
```typescript
interface Response {
  id: number;
  name: string;
}

interface Data {
  counter: number;
  users: Partial<{
    [key: string]: Response;
  }>;
}

class TestModel extends Model<Data> {
  increase = this.action((state) => {
    state.counter += 1;
  });

  getUser = $api.action((id: number) => {
    return this
      .get<Response>(`/api/users/${id}`)
      .onSuccess((state, action) => {
        state.users[id] = action.response;
      });
  });

  protected initialState(): Data {
    return {
      counter: 0,
      users: {},
    };
  }
}

export const testModel = new TestModel();
```

# With React Hooks
```typescript jsx
import React, { FC } from 'react';

const App: FC = () => {
  const counter = testModel.useData((data) => data.counter);
  const loading = testModel.getUser.useLoading();

  const increase = () => {
    testModel.increase();
    testModel.getUser(3);
  };

  return (
    <button onClick={increase}>
      {loading ? 'Waiting...' : `You clicked ${counter} times`}
    </button>
  );
};

export default App;
```

# With Vue Hooks
```vue
<template>
  <button @click="increase">
    {{loading.value ? 'Waiting...' : `You clicked ${counter.value} times`}}
  </button>
</template>

<script>
export default {
  setup() {
    const increase = () => {
      testModel.increase();
      testModel.getUser(3);
    };

    const counter = testModel.useData((data) => data.counter);
    const loading = testModel.getUser.useLoading();

    return {
      increase,
      counter,
      loading,
    };
  }
};
</script>
```

# With Redux Connect
```typescript jsx
import React, { Component } from 'react';
import { connect } from 'react-redux';

type Props = ReturnType<typeof mapStateToProps>;

class App extends Component<Props> {
  increase() {
    testModel.increase();
    testModel.getUser(3);
  }

  render() {
    const { loading, counter } = this.props;
    return (
      <button onClick={this.increase}>
          {loading ? 'Waiting...' : `You clicked ${counter} times`}
      </button>
    );
  }
}

const mapStateToProps = () => {
  return {
    counter: testModel.data.counter,
    loading: testModel.getUser.loading,
  };
};

export default connect(mapStateToProps)(App);
```

# Demos
* [Counter](https://codesandbox.io/s/redux-model-react-counter-zdgjh)
* [Persist](https://codesandbox.io/s/redux-model-react-persist-uwhy8)
* [Todo List](https://codesandbox.io/s/redux-model-react-todo-list-zn4nv)
* [Request](https://codesandbox.io/s/redux-model-react-request-1ocyn)
* [Request Throttle](https://codesandbox.io/s/redux-model-react-request-throttle-77mfy)
* [Listener](https://codesandbox.io/s/redux-model-react-listener-p7khk)
* [Action in Action](https://codesandbox.io/s/redux-model-react-action-in-action-oewkv)
* [Compose](https://codesandbox.io/s/redux-model-react-compose-42wrc)

# Documents

Here is the [document](https://redux-model.github.io/redux-model)

---------------------

Feel free to use it and welcome to send PR to me.
