```js
// testing library
function expect(arg) {
  if (typeof arg === 'function') {
    try {
      arg()
    } catch (err) {
      return {
        toThrow: () => true
      }
    }
  }
   return {
     toBe: function(val) {
       if (Object.is(arg, val)) return true
       return new Error('err')
     },
     not: {
       toBe: function(val) {
         if (Object.is(arg, val)) throw new Error()
         return true
       }
     },
   }
}

const test = function(testStr, cb) {
  try {
    cb()
    console.log(`✓ ${testStr} passed!!`)
  } catch(err) {
    console.log(`❌ ${testStr} failed!!`)
  }
}

// my source
const mySum = (a, b) => {
  if (typeof a === 'number' && typeof b === 'number')
  return a + b
  throw new Error('Types should be number')
}

// My tests
test('It should pass when 2 numbers are passed', () => {
  expect(mySum(1, 2)).toBe(3)
})

test('It should fail when wrong numbers are passed', () => {
  expect(mySum.bind(null, 4, '2')).toThrow()
})
```

Demo: https://codepen.io/siri404/pen/abePzgW
