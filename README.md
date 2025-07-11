#  Gamba.so – Client-side RNG Vulnerability (`Math.random()`)

This repository documents a **critical architectural vulnerability** in the Gamba demo game at [demo.gamba.so](https://demo.gamba.so), where **client-side RNG** is used to determine game outcomes.

---

##  Summary

- **Issue:** Slot outcomes and game logic rely on `Math.random()` in the browser
- **Impact:** A player can fully control and predict outcomes via DevTools
- **Severity:**  Critical
- **Affected game:** Slots (demo)
- **Type:** Insecure Randomness / Client-side Logic

---

##  Files

| File                         | Description                             |
|------------------------------|-----------------------------------------|
| `finding-03.md`              | Full write-up of the vulnerability      |
| `PoC/instructions.md`        | Exploitation steps (DevTools, override) |
| `screenshots/`               | Visual evidence of vulnerability        |
| `hackerone-response.md`      | (Optional) Response from disclosure      |

---

##  Key Vulnerability

Gamba's slot game uses the following logic on the client side:

```js
const at = React.useRef(Array.from({ length: 25 }).map(() => ({
  x: Math.random(),
  y: -Math.random() * 600
})));

setClientSeed(String(Math.random() * 1e9 | 0));

const mt = Math.random() * betBuffer.bet.length | 0;
pt = betBuffer.bet[mt];
