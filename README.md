<p align="center">
<img height="140" src="media/unmodal.png" alt="React Unmodal Banner" align="center" />
</p>

<br />

<div align="center"><strong>Promise-based utility to control modal states in React</strong></div>
<div align="center">Zero-dependency library that easily integrates with your existing UI components and allows you to naturally use modals in React</div>

<br />

<!-- TODO: Badges -->

<br/>

## Quick Features

- **Promise based**: open your modal with a simple function call and `await` for the result.
- **Uncontrolled**: open/close your modal from anywhere in the code (even inside the modal itself).
- **Decoupled**: no need to import a modal component to use it. Modals can be managed by ID.
- **Tiny**: zero-dependency to keep your bundle size under control: `~1.5kB`.
- **Easy integration**: easily integrate with any UI library.
- **Lazy-loading**: delay the rendering of your modal component until it's open.

## Examples

Try it on CodeSandbox or browse the [examples folder](https://github.com/thiagozf/react-unmodal/tree/main/examples).

[![Unmodal Examples](https://codesandbox.io/static/img/play-codesandbox.svg)](https://githubbox.com/thiagozf/react-unmodal/tree/main/examples/basic)

## Basic Usage

```jsx
import Unmodal from 'react-unmodal'
import MyModal from './MyModal'

// ...
const result = await Unmodal.open(MyModal, { myModalProp: 'value' })
// Do something with result
```

## Use-Case: Confirmation Modal

```jsx
/**
 * confirm.js
 */
import { Unmodal, useModal } from 'react-unmodal'

// Register your Confirm modal wrapping it with `Unmodal.create`
const Confirm = Unmodal.create(
  ({ title = 'Confirmation', message = 'Do you confirm this action?' }) => {
    // useModal hook to control UI components
    const modal = useModal()

    // Once resolved, automatically close the modal
    const resolve = value => () => {
      modal.resolve(value)
      modal.close()
    }

    // "title" and "message" are props sent with "modal.open()"
    return (
      <Modal open={modal.isOpen} onClose={modal.close} onExited={modal.remove}>
        <div>{title}</div>
        <div>{body}</div>
        <Button onClick={resolve(true)}>Yes</Button>
        <Button onClick={resolve(false)}>No</Button>
      </Modal>
    )
  }
)

// Create a custom confirm function
export const confirm = props => Unmodal.open(Confirm, props)

/**
 * page.js
 */
import { confirm } from './confirm'

export const Page = () => {
  const handleClick = async () => {
    const confirmed = await confirm({
      title: 'Are you sure?',
      message: 'This action is irreversible',
    })
    console.log(confirmed)
  }

  return <Button onClick={handleClick}>Action</Button>
}

/**
 * app.js
 */
import { Unmodal } from 'react-unmodal'

function App() {
  // Remember to wrap your app with Unmodal.Provider
  return (
    <Unmodal.Provider>
      <Page />
    </Unmodal.Provider>
  )
}
```

# Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

<!-- Force 3 -->
