# 12. Check Yourself — Answers

1. A Text inside a Row overflows. Which part of "constraints go down, sizes go up, parent sets position" was violated, and by which widget?
**Answer:** The "constraints go down" rule was violated by the `Row` widget. `Row` passed unbounded horizontal constraints ($\infty$) to the `Text` child, allowing the `Text` to calculate a size wider than the screen boundary instead of restricting it to the remaining available space.

---

 2. Why is adding `width: 150` to the text the wrong fix, even if the stripes disappear?
**Answer:** Adding a hard-coded width (`width: 150`) is a brittle workaround that moves the bug rather than fixing the constraint relationship. It fails to adapt when device screen widths, orientation, user accessibility font scales, or text lengths change.

---

 3. You fixed the landscape overflow by wrapping everything in a `SingleChildScrollView` and setting `shrinkWrap: true` on the list. Which test fails, and why does it matter once the data comes from an API?
**Answer:** Test 7 (500 items built lazily) fails because `shrinkWrap: true` forces Flutter to evaluate and build all list items eagerly up front instead of lazily on-demand. When data comes from an API with hundreds or thousands of items, building everything up front causes severe memory bloat, UI freezing, and app crashes.

---

4. Why does the tablet layout use `LayoutBuilder` rather than `MediaQuery.sizeOf(context)`?
**Answer:** `LayoutBuilder` provides the local incoming constraints of the parent container, allowing components to adapt correctly when embedded in multi-pane layouts or split screens. `MediaQuery.sizeOf(context)` only measures the global device window size, which ignores local layout bounds.

---

 5. The empty-data crash was not a layout error. Why does it belong in a layout lab anyway?
**Answer:** Handling zero data is an essential part of UI/UX layout responsiveness. A resilient screen must handle all edge-case data states cleanly—rendering an informative empty state widget rather than crashing or displaying broken, empty frames.
