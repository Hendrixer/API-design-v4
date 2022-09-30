## Unit test

A unit test is all about testing individual pieces of logic independently of each other. You have to make sure you write your code in a way that can be unit tested.

```ts
// not testable
const value = 100;
const action = () => {
  console.log(value);
};
``;
```

```ts
// testable
export const action = (value) => {
  console.log(value);
};
```

Using arguments vs creating closures and exporting your code are all great patterns to use when creating testable code. Now what does a unit test look like?

```ts
describe("user handler", () => {
  it("should do a thing", async () => {
    // .,...

    expect("something").toBe("something");
  });
});
```

This is how you might write a unit test in Jest. Each `it` block is an actual test where you usually call some function you want to test, and then create some assertion about what its return value should be. The `describe` function is just for organizing your test.

## Integraion test

Integration tests will test how an entire route works by actually making a request to observe what the API sent back and making assertions on that result. We can use jest along with supertest to run integration test.

```ts
import app from "../server";
import request from "supertest";

describe("POST /user", function () {
  it("responds with json", async () {
    const res = await request(app)
      .post("/user")
      .send({ username: "hello", password: "hola" })
      .set("Accept", "application/json")

    expect(res.headers["Content-Type"]).toMatch(/json/);
    expect(res.status).toEqual(200);
  });
});
```

In this test, we're using the `request` from supertest to make a request to `POST /user`, which in our app creates a user. We're sending up the required payload and expect to get a successful 200 when its done.
<br>
<br>
Now, go write some tests!
