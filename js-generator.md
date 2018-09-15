```js
function getOrder() {
    return 'Pizza'
}

function* logGenerator() {
    alert('How can I help you?')
    yield 'Step 1 completed'

    alert(`Your order was ${getOrder()}`)
    yield 'Step 2 completed'

    alert('Thanks for eating here')
    yield 'Step 3 completed'

    return 'Finished'
}

let gen = logGenerator()

gen.next(); // alert 'How can I help you?' then -> {value:'Step 1 completed', done: false}
gen.next(); // alert 'Your order was Pizza' then -> {value:'Step 2 completed', done: false}
gen.next(); // alert 'Thanks for eating here' then -> {value:'Step 3 completed', done: false}
gen.next(); // {value:'Finished', done: true}
```