# React Paginating

Simple lightweight pagination component.

The component applied `Function as Child Components` pattern. (You can read more
about this pattern
[here](https://medium.com/merrickchristensen/function-as-child-components-5f3920a9ace9)).

This approach allows you to fully control UI component and behaviours.

## Table content

* [Installation](https://github.com/ChoTotOSS/react-paginating#installation)
* [Usage](https://github.com/ChoTotOSS/react-paginating#usage)
* [Examples](https://github.com/ChoTotOSS/react-paginating#examples)
* [Props](https://github.com/ChoTotOSS/react-paginating#props)
* [Child callback functions](https://github.com/ChoTotOSS/react-paginating#child-callback-functions)
* [States](https://github.com/ChoTotOSS/react-paginating#states)
* [Alternatives](https://github.com/ChoTotOSS/react-paginating#alternatives)

## Installation

```bash
npm install --save react-paginating
```

or

```bash
yarn add react-paginating
```

## Usage

```js
import React from 'react';
import { render } from 'react-dom';
import Pagination from 'react-paginating';

const fruits = [
  ['apple', 'orange'],
  ['banana', 'avocado'],
  ['coconut', 'blueberry'],
  ['payaya', 'peach'],
  ['pear', 'plum']
];
const limit = 2;
const pageCount = 3;
const total = fruits.length * limit;

class App extends React.Component {
  constructor() {
    super();
    this.state = {
      currentPage: 1
    };
  }

  handlePageChange = page => {
    this.setState({
      currentPage: page
    });
  };

  render() {
    const { currentPage } = this.state;
    return (
      <div>
        <ul>
          {fruits[currentPage - 1].map(item => <li key={item}>{item}</li>)}
        </ul>
        <Pagination
          total={total}
          limit={limit}
          pageCount={pageCount}
          currentPage={currentPage}
        >
          {({
            pages,
            currentPage,
            hasNextPage,
            hasPreviousPage,
            previousPage,
            nextPage,
            totalPages,
            getPageItemProps
          }) => (
            <div>
              <button
                {...getPageItemProps({
                  pageValue: 1,
                  onPageChange: this.handlePageChange
                })}
              >
                first
              </button>

              {hasPreviousPage && (
                <button
                  {...getPageItemProps({
                    pageValue: previousPage,
                    onPageChange: this.handlePageChange
                  })}
                >
                  {'<'}
                </button>
              )}

              {pages.map(page => {
                let activePage = null;
                if (currentPage === page) {
                  activePage = { backgroundColor: '#fdce09' };
                }
                return (
                  <button
                    key={page}
                    style={activePage}
                    {...getPageItemProps({
                      pageValue: page,
                      onPageChange: this.handlePageChange
                    })}
                  >
                    {page}
                  </button>
                );
              })}

              {hasNextPage && (
                <button
                  {...getPageItemProps({
                    pageValue: nextPage,
                    onPageChange: this.handlePageChange
                  })}
                >
                  {'>'}
                </button>
              )}

              <button
                {...getPageItemProps({
                  pageValue: totalPages,
                  onPageChange: this.handlePageChange
                })}
              >
                last
              </button>
            </div>
          )}
        </Pagination>
      </div>
    );
  }
}

render(<App />, document.getElementById('root'));
```

## Props

### total

> `number`

Total results

### limit

> `number`

Number of results per page

### pageCount

> `number`

How many pages number you want to display in pagination zone.

### currentPage

> `number`

Current page number

## Child callback functions

### getPageItemProps

> `function({ pageValue: number, onPageChange: func })`

Allow to pass props and event to page item. When page is clicked, `onPageChange`
will be executed with param value `pageValue`.

**Note:** This callback function should only use for paging with state change.
If you prefer parsing page value from `query` url. **Please don't use this
callback function**

## States

### pages

> `array: [number]`

List of pages number will be displayed. E.g: [1, 2, 3, 4, 5]

### currentPage

> `number`

### previousPage

> `number`

### nextPage

> `number`

### totalPages

> `number`

### hasNextPage

> `boolean`

Check if it has `next page` or not.

### hasPreviousPage

> `boolean`

Check if it has `previous page` or not.

## Alternatives

If you don’t agree with the choices made in this project, you might want to
explore alternatives with different tradeoffs. Some of the more popular and
actively maintained ones are:

* [react-paginate](https://github.com/AdeleD/react-paginate)