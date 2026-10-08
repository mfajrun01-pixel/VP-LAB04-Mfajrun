# Lab 04 — Fix Log

| Widget | Error / symptom | Rule broken | Fix |
| :--- | :--- | :--- | :--- |
| `StoreHeader` | Overflowed on the right at 320 dp | The `Row` gave `Column` unbounded width and rating text had no overflow strategy | `Expanded` on store details `Column` + `Flexible` on rating `Row` + `maxLines: 1` + `ellipsis` |
| `CategoryBar` | Overflowed on the right at 320 dp | The `Row` of filter chips exceeded available screen width without scrolling | Wrapped `Row` in horizontal `SingleChildScrollView` |
| `PromoStrip` | Overflowed on the right at 320 dp / 430 dp & `RangeError` on empty data | Fixed 200 dp cards in `Row` exceeded screen width; assumed `promos` always contained ≥2 items | Wrapped `Row` in horizontal `SingleChildScrollView` & added `if (promos.length >= 2)` check |
| `PromoCard` | Item name text clipped / overflowed on long names | `Text` inside card column lacked bounded vertical space and overflow strategy | `Expanded` + `maxLines: 3` + `ellipsis` |
| `MenuTile` | Overflowed on the right with 200-character item name | The `Row` gave `Text` unbounded width without an overflow strategy | Wrapped title `Column` in `Expanded` + `maxLines: 1` + `ellipsis` |
| `MenuCard` | Overflowed by 45 pixels on bottom in tablet grid | Fixed container height (110) caused column children inside `Card` to exceed cell height | `Expanded` on image container + `maxLines: 1` + `ellipsis` |
| `CartBar` | Overflowed on the right at 320 dp | The `Row` gave cart summary `Text` unbounded width | Wrapped summary `Text` in `Expanded` + `maxLines: 1` + `ellipsis` |
| `CartBar` (Gesture bar) | Order button sat under the gesture bar | Bottom navigation bar did not respect system bottom safe area insets | Wrapped `CartBar` interior in `SafeArea(top: false, ...)` |
| `MenuScreen` (Empty state) | Blank screen showed when filter returned zero items | UI assumed list was non-empty and lacked required empty state widget | Checked `visible.isEmpty` and rendered empty state widget with `key: const Key('empty-state')` |
| `MenuScreen` (500 items) | Built all 500 items eagerly up front | Long list was built eagerly using `ListView(children: ...)` | Replaced with lazy `SliverList.builder` / `SliverGrid.builder` |
| `MenuScreen` (Tablet & Landscape) | Screen layout failed structure change test at 800 dp & overflowed when keyboard opened | Failed to change structure at 600 dp breakpoint & fixed column lacked scrollability | Used `CustomScrollView` with `LayoutBuilder` (600 dp threshold) dynamically rendering `SliverGrid.builder` or `SliverList.builder` |
