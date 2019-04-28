# Cypress.io 

---

Installing Cypress

------

```
npm i --save-dev cypress

yarn add cypress --dev
```

Note: https://docs.cypress.io/guides/getting-started/installing-cypress.html#System-requirements

---

Running Cypress

------

```
$(npm bin)/cypress open
npx cypress open
yarn cypress open
```

Note: https://docs.cypress.io/guides/getting-started/installing-cypress.html#System-requirements

---

Setting up your first test

------

Create a `*_spec.js` file in `cypress/integration` folder this will be picked up by the cypress runner.

Note: https://docs.cypress.io/guides/getting-started/writing-your-first-test.html#Add-a-test-file

---

Writing your first test

Note: https://docs.cypress.io/guides/getting-started/writing-your-first-test.html

------

Successful Test 

```js
describe('My First Test', () => {
  it('Does not do much!', () => {
    expect(true).to.equal(true);
  });
});
```

------

Failing Test

```js
describe('My First Test', () => {
  it('Does not do much!', () => {
    expect(true).to.equal(false);
  });
});
```

---

Writing a real test

------

3 Phases 

0. Setup Test
0. Run Test
0. Verify Test

---

API

------

For most things you'll use the following commands 

- `get` an item on the page
- `click` a button or link
- `type` with the keyboard
- `select` an item from a drop down list

------

API Documentation can be found here: 

https://docs.cypress.io/api/api/table-of-contents.html

I don't have time to go over it all with you



