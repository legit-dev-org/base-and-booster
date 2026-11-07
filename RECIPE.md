# 📖 Recipe JSON Schema & Filtering Architecture Specification

This document details the schema definition for the `recipes.json` data file and explains how multi-category array properties are evaluated within the `index.html` filtering engine.

---

## 🏗️ Recipe Object Properties

Each recipe object in `recipes.json` adheres to the following structural schema:

| Property | Type | Description |
| :--- | :--- | :--- |
| `id` | `String` | Unique alphanumeric identifier (e.g., `"rec-001"`). |
| `title` | `String` | Display title of the recipe. |
| `bases` | `Array of Numbers` | Required freezer structural bases (`1`, `2`, `3`, or `4`). |
| `flavors` | `Array of Strings` | Required cultural flavor boosters (`"A"`, `"B"`, `"C"`, `"D"`). |
| `time` | `Array of Strings` | Cook time brackets: `"0-10m"`, `"10-30m"`, or `"30+m"`. |
| `meal` | `Array of Strings` | Meal category tags: `"breakfast"`, `"lunch"`, `"dinner"`, or `"snack"`. |
| `culture` | `Array of Strings` | Regional lineages (e.g., `["Greek & Mediterranean", "Bistro & Steakhouse"]`). |
| `prep` | `Number` | Estimated preparation time in minutes. |
| `cook` | `Number` | Estimated active cooking time in minutes. |
| `protein` | `Array of Strings` | Main protein vehicles (e.g., `["Chicken", "Eggs"]`). |
| `starch` | `Array of Strings` | Main starch or carbohydrate vehicles (e.g., `["Orzo", "Jasmine Rice"]`). |
| `ingredients` | `Array of Strings` | Itemized ingredient list including freezer blocks and pantry add-ins. |
| `steps` | `Array of Strings` | Sequential cooking instructions. |

---

## 🔍 Multi-Category Filtering Logic

To support maximum flexibility and allow single recipes to span multiple categories (e.g., serving as both lunch and dinner, or combining cross-cultural flavor profiles), all major categorization properties (`culture`, `meal`, `protein`, `starch`, and `time`) are implemented as **Arrays**.

### Evaluation Rules in JavaScript:
1. **Bases & Flavors (OR / Set Intersection):** A recipe matches if **at least one** selected base and **at least one** selected flavor booster is present in the recipe's respective arrays.
2. **Multi-Category Arrays (`meal`, `culture`, `protein`, `starch`, `time`):** When filters are toggled in the UI, the filtering engine performs an array intersection check (`Array.some()`). If the user selects multiple filters within a single category, the recipe will match if it includes **any** of the selected tags.
3. **Cross-Category Filtering (AND Logic):** Across different categories (e.g., combining a Protein filter with a Meal filter), **AND** logic is applied. A recipe must satisfy all active category filters simultaneously to appear in the grid.