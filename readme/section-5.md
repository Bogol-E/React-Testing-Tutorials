# π» Section 5 - Mock Service Worker(MSW)

## π§βπ» MSW(1) - Mock Service Workerμ νΈλ€λ¬ μκ°

- [Mork Service Worker](https://mswjs.io/)
- MSWμ λͺ©μ μ λ€νΈμν¬ νΈμΆμ κ°λ‘μ±μ μ§μ λ μλ΅μ λ°νν΄μΌ νλ€. μ΄λ μ’λ¨ κ° νμ€νΈλ νμ§ μλλ€λ κ±Έ κΈ°μ΅νμ.
- νμ€νΈνλ λμ λ°μνλ λͺ¨λ  λ€νΈμν¬ νΈμΆμ λ§λλ€.
- μλ² μλ΅μ κΈ°λ°ν νμ€νΈ μ‘°κ±΄λ μ€μ νλ€. μ΄λ κ² λ  κ²½μ° νμ€νΈ μ‘°κ±΄μ μλ²κ° μ΅μμΌλ‘ λ¬΄μμ λ°ννλλμ λ¬λ €μλ€.

### MSW Setup

- MSWλ₯Ό μννκΈ°μν΄ μ°μ  ν¨ν€μ§λ₯Ό μ€μΉνλ€

```
npm i msw
λλ
yarn add msw
```

- μ€μΉ νμλ νΈλ€λ¬λ₯Ό μμ±ν΄μΌνλ€. νΈλ€λ¬λ, νΉμ ν URLκ³Ό λΌμ°νΈμ λ¬΄μμ λ°νν μ§ κ²°μ νλ ν¨μλ€.
- κ·Έ νμ μμ²­μ μ²λ¦¬ν  μλ²λ μμ±νλ€.
- νμ€νΈνλ λμ νμ€νΈ μλ²κ° ν­μ μμ  λκΈ° μ€μΈμ§ μΈν°λ·μΌλ‘ λκ°λ νΈμΆμ κ°λ‘μ±κ³  μλμ§λ νμΈν΄μΌ νλ€. μ΄λ μ€μ  νμ€νΈ νμΌμμ νμΈν  μ μλ€.
  - κ°μ νμΌμμ κ° νμ€νΈ νμ μλ² νΈλ€λ¬λ₯Ό μ¬μ€μ νλ€. νμ€νΈνλ€κ° νΈλ€λ¬μ λ¬Έμ κ° μκΈ°λ©΄ λμ νμ€νΈλ₯Ό μν΄ μ¬μ€μ μ ν΄μΌλλ€.

### Handler

- [MSW - Mocking REST API](https://mswjs.io/docs/getting-started/mocks/rest-api)
- μμ κ°μ΄λ λΌμΈλλ‘ REST APIμ νμν νμ μμλ₯Ό κ°μ Έμλ³΄μ.

```js
// src/mocks/handlers.js
import { rest } from "msw";

// Example
export const handlers = [
  // Handles a POST /login request
  rest.post("/login", null),
  // Handles a GET /user request
  rest.get("/user", null),
];
```

- μ¬κΈ°μ μ°μ  rest.get, rest.postκ° μ΄λ€ λμμΌλ‘ μμ§μ΄λμ§ νμΈν΄λ³΄μ.

```js
rest.get("http://localhost:3030/scoops", (req, res, ctx) => {});
```

- expressλ₯Ό ν΄λ΄€λ€λ©΄ μμ ν¬λ§·μ΄ μ΅μν  κ²μ΄λ€. expressμ νΈλ€λ¬λ λΉμ·ν μμ²­κ³Ό μλ΅ λ° μ»¨νμ€νΈ κΈ°λ₯μ μ¬μ©νλ€.
- μ μ½λλ₯Ό νλνλ λΆμν΄λ³΄μ
  - Handler Type: `rest` or `graphql`
    - κ°μ₯ μμ restλΆλΆμΈλ° λ§ κ·Έλλ‘ νΈλ€λ¬ νμμ΄λ€.
    - RESTμ΄λ  GraphQLμ΄λ  MSWμμ κ°μ Έμ¨λ€.
  - method: HTTP Method(`get`, `post`, `delete`, `put`, `patch` λ±)
    - get λΆλΆμ νΉμ  URLμ mockingνλ €λ HTTP λ©μλκ° μ¨λ€.
    - μ²« λ²μ§Έ μΈμλ‘ mockingν  `μ μ²΄ URL`μ μλ ₯νλ€.
    - λ λ²μ§Έ μΈμλ‘ ν¨μλ₯Ό μ¨λ€. μ΄ ν¨μλ μμ²­, μλ΅ κ°μ²΄μ μλ΅μ κ΅¬μΆνλ μ νΈλ¦¬ν°μΈ μ»¨νμ€νΈλ‘ μ΄λ€μ§λ€.
    - [MSW - Pesponse resolver](https://mswjs.io/docs/basics/response-resolver) μμΈνκ±΄ λ€μ μ¬μ΄νΈλ₯Ό μ°Έκ³ νλ€.
- μλ²κ° μ€μ λ‘ νλ μμκ³Ό μμ²­ λ΄μ©μλ°λΌ μ΄λ¬ν MSW νΈλ€λ¬λ₯Ό ν΅ν΄ λ§μ μ κ΅ν μμμ μ§νν  μ μλ€.

<br />

- μ κ΅ν μμμ μν΄ Serverμͺ½ μ½λμ μ΄λ€ λ°μ΄ν° ν¬λ§·μ κ°λμ§ νμΈν΄λ³΄μ.

```js
// sundaes-on-demand-server/server.js

// read data from options file
const sundaeOptionsRaw = fs.readFileSync("./sundae-options.json", "utf-8");
const sundaeOptions = JSON.parse(sundaeOptionsRaw);

app.get("/scoops", (req, res) => {
  // return data from file
  res.json(sundaeOptions.iceCreamFlavors);
});
```

```json
// sundaes-on-demand-server/sundae-options.json/iceCreamFlavors
{
  "iceCreamFlavors": [
    {
      "name": "Mint chip",
      "imagePath": "/images/mint-chip.png"
    },
    {
      "name": "Vanilla",
      "imagePath": "/images/vanilla.png"
    },
    {
      "name": "Chocolate",
      "imagePath": "/images/chocolate.png"
    },
    {
      "name": "Salted caramel",
      "imagePath": "/images/salted-caramel.png"
    }
  ],
  "toppings": [
    {
      "name": "M&Ms",
      "imagePath": "/images/m-and-ms.png"
    },
    {
      "name": "Hot fudge",
      "imagePath": "/images/hot-fudge.png"
    },
    {
      "name": "Peanut butter cups",
      "imagePath": "/images/peanut-butter-cups.png"
    },
    {
      "name": "Gummi bears",
      "imagePath": "/images/gummi-bears.png"
    },
    {
      "name": "Mochi",
      "imagePath": "/images/mochi.png"
    },
    {
      "name": "Cherries",
      "imagePath": "/images/cherries.png"
    }
  ]
}
```

- μμμ²λΌ μλ²μμ λκ²¨μ£Όλ λ°μ΄ν°λ₯Ό νμΈνμΌλ©΄ MSWλ‘ μ΄λ»κ² Mocking ν΄μΌνλμ§ μ μ μμ κ²μ΄λ€.
- κ·Έλ λ€λ©΄ μ€μ λ‘ MSW Handlerλ₯Ό μμ±ν΄λ³΄μ.

```js
export const handlers = [
  rest.get("http://localhost:3030/scoops", (req, res, ctx) => {
    return res(
      ctx.json([
        { name: "Chocolate", imagePath: "/images/chocolate.png" },
        { name: "Vanilla", imagePath: "/images/vanilla.png" },
      ])
    );
  }),
];
```

- μμμ²λΌ Handlerλ₯Ό μμ±νμΌλ©΄ μ΄μ  MSW μλ²λ₯Ό μ€μ ν΄λ³΄μ.

<br />

### MSW Server μ€μ 

- [MSW - Integrate(Node)](https://mswjs.io/docs/getting-started/integrate/node)
- MSWμ Integrateμλν΄μ μμλ³Όκ±΄λ° Intergrateλ λΈλΌμ°μ μ λΈλ νκ²½ κ°μ λμΌν μμ²­ μ²λ¦¬κΈ°λ₯Ό κ³΅μ νλ κ²μ λ§νλ€. μ°Έκ³ λ‘ μ¬κΈ°μλ λΈλΌμ°μ λ μ¬μ©νμ§ μκ³  Nodeλ₯Ό μ¬μ©νλ€.
- λΈλλ Jestλ₯Ό μ€ννλ©΄ μ€νλλ€.
- μ°μ  `src/mocks`μ `server.js`νμΌμ μμ±νλ€. κ·Έλ¦¬κ³  μλμ κ°μ΄ μ½λλ₯Ό μμ±νλ€.

```js
// src/mocks/server.js
import { setupServer } from "msw/node";
import { handlers } from "./handlers";
// This configures a request mocking server with the given request handlers.
export const server = setupServer(...handlers);
```

- `setupServer(...handlers)`λ setupServerκ° handlersμ ν¨κ» μ€νλ¨μ μλ―Ένλ€. λ°°μ΄μ μ κ° μ°μ°μλ‘ νΌμ³μ λ°°μ΄μ κ° μμλ₯Ό λ³κ°μ μΈμλ‘ λ§λ λ€.
- λ§μ§λ§μΌλ‘ MSWκ° λ€νΈμν¬ μμ²­μ κ°λ‘μ± νΈλ€λ¬μκ² μ€μ ν μλ΅μ λ°ννλλ‘ create-react-app(CRA) μ κ΅¬μ±ν΄μΌ νλ€.
- CRAλ₯Όνλ©΄ μμ±λλ `src/setupTests.js`λ₯Ό μλμ κ°μ΄ μμ νλ€.

```js
// src/setupTests.js
// jest-domλλ¬Έμ jest-dom λ¨μΈμ μ¬μ©ν  μ μλ€.
import "@testing-library/jest-dom";
import server from "./mocks/server.js";

// νμ€νΈλ₯Ό νκΈ° μ μ ν­μ μλ²κ° μμ μ λκΈ°νλλ‘ νλ€.
// λ€μ΄μ€λ λͺ¨λ  λ€νΈμν¬ μμ²­μ μ€μ  λ€νΈμν¬κ° μλ MSWλ‘ λΌμ°νν¨μ μλ―Ένλ€.
beforeAll(() => server.listen());

// κ° νμ€νΈκ° λνλ©΄ νΈλ€λ¬λ₯Ό μλ²λ₯Ό μ μνμ λμ νΈλ€λ¬λ‘ μ¬μ€μ νλ€.
// κ²°κ΅­ νΉμ  νμ€νΈμ λν νΉμ  νΈλ€λ¬κ° μκΈ΄λ€κ³  ν  μ μλ€.
// λ€μ λ§ν΄, μλ²κ° μ€λ₯λ₯Ό λ°ννλ©΄ μ±μμ λ¬΄μ¨ μΌμ΄ μκΈ°λμ§ νμ€νΈνκΈ° μν΄μ μ΄λ€ νμ€νΈμμ μλ²κ° μ€λ₯λ₯Ό λ°ννκ² ν  μμ μ΄λ€.
afterEach(() => server.resetHandlers());

// νμ€νΈκ° λλλ©΄ μλ²λ₯Ό λ«μ μ λΆ κΉλνκ² μ§μ΄λ€.
afterAll(() => server.close());
```

<br />

## π§βπ» MSW(2) - MSWλ‘ μ€μΏ± μ΅μ νμ€νΈνκΈ°

- μ€μΏ± μ΅μμ νμ€νΈνκΈ° μ μ κ°μ₯ λ¨Όμ  entry ν΄λ μμ± νμ Options.js, OptionItem.js μ»΄ν¬λνΈλ₯Ό μμ±νλ€.

```js
// entry/Options
import React from "react";

const Options = ({ optionType }) => {
  return <div></div>;
};

export default Options;
```

```js
// entry/OptionItem
import React from "react";

const OptionItem = () => {
  return <div></div>;
};

export default OptionItem;
```

- κ·Έλ¦¬κ³  entry/tests ν΄λμλ€ Option.test.jsλ₯Ό μμ±νλ€.
- μ°Έκ³ λ‘ Option νμ€νΈλ κ°λ¨νλ€. μλ²μμ λ°νν  κ° μ΅μμ μ΄λ―Έμ§λ₯Ό λμ°λ κ²μ νμ€νΈ ν  κ²μ΄κΈ° λλ¬Έμ΄λ€. μ νν λ§νλ©΄ μλ²λ μλκ³  `MSW`μ΄λ€.

```js
// entry/tests/Option.test.js
import { render, screen } from "@testing-library/react";
import Options from "../Options";

test("display image for each scoop option from server", () => {
  render(<Options optionType="scoops" />);

  // find images
  // λͺ¨λ  μ΄λ―Έμ§ μμλ₯Ό μ­ν λ‘μ κ°μ ΈμμΌνκΈ° λλ¬Έμ getAllByRole μ¬μ©
  // λͺ¨λ  alt νμ€νΈκ° scoopμ΄λΌλ λ¬Έμμ΄λ‘ λλμΌ νλ€.
  const scoopImages = screen.getAllByRole("img", {
    name: /scoop$/i,
  });
  expect(scoopImages).toHaveLength(2);

  // confirm alt text of images
  // mapμ μ΄μ©ν΄ λͺ¨λ  μ΄λ―Έμ§μ λν alt νμ€νΈλ₯Ό μ»μ μ μλ€.
  const altText = scoopImages.map((el) => el.alt);

  // κ°μ²΄λ λ°°μ΄μ μ¬μ©ν  λλ toBe λ§κ³  toEqual μ¬μ©ν΄μΌ νλ€.
  expect(altText).toEqual(["Chocolate scoop", "Vanilla scoop"]);
});
```

- μμ μ²λΌ Option μ»΄ν¬λνΈμ λν μ½λλ₯Ό μμ±νλ€. λͺ κ°μ§ μ΄ν΄λ³Ό λ΄μ©μ μ£ΌμμΌλ‘ λ¨κ²Όλ€.
- νμ§λ§ μμ κ°μ΄ μ½λλ₯Ό μμ±ν΄λ νμ€νΈλ₯Ό μ§ννλ©΄ μλ¬κ° λ°μνλ€. ν΄λΉ μλ¬λ₯Ό ν΄κ²°νκΈ° μν΄μλ λΉλκΈ°μμΌλ‘ νμ΄μ§μ λνλ  λΉλκΈ° μμμ ν  λ `await`κ³Ό `findBy`λ₯Ό μ¬μ©ν΄μΌ νλ€.
- κ·ΈμΈμλ λΉλκΈ° μμμ νμ€νΈ ν  λλ `waitFor`λΌλ λ©μλλ μ¬μ©ν  μ μλ€.

```js
import { render, screen, waitFor } from "@testing-library/react";
import Options from "../Options";

test("display image for each scoop option from server", async () => {
  render(<Options optionType="scoops" />);

  // find images
  // λͺ¨λ  alt νμ€νΈκ° scoopμ΄λΌλ λ¬Έμμ΄λ‘ λλμΌ νλ€.
  const scoopImages = await screen.findAllByRole("img", {
    name: /scoop$/i,
  });
  expect(scoopImages).toHaveLength(2);

  // confirm alt text of images
  // mapμ μ΄μ©ν΄ λͺ¨λ  μ΄λ―Έμ§μ λν alt νμ€νΈλ₯Ό μ»μ μ μλ€.
  const scoopImageAltText = scoopImages.map((el) => el.alt);

  // κ°μ²΄λ λ°°μ΄μ μ¬μ©ν  λλ toBe λ§κ³  toEqual μ¬μ©
  expect(scoopImageAltText).toEqual(["Chocolate scoop", "Vanilla scoop"]);
});
```

- λ¦¬μ‘νΈ μ½λλ sundaes-on-demand-client νλ‘μ νΈμ `pages/entry/Options`, `OptionItem`μ μ°Έκ³ νμ

<br />

<br />

## π§βπ» MSW(3) - MSW Error νμ€νΈ

- μλ²μμ `μλ¬` μλ΅μ΄ λ°μν  κ²½μ° μ νλ¦¬μΌμ΄μμ΄ μ μ ν λμν΄μΌ νλ€.
- μλ² μλ¬λ₯Ό λ°μμν€λ νμ€νΈλ₯Ό μν΄μλ κΈ°μ‘΄μ serverμ handlerλ€μ νμ€νΈ νμΌμμ `override(μ€λ²λΌμ΄λ)`νλ©΄ λλ€.
- κ·Έλ¦¬κ³  μλ μμ μμλ axios catchλ₯Ό μ΄μ©ν λΉλκΈ° νμ€νΈμ΄κΈ° λλ¬Έμ `find`μ `waitFor`λ₯Ό μ΄μ©ν΄μ νμ€νΈλ₯Ό μ§ννλ€.

```js
// OrderEntry.test.js
import { render, screen, waitFor } from "@testing-library/react";
import OrderEntry from "../OrderEntry";
import { rest } from "msw";
import server from "../../../mocks/server";

test("handles error for scoops toppings router", async () => {
  // κΈ°μ‘΄μ μ€μ ν server handlerλ₯Ό μ€λ²λΌμ΄λ© νλ μ½λ (μλ¬ λ°μμν€κΈ° μν¨)
  server.resetHandlers(
    rest.get("http://localhost:3030/scoops", (req, res, ctx) => {
      // λ°νμ μν΄μ£Όλ©΄ νμ€νΈλ ν΅κ³Όνμ§λ§ warn κ²½κ³ κ° λμ΄! λ°νμ ν΄μ£Όμ
      return res(ctx.status(500));
    }),
    rest.get("http://localhost:3030/toppings", (req, res, ctx) => {
      return res(ctx.status(500));
    })
  );

  render(<OrderEntry />);

  // waitForλ‘ λΉλκΈ° μ²λ¦¬ν΄μ£Όμ§ μμΌλ©΄ λ¨μΈμ΄ λκΈ°μ μΌλ‘ μλν΄μ μ€λ₯κ° λ°μ ν¨
  // findλ‘λ νκ³κ° μμ Alertμ΄ 2κ°κ° λμμΌλλ μν©μΈλ°, 1κ°λ§ κΈ°λ€λ¦¬λκ²μλ 2κ° λͺ¨λ κΈ°λ€λ €μΌ λ¨
  await waitFor(async () => {
    // axios catchλ₯Ό μ΄μ©νλ―λ‘(λΉλκΈ°) findλ₯Ό μ΄μ©
    const alerts = await screen.findAllByRole("alert");
    // scoops, topping 2κ°μ alertμ΄ λμμΌ ν¨
    expect(alerts).toHaveLength(2);
  });
});
```

<br />

### test.only/skip

- test.onlyμ test.skipμ μ΄μ©ν΄μ νμΌ λ΄ νΉμ  νμ€νΈλ₯Ό κ²©λ¦¬ν  μ μλ€.

```js
test.only("only test", () => {
  // code
});

test.skip("skip test", () => {
  // code
});
```

<br />
