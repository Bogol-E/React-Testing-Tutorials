# π» Section 7 - μ΅μ’ μΉμ

## π§βπ» μ΅μ’ μΉμ(1) - Happy Path Test

- Happy Path νμ€νΈλ, μλ¬μμ΄ μ νλ¦¬μΌμ΄μμ κ³ κ° νλ‘μ°μ ν¨κ» μλνλ νμ€νΈμ΄λ€.
- μ°λ¦¬μ μ±μ λ€μκ³Ό κ°μ νλ‘μ°λ₯Ό κ°λλ€.
  - 1. μ£Όλ¬Έ μμ±
  - 2. μμ½ νμ΄μ§ μ΄λ ν μ΄μ© μ½κ΄μ μμ©νκ³  μ μΆ
  - 3. νμΈ νμ΄μ§λ‘ μ΄λ, νμΈ νμ΄μ§μμ μ μ£Όλ¬Έμ ν΄λ¦­νλ©΄ OrderEntry νμ΄μ§λ‘ λλμκ°λ€.

<br />

### Debugging Tips

- screen.debug()
  - μ€ν¬λ¦° νΉμ DOMμ΄ ν΄λΉ μμ μμ μ΄λ€ λͺ¨μ΅μΈμ§ νμ€νΈ μΆλ ₯κ°μΌλ‘ νμΈν  μ μλ€. λ°λΌμ, νΉμ  ν­λͺ©μ μ°Ύκ±°λ λͺ» μ°Ύλ κ²½μ° μμΈμ νμνλ λ° μ μ©νλ€.
- await findBy...
  - μλ² νΈμΆμλ λΉλκΈ° μμμ΄ μμ λ `getBy...`λ₯Ό μ¬μ©νλ€ μ€ν¨νλ©΄ `await findBy`λ₯Ό μ¬μ©ν΄μΌ νλ€. `getBy...`λ₯Ό μ¬μ©νλ€ μ€ν¨νλ©΄ λΉλκΈ°μΈμ§ νμΈνκ³  `await findBy`λ₯Ό μ¬μ©ν΄μΌ νλμ§λ μκ°ν΄ λ΄μΌνλ€.
- νμ€νΈ μλ¬ μΆλ ₯ κ°μ μ£Όμ κΉκ² νμΈν΄λΌ.
- μ΄λ€ λ¨μΈμ΄ μ€ν¨νλμ§, νμ€νΈ λ΄ μ΄λ€ μ€μ λ¬Έμ κ° μλμ§λ νμΈν΄μΌ νλ€.
- νμ€νΈμ μ€μ  μ½λ μ€μ λ­κ° λ¬Έμ μΈμ§ νμ€νμ§ μμ κ²½μ°μλ λ―Έλ¦¬ μμ±λ μ½λλ‘ μμμ μ¬μ©νλ μ½λλ₯Ό λμ²΄ν΄λΌ.
  - μ½λμ νμ€νΈ λͺ¨λ μμ±νλ μ€λ¬΄λΌλ©΄ μ¬μ©νκΈ° μ΄λ €μ΄ μ΅μμ΄μ§λ§ μ°μ΅ν  λλ μ½λμ νμ€νΈ μ€ λ¬Έμ κ° λ­μ§ νμνλ κ°κ°μ κΈ°λ₯΄κΈ°μ μ μ©ν νμ΅ λκ΅¬μ΄λ€.

<br />

### μ£Όμ νμ€νΈ μλ¬μ ν΄κ²°μ±

- Unable to find role="role"
  - μμ±μ μ΄λ¦μ μ§μ νμ§ μμμ λ°μνλ μλ¬μ΄λ€.
  - μ΄λ₯Ό ν΄κ²°νλ €λ©΄ μ΄λ¦μ μ­μ νκ³  νμΈνκ±°λ, screen.debug()λ₯Ό μ΄μ©νλ©΄ λλ€.
- Warning: An update to component inside a test was not wrapped in act(...)
  - μλ°μ΄νΈκ° actλ‘ λνλμ§ μμλ€λ κ²½κ³  λ¬Έκ΅¬μ΄λ€. μ΄λ νμ€νΈ μλ£ νμ μΆκ°μ μΌλ‘ μλ°μ΄νΈκ° μ§νλμ λ λ°μνλ€.
  - μΈλ§μ΄νΈλ μ»΄ν¬λνΈμ React μν μλ°μ΄νΈκ° μλλ κ²½μ° actλ‘ λννμ§ μμ λ°μν μλ¬μ μμΈμ΄ λμΌνλ€.
  - μ΄λ₯Ό ν΄κ²°νλ €λ©΄ `await findBy` λ₯Ό μ¬μ©ν΄ ν΄κ²°ν  μ μλ€.
- Error: connect ECONNREFUSED 127.0.0.1
  - μ°κ²°μ΄ κ±°λΆλλ€λ©΄ νΈμΆλ λΌμ°νΈ λ° λ©μλμ μ°κ΄λ MSW νΈλ€λ¬κ° μλ€λ μλ―Έμ΄λ€.
  - λΌμ°νΈμ λ©μλλ₯Ό λͺ¨λ νμΈν΄λ΄μΌ λλ€.

<br />

## π§βπ» μ΅μ’ μΉμ(2) - orderPhase νμ€νΈ μ½λ

```js
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import App from "../App";

test("order phases for happy path", async () => {
  // render app
  render(<App />);

  // add ice cream scoops and toppings
  const vanillaInput = await screen.findByRole("spinbutton", {
    name: "Vanilla",
  });
  userEvent.clear(vanillaInput);
  userEvent.type(vanillaInput, "1");

  const chocolateInput = screen.getByRole("spinbutton", {
    name: "Chocolate",
  });
  userEvent.clear(chocolateInput);
  userEvent.type(chocolateInput, "2");

  const cherriesCheckbox = screen.getByRole("checkbox", {
    name: "Cherries",
  });
  userEvent.click(cherriesCheckbox);

  // find and click order button
  const orderSummaryButton = screen.getByRole("button", {
    name: /order sundae!/i,
  });
  userEvent.click(orderSummaryButton);

  // μνκ° λ³κ²½λκΈ° λλ¬Έμ μ΄λ₯Ό κΈ°λ€λ €μ€λ€
  // check summary information based on order
  const summaryHeading = await screen.findByRole("heading", {
    name: "Order Summary",
  });
  expect(summaryHeading).toBeInTheDocument();

  const scoopsHeading = screen.getByRole("heading", {
    name: "Scoops: $6.00",
  });
  expect(scoopsHeading).toBeInTheDocument();

  const toppingsHeading = screen.getByRole("heading", {
    name: "Toppings: $1.50",
  });
  expect(toppingsHeading).toBeInTheDocument();

  // check summary option items
  expect(screen.getByText("1 Vanilla")).toBeInTheDocument();
  expect(screen.getByText("2 Chocolate")).toBeInTheDocument();
  expect(screen.getByText("Cherries")).toBeInTheDocument();

  // accept terms and conditions and click button to confirm order
  const tcCheckbox = screen.getByRole("checkbox", {
    name: /terms and conditions/i,
  });
  userEvent.click(tcCheckbox);

  const confirmOrderButton = screen.getByRole("button", {
    name: /confirm order/i,
  });
  userEvent.click(confirmOrderButton);

  // μνκ° λ³κ²½λκΈ° λλ¬Έμ μ΄λ₯Ό κΈ°λ€λ €μ€λ€
  // confirm order number on confirmation page
  const thankYouHeader = await screen.findByRole("heading", {
    name: /thank you/i,
  });
  expect(thankYouHeader).toBeInTheDocument();

  const orderNumber = await screen.findByText(/order number/i);
  expect(orderNumber).toBeInTheDocument();

  // click "new order" button on confirmation page
  const newOrderButton = screen.getByRole("button", {
    name: /create new order/i,
  });
  userEvent.click(newOrderButton);

  // μνκ° λ³κ²½λκΈ° λλ¬Έμ μ΄λ₯Ό κΈ°λ€λ €μ€λ€
  // check that scoops and toppings subtotals have been reset
  const scoopsTotal = await screen.findByText("scoops total: $0.00");
  expect(scoopsTotal).toBeInTheDocument();

  const toppingsTotal = screen.getByText("toppings total: $0.00");
  expect(toppingsTotal).toBeInTheDocument();
});
```

<br />

## π§βπ» μ΅μ’ μΉμ(3) - Jest Mock(λͺ¨μ) ν¨μ

- Jestλ mockν¨μ μ¦ κ°μ§ ν¨μλ₯Ό μμ±ν  μ μλλ‘ `jest.fn()`μ μ κ³΅νλ€.
- κ·Έλ¦¬κ³  μ΄ mock ν¨μλ μΌλ° μλ°μ€ν¬λ¦½νΈ ν¨μμ λμΌν λ°©μμΌλ‘ μΈμλ₯Ό λκ²¨ νΈμΆ ν  μ μλ€.

```js
const mockFn = jest.fn();
mockFn();
mockFn(1);
mockFn("a");
mockFn([1, 2]);
```

- μ mock ν¨μμ νΈμΆ κ²°κ³Όλ λͺ¨λ `undefined`μ΄λ€. μ΄λ€ κ°μ λ¦¬ν΄ν΄μΌν μ§ μμ§ μλ €μ£Όμ§ μμκΈ° λλ¬Έμ΄λ€.

```js
mockFn.mockReturnValue("μΌλ° νμ€νΈ!");
console.log(mockFn()); // μΌλ° νμ€νΈ!
```

- `mockReturnValue(λ¦¬ν΄ κ°)` ν¨μλ₯Ό μ΄μ©ν΄μ κ°μ§ ν¨μκ° μ΄λ€ κ°μ λ¦¬ν΄ν΄μΌν μ§ μ€μ ν΄ μ€ μ μλ€.

```js
mockFn.mockResolvedValue("λΉλκΈ° νμ€νΈ!");
mockFn().then((result) => {
  console.log(result); // λΉλκΈ° νμ€νΈ!
});
```

- λΉμ·ν λ°©μμΌλ‘ `mockResolvedValue(Promiseμ resolve κ°)` ν¨μλ₯Ό μ΄μ©ν΄μ κ°μ§ λΉλκΈ° ν¨μλ₯Ό λ§λ€ μ μλ€.

```js
mockFn.mockImplementation((name) => `I am ${name}!`);
console.log(mockFn("Dale")); // I am Dale!
```

- λΏλ§ μλλΌ `mockImplementation(κ΅¬ν μ½λ)` ν¨μλ₯Ό μ΄μ©νλ©΄ μμ ν΄λΉ ν¨μλ₯Ό ν΅μ§Έλ‘ μ¦μν΄μ μ¬κ΅¬νν΄λ²λ¦΄ μλ μμ΅λλ€.

### mock ν¨μ μ¬μ© μ΄μ 

- νμ€νΈλ₯Ό μμ±ν  λ mock ν¨μκ° μ μ©ν μ΄μ λ mock ν¨μλ μμ μ΄ μ΄λ»κ² νΈμΆλμλμ§ λͺ¨λ κΈ°μ΅νλ€λ μ μ΄λ€.

```js
mockFn("a");
mockFn(["b", "c"]);

expect(mockFn).toBeCalledTimes(2);
expect(mockFn).toBeCalledWith("a");
expect(mockFn).toBeCalledWith(["b", "c"]);
```

- μμ κ°μ΄ mock ν¨μ μ© μ€κ³λ Jest MatcherμΈ `toBeCalled` ν¨μλ₯Ό μ¬μ©νλ©΄ mock ν¨μκ° λͺλ² `νΈμΆ`λμκ³  `μΈμ`λ‘ λ¬΄μμ΄ λμ΄μμλμ§λ₯Ό κ²μ¦ν  μ μμ΅λλ€.

<br />
