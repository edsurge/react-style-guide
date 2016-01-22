# EdSurge React Style Guide

![React](https://cloud.githubusercontent.com/assets/992008/12514949/baf26484-c0da-11e5-8ffa-b4e6be7d62ad.png)

## Skip `isRequired` for `propTypes`

- Validating w/ `isRequired` has not been useful for our codebase. Remove them.
- But if we're open sourcing a component, use it.

#### No:

```js
static propTypes = {
  foo: PropTypes.array.isRequired
};
```

#### Yes:

```js
static propTypes = {
  foo: PropTypes.array
};
```

## Use functional components if the component only has `render`

#### No:

```
export default class Foo extends Component {
  render () {
    return <div></div>
  }
}
```


#### Yes:
export default ({ ... }) => (
  <div></div>
)


-----------------------------------------------------------------------

![Redux](https://cloud.githubusercontent.com/assets/992008/12514962/c5501bce-c0da-11e5-93b2-5af0ed807061.png)

## Use `defaultProps` instead of `select` (`mapStateToProps`) to assign default values coming in from the store/do null check

- You can use `defaultProps` or `select` (`mapStateToProps`) to assign default values. You may need this to avoid unexpected errors b/c of passing `undefined`.
- Prefer `defaultProps` for this because that's what it's meant for. Keep `select` to do just one thing: selecting stuff from state.

#### No:

```js
render () {
  this.props.list.map(...) // Can skip null check
}

...

function select(state) {
  return {
    list: state.list || []
  }
}

export default connect(select)(...)
```

#### Yes:

```js
static defaultProps = {
  list: []
};

render () {
  this.props.list.map(...) // Can skip null check
}

...

function select(state) {
  return {
    list: state.list
  }
}

export default connect(select)(...)
```
