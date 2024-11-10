```js
// testing library
function expect(arg) {
  if (typeof arg === "function") {
    try {
      arg();
    } catch (err) {
      return {
        toThrow: () => {}
      };
    }
  }

  const not = {
    toBe
  };

  function toBe(val) {
    const isEqual = Object.is(arg, val);
    if (typeof this === not) {
      if (isEqual) throw new Error();
    } else if (!isEqual) throw new Error();
    return true;
  }

  return {
    toBe,
    not
  };
}

const test = function (testStr, cb) {
  try {
    cb();
    console.log(`✓ [PASS] ${testStr}!!`);
  } catch (err) {
    console.log(`❌ [FAIL] ${testStr} failed!!`);
  }
};

// my source
const mySum = (a, b) => {
  if (typeof a === "number" && typeof b === "number") return a + b;
  throw new Error("Types should be number");
};

// My tests
test("It should pass when 2 numbers are passed", () => {
  expect(mySum(1, 2)).toBe(3);
});

test("It should throw when wrong numbers are passed", () => {
  expect(mySum.bind(null, 4, "2")).toThrow();
});

```

Demo: https://codepen.io/siri404/pen/abePzgW
