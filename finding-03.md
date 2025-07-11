#  Finding #3 — Client-side RNG via Math.random()

**Severity:**  High  
**Category:** Insecure Randomness / Client-Side Logic Flaw  
**Target:** https://demo.gamba.so/slots  
**File(s):** index-debc2fca.js, index-6e531b03.js  

##  Description

Gamba.so's slot game demo uses Math.random() directly in the frontend to calculate spin outcomes, clientSeed values, and multiplier logic. This makes the game results fully predictable and manipulatable from the browser.

---

##  Code Evidence

```js
const at = React.useRef(Array.from({ length: 25 }).map(() => ({
  x: Math.random(),
  y: -Math.random() * 600
})));

setClientSeed(String(Math.random() * 1e9 | 0));

const mt = Math.random() * betBuffer.bet.length | 0;
pt = betBuffer.bet[mt];
```

---

##  PoC

1. Open DevTools on https://demo.gamba.so/slots
2. Click `Spin`, pause execution with debugger
3. Override randomness:

```js
Math.random = () => 0.999;
```

4. Resume — result will be based on fake input.

---

##  Impact

- Game outcomes are fully predictable
- Users can create fake winning animations
- No backend or cryptographic randomness
- Violates basic Web3 fairness expectations

---

##  Recommendation

- Replace Math.random() with server-signed or on-chain randomness
- Use Chainlink VRF or commit-reveal patterns
- Separate visual rendering from outcome logic

---

##  See screenshots/

Refer to the `/screenshots` folder for visual proof of code behavior and DevTools manipulation.

