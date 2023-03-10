# ๐ป Section 6 - Provider์ ๋ํ๋ ์ปดํฌ๋ํธ ํ์คํธ

## ๐งโ๐ป Provider(1) - ํ์คํธ ์๋ ฅ๋ ์ฑ์ฐ๊ธฐ: ์๊ณ ํ์คํธ

- [getByText](https://testing-library.com/docs/queries/bytext/)๋ก ์์๋ฅผ ๊ฐ์ ธ์ฌ ๋ 2๋ฒ์งธ ์ธ์๋ก exact๋ผ๋ ์ต์์ด ์กด์ฌํ๋ค. ์ด๋ ๊ธฐ๋ณธ์ ์ผ๋ก true๋ก ์ค์ ๋์ด ์์๋๋ฐ `๋ถ๋ถ์  ๋งค์น`์ผ ๋๋ exact๋ฅผ `false`๋ก ์ค์ ํด์ค์ผ ํ๋ค.

```js
// totalUpdates.test.js
test("update scoop subtotal when scoops change", () => {
  render(<Options optionType={"scoops"} />);

  // make sure total starts out $0.00
  const scoopsSubtotal = screen.getByText("Scoops total: $", { exact: false });
});
```

<br />

- ํ์คํธ๋ฅผ ์๋ฐ์ดํธํ  ๋๋ง๋ค ๊ฐ์ฅ ๋จผ์  ํ๋ฉด ์ข์ ์์์ `clear(element)`๋ก ์์๋ฅผ ์ญ์ ํ๋ ๊ฒ์ด๋ค. ์๋ํ๋ฉด ๊ทธ ์ด์ ์ ๋ฌด์จ ๊ฐ์ด ์์๋์ง ์ ์ ์๊ธฐ ๋๋ฌธ์ด๋ค.
- `type` ์ด๋ฒคํธ๋ ์์๋ฅผ ๊ฐ์ ธ์์ ํ์คํธ ์๋ ฅ์ ํ์คํธ ํ  ์์๋ค. ์ฐธ๊ณ ๋ก ์ธ์๋ก ๋ฌธ์์ด์ ๋ฃ์ด์ค์ผ ํ๋ค.
- ์ฐธ๊ณ ๋ก ์๋ ์์ ์์๋ ๋๋ฒ์งธ์ธ์๋ก 1์ ์คฌ๋๋ฐ spinbutton์ 1ํ ๋๋ ๋ค๋ ๋ป์ด๋ค.
- ์๋กญ๊ฒ ์์๋ณด๋ [spinbutton](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/spinbutton_role)๋ ๋ฌธ์๋ฅผ ์ฐธ๊ณ ํ์.

```js
// totalUpdates.test.js
test("update scoop subtotal when scoops change", async () => {
  // ...

  // update vanilla scoops to 1 and check the subtotal
  // ์๋ฒ์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ๊ธฐ์ ์ ์ฑ์ฐ์ง ์๊ธฐ ๋๋ฌธ์ async/await, find๋ฅผ ์ด์ฉ
  const vanillaInput = await screen.findAllByRole("spinbutton", {
    name: "Vanilla",
  });

  userEvent.clear(vanillaInput);
  userEvent.type(vanillaInput, "1"); // 2๋ฌ๋ฌ ์ฆ๊ฐ
  await waitFor(() => expect(scoopsSubtotal).toHaveTextContent("2.00"));
});
```

<br />

## ๐งโ๐ป Provider(2) - ํ์คํธ ์ค์ ์ Context์ถ๊ฐํ๊ธฐ

- React์ฝ๋์์ Context Provider ์ฝ๋๋ฅผ ์์ฑํ๊ณ  ์ ์ฉ์ ํด์คฌ๋๋ฐ ํ์คํธ๋ฅผ ์งํํด๋ณด๋ฉด ์์ฒญ๋ ์๋ฌ๊ฐ ๋ฐ์ํ๋ค. `(context/OrderDetails)`
- ์ด๋ ๊ธฐ์กด์ ํ์คํธ ์ฝ๋์ Context๋ฅผ ์ ๊ณตํ์ง ์์๊ธฐ ๋๋ฌธ์ด๋ค. ์ฆ, ํ์คํธ ๋ด์์ Options ์ปดํฌ๋ํธ๋ฅผ ์ํ Context๋ฅผ ์ ๊ณตํด์ผ๋จ์ ์๋ฏธํ๋ค. ์ด๋ wrapper์ต์์ ์ด์ฉํ๋ค.
- ๊ธฐ์กด์ ์์ฑํ OrderDetailsProvider๋ฅผ wrapper์ ์ถ๊ฐํด์ค๋ค.
- Context๋ฟ๋ง ์๋๋ผ `Redux Provider`, `Router` ๋ฑ์ ์ถ๊ฐํ  ์ ์๋ค. ์ฆ, ํ์คํธ๋ฅผ ์ํด ์ปดํฌ๋ํธ๋ฅผ ๋ํํ  ์ ์๋ ๊ฒ์ ๋ญ๋  ๊ฐ๋ฅํ๋ค.

```js
test("update scoop subtotal when scoops change", async () => {
  render(<Options optionType={"scoops"} />, { wrapper: OrderDetailsProvider });
  // ...
});
```

<br />

## ๐งโ๐ป Provider(3) - Provider Wrapper ์ ์ฉ

- [Custom Render](https://testing-library.com/docs/react-testing-library/setup/#custom-render)
- Wrapper๋ฅผ ์ด์ฉํ๋ฉด Provider๋ฅผ ์ฐ๋ฆฌ๊ฐ ๋ ๋๋งํ๋ ๋ชจ๋  ์ปดํฌ๋ํธ์ ํ์คํธ์ ์ ์ญ์ ์ผ๋ก ์ ์ฉํด ๊ฐ๋ณ ์์์ด ํ์ ์๊ฒ๋ ํ  ์ ์๋ค.

```js
//test-utils/testing-library-utils.js
import { render } from "@testing-library/react";
import { OrderDetailsProvider } from "../contexts/OrderDetails";

const customRender = (ui, options) => {
  return render(ui, { wrapper: OrderDetailsProvider, ...options });
};

// re-export
export * from "@testing-library/react";

// override render method
export { customRender as render };
```

- ์์ ๊ฐ์ด test utilsํจ์๋ฅผ ๋ง๋ ๋ค.
- `@testing-library/react`์ ๋ชจ๋ ๊ฑธ re-exportํ๋ฉฐ `customRender`๋ฅผ ํตํด์ ์ฐ๋ฆฌ๊ฐ ๋ํํ๊ณ ์ ํ๋ ๋ด์ฉ์ ์ถ๊ฐํด exportํ๋ค.

```js
import { render, screen } from "../../../test-utils/testing-library-utils";
import Options from "../Options";

test("display image for each scoop option from server", async () => {
  render(<Options optionType="scoops" />);
  // ...
});
```

- ์ด๋ฅผ ์์๊ฐ์ด test-utils/testing-library-utils๋ฅผ importํด์ ์ฌ์ฉํ๋ฉด ๋๋ค.

<br />

## ๐งโ๐ป Provider(4) - update toppings subtotal

- scoops, toppings ์ subTotal์ ๊ตฌํ๋ ํ์คํธ๋ ๊ฑฐ์ ๋งฅ๋ฝ์ด ๋น์ทํ๋ค.

```js
test("update toppings subtotal when toppings change", async () => {
  // ํ ํ Subtotal์ด๊ธฐ ๊ฐ 0 ํ์คํธ
  render(<Options optionType={"toppings"} />);
  // exact๊ฐ false์ด๋ฉด ๊ผญ ๋ชจ๋  ๊ธ์๊ฐ ์ ํํ ๋ง์ ํ์์๋ค. ๊ธฐ๋ณธ๊ฐ์ true
  const toppingsSubtotal = screen.getByText("toppings total: $", {
    exact: false,
  });

  expect(toppingsSubtotal).toHaveTextContent("0.00");

  // ํ ์ต์์ ๋ํ ๋ฐ์ค๋ฅผ ์ฐพ์ ์ฒดํฌํ๊ณ  ์๋ฐ์ดํธ๋ ๋ถ๋ถ ํฉ๊ณ์ ๋จ์ธ(2๊ฐ)
  const CherriesCheckbox = await screen.findByRole("checkbox", {
    name: "Cherries",
  });
  const GummiCheckbox = await screen.findByRole("checkbox", {
    name: "M&Ms",
  });

  userEvent.click(CherriesCheckbox); // 1.5๋ฌ๋ฌ ์ฆ๊ฐ
  await waitFor(() => expect(toppingsSubtotal).toHaveTextContent("1.50"));

  userEvent.click(GummiCheckbox); // 1.5๋ฌ๋ฌ ์ฆ๊ฐ
  await waitFor(() => expect(toppingsSubtotal).toHaveTextContent("3.00"));

  userEvent.click(CherriesCheckbox); // 1.5๋ฌ๋ฌ ๊ฐ์
  await waitFor(() => expect(toppingsSubtotal).toHaveTextContent("1.50"));
});
```

<br />

## ๐งโ๐ป Provider(5) - ์ด๊ณ(Grand total)

```js
describe("grand total", () => {
  test("grand total updates properly if scoop is added first", async () => {
    render(<OrderEntry />);

    const grandTotal = screen.getByRole("heading", {
      name: /grand total: \$/i,
    });
    const vanillaInput = await screen.findByRole("spinbutton", {
      name: "Vanilla",
    });
    const CherriesCheckbox = await screen.findByRole("checkbox", {
      name: "Cherries",
    });

    // scoop add
    userEvent.clear(vanillaInput);
    userEvent.type(vanillaInput, "2"); // 4๋ฌ๋ฌ ์ฆ๊ฐ
    await waitFor(() => expect(grandTotal).toHaveTextContent("4.00"));

    // topping add
    userEvent.click(CherriesCheckbox); // 1.5๋ฌ๋ฌ ์ฆ๊ฐ
    await waitFor(() => expect(grandTotal).toHaveTextContent("5.50"));
  });
  test("grand total updates properly if topping is added first", async () => {
    render(<OrderEntry />);

    const grandTotal = screen.getByRole("heading", {
      name: /grand total: \$/i,
    });
    const vanillaInput = await screen.findByRole("spinbutton", {
      name: "Vanilla",
    });
    const CherriesCheckbox = await screen.findByRole("checkbox", {
      name: "Cherries",
    });

    // topping add
    userEvent.click(CherriesCheckbox); // 1.5๋ฌ๋ฌ ์ฆ๊ฐ
    await waitFor(() => expect(grandTotal).toHaveTextContent("1.50"));

    // scoop add
    userEvent.clear(vanillaInput);
    userEvent.type(vanillaInput, "2"); // 4๋ฌ๋ฌ ์ฆ๊ฐ
    await waitFor(() => expect(grandTotal).toHaveTextContent("5.50"));
  });

  test("grand total updates properly if item is removed", async () => {
    render(<OrderEntry />);

    const grandTotal = screen.getByRole("heading", {
      name: /grand total: \$/i,
    });
    const vanillaInput = await screen.findByRole("spinbutton", {
      name: "Vanilla",
    });
    const CherriesCheckbox = await screen.findByRole("checkbox", {
      name: "Cherries",
    });

    // topping add
    userEvent.click(CherriesCheckbox); // 1.5๋ฌ๋ฌ ์ฆ๊ฐ

    // scoop add
    userEvent.clear(vanillaInput);
    userEvent.type(vanillaInput, "2"); // 4๋ฌ๋ฌ ์ฆ๊ฐ

    // scoop remove
    userEvent.clear(vanillaInput);
    userEvent.type(vanillaInput, "1"); // 2๋ฌ๋ฌ ๊ฐ์

    await waitFor(() => expect(grandTotal).toHaveTextContent("3.50"));

    // topping remove
    userEvent.click(CherriesCheckbox); // 1.5๋ฌ๋ฌ ๊ฐ์

    await waitFor(() => expect(grandTotal).toHaveTextContent("2.00"));
  });
});
```

<br />

## ๐งโ๐ป Provider(6) - act(...), Unmounted Component ์๋ฌ

```
When testing, code that causes React State updates should be wrapped into act(...)
```

```
Warning: Can't perform a React state update on unmounted component. ~~
```

- ํ์คํธ๋ฅผ ์งํํ๋ค๋ณด๋ฉด ์์ ๊ฐ์ ์๋ฌ๋ค์ด ๋ฐ์ํ๋ ๊ฒฝ์ฐ๊ฐ ์๋ค.

```js
test("grand total starts at $0.00", () => {
  render(<OrderEntry />);

  const grandTotal = screen.getByRole("heading", {
    name: /grand total: \$/i,
  });

  expect(grandTotal).toHaveTextContent("0.00");
});
```

- ์ค์ ๋ก ์ ์ฝ๋์์๋ ๋น๋๊ธฐ ์ฒ๋ฆฌ์ ์ ํ ๊ด๊ณ์๋ ํ์คํธ์ด๋ค. ํ์ง๋ง ์์ ๊ฐ์ ์๋ฌ๊ฐ ๋ฐ์ํ๋ ์ด์ ๋ ์ปดํฌ๋ํธ๊ฐ ํ์คํธ ์ข๋ฃ ํ์ ๋น๋๊ธฐ ์๋ฐ์ดํธ๋ฅผ ๊ณ์ ํ๋ค๋ ๋ป์ด๋ค.
- ํด๋น ์๋ฌ๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด์๋ ์ฌ๋ฌ ๋ฐฉ๋ฒ์ด ์์ง๋ง ๊ฐ์ฅ ์ ํธํ๋ ๋ฐฉ๋ฒ์ Axios๊ฐ ์ฑ๊ณตํ๋ฉด ์ํ๋ฅผ ์๋ฐ์ดํธํ  ๋ ๋ณ๊ฒฝ์ด ์ผ์ด๋๊ธฐ ๋๋ฌธ์, ๋น๋๊ธฐ ํ์คํธ๊ฐ ์งํ๋๋ ํ์คํธ์ ๋น๋๊ธฐ๊ฐ ๋ถ ํ์ํ ํ์คํธ ์ฝ๋๋ฅผ ํฌํจํ๋ ๋ฐฉ๋ฒ์ด๋ค.
  - ํ์คํธ ์ฝ๋๋ฅผ ํฌํจํ๋ฉด ๊ธฐ์กด์ ๋ถ ํ์ํ ํ์คํธ๋ ์ ๊ฑฐํ๋ค.

```js
test("grand total updates properly if scoop is added first", async () => {
  render(<OrderEntry />);

  const grandTotal = screen.getByRole("heading", {
    name: /grand total: \$/i,
  });
  const vanillaInput = await screen.findByRole("spinbutton", {
    name: "Vanilla",
  });
  const CherriesCheckbox = await screen.findByRole("checkbox", {
    name: "Cherries",
  });

  // (*)
  expect(grandTotal).toHaveTextContent("0.00");

  userEvent.clear(vanillaInput);
  userEvent.type(vanillaInput, "2");
  await waitFor(() => expect(grandTotal).toHaveTextContent("4.00"));

  // ...
});
```

- ๋ํ, await์ ํ์คํธ ๋์ ์ถ๊ฐํด ์ ์๋ฌ๋ฅผ ํผํ  ์ ์๋ค. ๊ฐ์ฅ ๋ฌธ์ ๊ฐ ์ ๊ณ  ํ์คํธ์์ ์๋ฌ๋ฅผ ํผํ๊ณ ์ ๋ฒ๊ฑฐ๋ก์ด ์์์ ์คํํ  ํ์๊ฐ ์์ด ์ ์ฉํ๊ธด ํ์ง๋ง ๊ฐ์ฌ๋ถ์ ์ ํธํ์ง๋ ์๋๋ค๊ณ  ํ๋ค. ์ฐจ๋ผ๋ฆฌ ์์์ฒ๋ผ ๋น๋๊ธฐ ์ฒ๋ฆฌํ๋ ํ์คํธ์๋ค ํ์คํธ ์ฝ๋๋ฅผ ํฌํจํ๋๊ฒ ์ข์ ๋ณด์ธ๋ค.

<br />

## ๐งโ๐ป Provider(7) - ๊ธฐ๋ฅ ํ์คํธ๋ ๋ฌด์์ ์ก์์ผ ํ๋?

- ๋ณดํต ๊ธฐ๋ฅ ํ์คํธ๋ ์ฝ๋ ์๋ ๋ฐฉ์์ ์ํํ๋ค. ์ฌ์ดํธ์ ์ ์  ํ์ด์ง๊ฐ ์๋๋ผ ์ฝ๋ ํ๋ก์ธ์ค๋ฅผ ๊ฒ์ฌํ๋ ๊ฒ์ด๋ค. ์ฆ, ํฅํ ์ฝ๋ฉ์ผ๋ก ๋ณ๊ฒฝ๋  ์ ์๋ ์์๋ฅผ ๊ธฐ๋ฅ ํ์คํธ๋ก ํ์ธํ๋ ๊ฒ์ด๋ค.
- ์ ์  ํ์ด์ง ๋ฐ์ํ ๋ฌธ์ ๋ Cypress ํน์ Selenium์ ์ฌ์ฉํ๋ ์ธ์ ํ์คํธ ์์ญ์ ์ํ๋ค.
