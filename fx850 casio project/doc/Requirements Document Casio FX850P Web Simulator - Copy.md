Requirements Document: Casio FX-850P Web Simulator

Version: 1.1
Date: 2023-10-27 (Updated 2023-10-28)

**1. Introduction**

*   1.1. Project Purpose: To create a web-based simulator for the Casio FX-850P Pocket Computer. The simulator aims to replicate the look, feel, and core functionality of the original hardware within a single HTML file using JavaScript.
*   1.2. Target Audience: Retro-computing enthusiasts, former users of the FX-850P, students learning programming concepts, and individuals interested in calculator history.
*   1.3. Goal: Provide an accessible and reasonably accurate simulation experience of the Casio FX-850P, focusing on its user interface, calculator functions, and BASIC programming capabilities.

**2. References**

*   2.1. Visual References: The simulator's visual design should be based on images of the Casio FX-850P/FX-870P (as provided in the prompt), prioritizing the layout and key labels relevant to the FX-850P model where differences exist. The final agreed-upon ASCII key map serves as the definitive layout reference.
*   2.2. Functional References: Functionality should be based on publicly available information regarding the Casio FX-850P (manuals, articles, forums) and the specific functions identified on the final agreed-upon key map. Key researched features to include:
    *   2-line x 32-character LCD display simulation.
    *   QWERTY keyboard plus dedicated numeric/function keypad layout (as per final ASCII map).
    *   Specific scientific calculator functions (as detailed in Scope).
    *   Casio BASIC programming language support (core subset).
    *   Base RAM simulation (~8KB).
    *   "Scientific Library 116" (Presence noted, implementation Out of Scope).
    *   Final ASCII Key Map (represents the target UI and key function set).

**3. Scope**

*   3.1. In Scope:
    *   **UI:** Visual representation of the FX-850P layout based on the final agreed-upon ASCII map, including casing, display area, QWERTY keyboard, and function/numeric keypad.
    *   **Display:** Simulation of the 2x32 character monochrome LCD, including cursor, character rendering, and status indicators (e.g., DEG/RAD/GRA, SHIFT/Function mode if applicable based on key logic).
    *   **Input:**
        *   Handling clicks on the virtual keys using a mouse/touch.
        *   Mapping relevant physical keyboard keys to virtual key presses.
        *   Handling required modifier logic (e.g., accessing secondary functions listed above keys).
        *   Handling input from P0-P9 keys (triggering an identifier or placeholder action).
    *   **Calculator Mode:**
        *   Basic arithmetic operations (+, -, *, /).
        *   Standard scientific functions identified on the map: `sin`, `cos`, `tan`, `sin⁻¹`, `cos⁻¹`, `tan⁻¹`, `log`, `ln`, `10x`, `ex`, `hyp`, `√`, `x²`, `FACT`.
        *   Number base / Data type functions: `HEX$`, `DMS$`, `&H`, `DEG(`.
        *   Numerical functions: `INT`, `FRAC`, `RAN#`.
        *   Coordinate conversion functions: `POL(`, `REC(`.
        *   Constants: `π`.
        *   Order of operations (precedence) and parenthesis `( )` handling.
        *   Angle modes (DEG, RAD, GRA) selection and calculation.
        *   `ANS` (Last Answer) functionality.
        *   Basic single calculator memory (`M`): Store (e.g., via `SHIFT`+`MR`/`M+`), Recall (`MR`), Add (`M+`), Subtract (`M-`). (Requires defining key combos if dedicated MR/M+/M- aren't present, or using existing keys with SHIFT). *Self-correction: Base map doesn't show dedicated M keys, implementation needs defining.* Let's assume basic `M` variable accessible via BASIC/CALC modes.
        *   Other Keys: `ENG` (Eng Notation display toggle), `E` (Exponent entry), `<-` (Backspace/Delete).
    *   **BASIC Programming Mode:**
        *   Implementation of a Casio BASIC interpreter supporting a core subset: `PRINT`, `INPUT`, `LET` (often implicit), `GOTO`, `IF...THEN`, `FOR...TO...STEP...NEXT`, `GOSUB...RETURN`, `END`, `LIST`, `RUN`, `NEW`, `CLS` (or equivalent screen clear, possibly mapped to `L.CAN` or similar), `DIM`.
        *   Support for line numbers.
        *   Support for numeric and string variables (including a basic 'M' variable).
        *   Basic array support (`DIM`).
        *   Program entry and line editing (using `INS`, `DEL`, arrow keys `←`, `→`, `↑`, `↓`, `HOME`, `L.TOP`, `L.END`).
        *   Execution control: `RUN`, `STOP` (via `SHIFT`+`ANS`), `BRK`.
        *   Basic error handling and reporting.
    *   **Mode Switching:** Functional mechanism to switch between Calculator (`CALC` key) and BASIC modes (via `MODE` key or BASIC prompt).
    *   **State Management:** Maintain the calculator's state (current mode, display content, variable values including `M`, stored program) within the browser session.

*   3.2. Out of Scope (Initial Version):
    *   Hardware Interfaces (ports for printers, cassette recorders).
    *   RAM Expansion simulation beyond base model.
    *   Full implementation of the "Scientific Library 116".
    *   Complex functionality of `LIB`, `MENU`, `IN`, `OUT` keys (these keys will be visually present but likely non-functional or have placeholder actions in v1).
    *   Full storage and programmability functionality of P-keys (P0-P9). They will act as input triggers only.
    *   Sound simulation (beeper).
    *   Persistence (saving/loading state/programs between browser sessions).
    *   Cycle-Accurate Emulation.
    *   Physical Switches simulation (Power slider, Hardware Reset button).
    *   Advanced/Obscure BASIC commands not listed in 3.1.
    *   Full implementation of `SET` key functionality (likely complex configuration).
    *   Complex Character Sets beyond standard ASCII/calculator symbols.

**4. Functional Requirements**

*   FR1: UI Rendering: Display a static visual representation of the Casio FX-850P based on the final ASCII map.
*   FR2: Display Simulation:
    *   FR2.1: Provide a virtual 2-line, 32-character display area.
    *   FR2.2: Display text and results mimicking a character-based LCD.
    *   FR2.3: Display and update a cursor correctly for input and editing.
    *   FR2.4: Display status indicators (DEG, RAD, GRA, etc.) based on current mode/settings.
*   FR3: Input Handling:
    *   FR3.1: Handle clicks on virtual keys.
    *   FR3.2: Handle mapped physical keyboard keys.
    *   FR3.3: Provide visual feedback on key activation.
    *   FR3.4: Correctly interpret key presses based on modifier states (e.g., for secondary functions).
*   FR4: Mode Management:
    *   FR4.1: Support distinct Calculator and BASIC modes.
    *   FR4.2: Allow users to switch between modes using simulated `CALC`, `MODE` keys or context.
    *   FR4.3: Clearly indicate the current mode.
*   FR5: Calculator Functionality:
    *   FR5.1: Implement all calculator functions listed as In Scope in Section 3.1.
    *   FR5.2: Correctly evaluate mathematical expressions respecting operator precedence and parentheses.
    *   FR5.3: Implement `ANS` functionality.
    *   FR5.4: Support DEG, RAD, GRA modes and display.
    *   FR5.5: Allow access/manipulation of a basic numeric memory variable 'M'.
*   FR6: BASIC Interpreter Functionality:
    *   FR6.1: Accept BASIC lines with line numbers.
    *   FR6.2: Store program lines.
    *   FR6.3: Implement `LIST` command.
    *   FR6.4: Implement `RUN` command.
    *   FR6.5: Implement `NEW` command.
    *   FR6.6: Execute core BASIC commands listed in Scope (3.1).
    *   FR6.7: Manage numeric and string variables (including 'M').
    *   FR6.8: Implement basic line editing using `INS`, `DEL`, `<-`, `→`, `↑`, `↓` and related secondary functions (`HOME`, `L.TOP`, `L.END`).
    *   FR6.9: Display appropriate error messages.
    *   FR6.10: Implement program interruption via `BRK` key.
*   FR7: Key Mapping: Define and implement logical mapping for virtual and physical keys according to the final ASCII map, including primary, secondary, and P0-P9 functions.

**5. Non-Functional Requirements**

*   NFR1: Look and Feel: UI layout, key appearance, and overall visual aesthetic should closely resemble the reference images and final ASCII map. Use appropriate fonts (monospace for display) and color scheme.
*   NFR2: Performance: Simulator must be responsive; calculations and BASIC execution reasonably fast.
*   NFR3: Platform: Run correctly in latest major desktop browsers (Chrome, Firefox, Edge, Safari).
*   NFR4: Implementation: Single HTML file with HTML, CSS, and vanilla JavaScript (ES6+). No external JS libraries/frameworks. No server-side code.
*   NFR5: Usability: Interface should be intuitive. Input methods reliable.

**6. Technical Requirements**

*   TR1: Languages: HTML5, CSS3, JavaScript (ES6+).
*   TR2: Structure: Single `.html` file (CSS in `<style>`, JS in `<script>`).
*   TR3: Dependencies: None.

**7. Future Considerations (Optional Enhancements)**

*   Persistence (`localStorage`).
*   Sound output.
*   Expanded BASIC command set.
*   "Scientific Library 116" simulation attempt.
*   Implement P-key storage/programmability.
*   Implement `LIB`, `MENU`, `IN`, `OUT`, `SET` key functionalities.
*   Improved visual fidelity.
*   Mobile responsiveness.