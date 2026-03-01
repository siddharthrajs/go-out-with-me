# AGENTS.md

This file provides guidance to agents when working with code in this repository.

- Static site only: no build/lint/test pipeline. Do not assume npm/yarn scripts exist; edits should work by opening [index.html](index.html) directly or via a simple static server.
- Button visuals depend on DOM order via CSS nth-child rules. Changing button count/order without updating selectors will flip styles. See [button:nth-child rules](style.css:51) and [index.html](index.html:23).
- Evasion logic assumes buttons are positioned against the viewport. Do not add position: relative to containers without updating [handleNoMouseOver()](script.js:150), which computes random left/top against window.innerWidth/innerHeight.
- On "Yes", code removes the No button first, then replaces the Yes button. If you change this order, CSS nth-child side-effects change. Flow lives in [handleYesClick()](script.js:6).
- The replacement "Let's Go!" button uses inline positioning with a width breakpoint at 800px and transform translate(-50%, -50%) without an explicit top. Layout tweaks in CSS can shift it unexpectedly; adjust logic near [letsGoBtn.style.left](script.js:129) and [script.js](script.js:135).
- JS relies on class names .yes-btn and .no-btn for initial wiring via a tuple selector map: [const [yesBtn, noBtn] = [".yes-btn", ".no-btn"].map(qs)](script.js:4). Renaming classes requires code updates.
- The quick selector helper [qs](script.js:1) returns a single element; code assumes exactly one match for each selector.
- External network dependencies: Google Fonts and Giphy GIFs. Offline or blocked third-party requests will degrade visuals; vendor locally if needed. See [index.html](index.html:8) and [gif.src updates](script.js:8).
- If you add elements inside .btn-group, revisit nth-child-based styling and absolute positioning in [style.css](style.css:38) and margins in [style.css](style.css:51).
- No tests configured. If introducing tests for DOM behavior, ensure the environment provides window.innerWidth/innerHeight and getBoundingClientRect semantics used in [handleNoMouseOver()](script.js:150).

