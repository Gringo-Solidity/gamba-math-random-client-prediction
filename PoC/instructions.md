#  PoC: Exploiting Gamba's Math.random() Vulnerability

This guide demonstrates how to reproduce and exploit the slot outcome predictability caused by client-side RNG.

---

##  Steps to Reproduce

1. **Open the Gamba Slots Demo:**
   https://demo.gamba.so/slots

2. **Open DevTools:**
   - Press F12
   - Go to the **Sources** tab

3. **Pause Execution:**
   - Enable “Event Listener Breakpoints” > Mouse > click
   - Press the `Spin` button to trigger the breakpoint

4. **Override Math.random():**
   In the Console tab, type:

```js
Math.random = () => 0.99;
```

5. **Resume Execution:**
   - Press F8 to continue script
   - The result of the spin is now manipulated

---

##  Optional: Override clientSeed generation

```js
Object.defineProperty(Math, 'random', {
  value: () => 0.999,
  writable: false
});
```

---

##  Outcome

- Results are based on fake RNG
- No backend validation or signature
- Visuals reflect manipulated data
