# 📖 Writing Your Own Recipes

The Stacking Studio ([index.html](index.html)) doesn't have any recipes built in. It loads them from JSON files:

1. **`recipes.json`** at the root of this repo is the default library. It loads automatically when the page opens.
2. **Your own files** can be imported from the page. They **merge** into the library.

This page covers the file format, every recipe property, and how filtering and importing work.

---

## 🚀 Quick start

1. Copy the template below into a new file, e.g. `my-recipes.json`.
2. Fill in your recipe(s). Every recipe needs a unique `id` and a `title`.
3. Open the Stacking Studio and click **Import** (in the header or under *Recipe Library* in the sidebar), or drag and drop the file onto the page.
4. Your recipes show up right away and stay there when you reload, because they're saved in your browser.

```json
{
  "schemaVersion": 1,
  "recipes": [
    {
      "id": "my-weeknight-skillet",
      "title": "My Weeknight Skillet",
      "description": "One sentence that sells the dish.",
      "servings": 2,
      "prepMinutes": 5,
      "cookMinutes": 12,
      "meals": ["lunch", "dinner"],
      "proteins": ["chicken", "turkey"],
      "cultures": ["mexican"],
      "starches": ["rice", "tortillas"],
      "tags": ["one-pan"],
      "bases": [{ "id": 2, "cubes": 2 }],
      "boosters": [{ "id": "D", "cubes": 1 }],
      "ingredients": [
        { "item": "chicken thighs", "qty": "1 lb", "aisle": "meat", "protein": "chicken" },
        { "item": "turkey cutlets", "qty": "1 lb", "aisle": "meat", "protein": "turkey" },
        { "item": "lime", "qty": "1", "aisle": "produce" }
      ],
      "steps": [
        { "title": "Sear", "text": "Sear the protein until golden." },
        { "protein": "turkey", "text": "Turkey is lean, so pull it 1 minute early." },
        "Melt the cubes with 2 tbsp water and toss everything together."
      ],
      "notes": ["Freezes well for up to 3 months."]
    }
  ]
}
```

> **Opening the page from disk?** Browsers won't let a page opened as `file://` read `recipes.json`. Run `python3 -m http.server` in this folder and visit <http://localhost:8000>. You can also just import `recipes.json` by hand. Imported recipes work either way.

---

## 📦 File structure

| Key | Type | Required | Description |
|---|---|---|---|
| `schemaVersion` | number | recommended | Format version. Currently `1`. |
| `recipes` | array | ✅ | The list of recipe objects. |

A bare JSON array of recipes (`[ {...}, {...} ]`) also works when importing.

---

## 🧾 Recipe properties

### Identity & display

| Property | Type | Required | Description |
|---|---|---|---|
| `id` | string | ✅ | Unique, stable identifier, such as `"chipotle-taco-skillet"`. It's normalized to lowercase-kebab-case. **Importing a recipe with an `id` that already exists replaces that recipe.** |
| `title` | string | ✅ | Display name. |
| `description` | string | | One or two sentences shown on the card and in the recipe view. |
| `servings` | number \| string | | `2` or `"12 halves"`. |
| `tags` | string[] | | Free-form keywords like `"one-pan"`, `"meal-prep"`, `"freezer-friendly"`. They show on the recipe and are **searchable**, but they don't get a filter group. |

### Time

| Property | Type | Description |
|---|---|---|
| `prepMinutes` | number | Hands-on prep time. Defaults to `0`. |
| `cookMinutes` | number | Cooking time. Defaults to `0`. |

You don't set the **Total Time** filter yourself. The page adds `prepMinutes + cookMinutes` and puts the recipe in one bucket:

| Bucket | Rule |
|---|---|
| `0–10 min` | total ≤ 10 |
| `10–30 min` | 11 ≤ total ≤ 30 |
| `30+ min` | total > 30 |

### Filter axes (multi-value)

Every filter axis is an **array**, so one recipe can satisfy several options. For example, a taco skillet that works with ground beef *or* ground turkey for lunch *or* dinner:

```json
"meals": ["lunch", "dinner"],
"proteins": ["ground-meat", "turkey"]
```

Values are case-insensitive and normalized to kebab-case, so `"Ground Meat"` becomes `ground-meat`. Use the **canonical values** below so your recipes line up with the built-in filter chips. If you use a value that isn't in the list, such as `"lamb"` or `"caribbean"`, it **gets its own filter chip automatically**.

#### `meals`

| Value | Label |
|---|---|
| `breakfast` | Breakfast |
| `lunch` | Lunch |
| `dinner` | Dinner |
| `snack` | Snack |

#### `proteins`

| Value | Label | Use for |
|---|---|---|
| `chicken` | Chicken | Thighs, breasts, ground chicken, rotisserie |
| `ground-meat` | Ground Meat | Ground beef, pork, lamb, or blends |
| `eggs` | Eggs | Any egg-centric dish |
| `turkey` | Turkey | Cutlets, tenderloin, ground turkey |
| `beef` | Beef & Steak | Whole-muscle beef |
| `pork` | Pork | Chops, tenderloin, sausage |
| `seafood` | Fish & Seafood | |
| `tofu` | Tofu & Tempeh | |
| `beans` | Beans | Black, pinto, white, etc. |
| `chickpeas` | Chickpeas | |
| `lentils` | Lentils | |

> 💡 **Overlap is fine.** A ground-turkey dish can list both `"turkey"` and `"ground-meat"`, so it matches either filter.

#### `cultures`

| Value | Label |
|---|---|
| `mediterranean` | Mediterranean |
| `european` | European Bistro |
| `mexican` | Mexican & Tex-Mex |
| `south-asian` | South Asian |
| `east-asian` | East Asian |
| `southeast-asian` | Southeast Asian |
| `middle-eastern` | Middle Eastern |
| `american` | American |

#### `starches`

| Value | Label |
|---|---|
| `rice` | Rice |
| `pasta` | Pasta |
| `noodles` | Noodles |
| `bread` | Bread & Toast |
| `tortillas` | Tortillas |
| `potatoes` | Potatoes |
| `grains` | Grains (quinoa, farro, etc.) |
| `none` | No Starch |

An empty or missing `starches` array is treated as `["none"]`.

### Freezer block stack

These tie a recipe to the Base & Booster system described in the [README](README.md).

| Property | Type | Description |
|---|---|---|
| `bases` | array | Structural Bases used. Each entry is `{ "id": 1-4, "cubes": n }`. The shorthand `2` means `{ "id": 2, "cubes": 1 }`. |
| `boosters` | array | Flavor Boosters used. Each entry is `{ "id": "A"-"D", "cubes": n }`. The shorthand `"D"` means `{ "id": "D", "cubes": 1 }`. |

| Base `id` | Name | | Booster `id` | Name |
|---|---|---|---|---|
| `1` | Clean French Mirepoix | | `A` | Euro-Bistro |
| `2` | Roasted Allium-Tomato Jam | | `B` | East & SE Asian Umami |
| `3` | Green Citrus & Herb Slurry | | `C` | South Asian Masala |
| `4` | Velvet Garlic-Nut Cream | | `D` | Latin & Tex-Mex Adobo |

Listed blocks are all **used together** in the recipe. The *Freezer Bases* and *Boosters* filters match any recipe that uses **at least one** of the selected blocks. Cube counts are added up in the shopping list's **Pull from the freezer** summary.

Don't list freezer cubes in `ingredients`. They come from `bases` and `boosters`, and keeping them out stops them from showing up on the grocery list.

### `ingredients`

An array of ingredient objects. A plain string also works, but it lands in the "Other" aisle with no quantity.

| Property | Type | Description |
|---|---|---|
| `item` | string ✅ | The ingredient name, e.g. `"boneless chicken thighs"`. The same `item` + `aisle` in different planned recipes is **merged into one grocery line**. |
| `qty` | string | Free-text amount: `"1 lb"`, `"2 cups"`, `"to serve"`. Merged lines show both, like `1 lb + 1 lb`. |
| `aisle` | string | Grocery section used to group the shopping list (see below). Defaults to `other`. |
| `note` | string | Prep note shown after the item: `"finely diced"`. |
| `optional` | boolean | Marks the item as optional in the recipe and the shopping list. |
| `protein` | string | **Protein variant.** Only shown when this protein is selected (see below). |

**Aisles:** `produce`, `meat`, `dairy-eggs`, `bakery`, `pantry`, `spices`, `frozen`, `other`. Other values are allowed and appear as extra sections.

### `steps`

An array of step objects (or plain strings).

| Property | Type | Description |
|---|---|---|
| `text` | string ✅ | The instruction. Be specific: heat level, time, and the visual cue for "done". |
| `title` | string | A short bold heading such as `"Sear"` or `"Build the sauce"`. |
| `protein` | string | **Protein variant.** Only shown when this protein is selected. |

Steps are numbered automatically, and variant steps that are hidden aren't counted.

### `notes`

An array of strings shown as **Notes & Swaps**. Use it for storage tips, substitutions, and ways to scale the recipe up or down.

---

## 🔀 Protein variants

When a recipe lists more than one protein **and** at least one ingredient or step has a `protein` key, the recipe view shows a **"Cook it with"** picker. Picking a protein:

- shows ingredients and steps with **no** `protein` key, which are shared by every version,
- shows ingredients and steps whose `protein` matches the pick,
- hides the rest.

The pick also carries over to the **meal plan**, so the grocery list only includes that protein. If a protein filter is active, the picker starts on the matching protein.

```json
"proteins": ["chicken", "tofu"],
"ingredients": [
  { "item": "chicken thighs", "qty": "1 lb", "aisle": "meat", "protein": "chicken" },
  { "item": "extra-firm tofu", "qty": "14 oz", "aisle": "produce", "protein": "tofu" },
  { "item": "jasmine rice", "qty": "2 cups", "aisle": "pantry" }
],
"steps": [
  { "protein": "chicken", "text": "Sear the chicken 4 minutes per side." },
  { "protein": "tofu",    "text": "Fry the tofu 8 minutes, turning, until crisp." },
  { "text": "Melt the cubes and toss to glaze." }
]
```

If a recipe lists several proteins but has no variant ingredients or steps, they show as plain "Protein" tags, meaning the recipe simply works with any of them as written.

---

## 🔍 How filtering works

- **Within a group, OR.** Selecting *Chicken* and *Turkey* shows recipes that list either one.
- **Across groups, AND.** *Chicken* + *Breakfast* shows only recipes that list both.
- The number on each chip is how many recipes you'd see if you added that option to your current filters. Chips with `0` are dimmed.
- **Search** matches every word you type against the title, description, tags, ingredient names, and all filter values.

---

## 📥 Importing & merging

- **Import** accepts one or more `.json` files. You can also drag and drop them onto the page.
- Recipes are matched by `id`:
  - a **new** `id` is added to the library,
  - an **existing** `id` is **replaced** by the imported version. This includes default recipes, so you can override one by importing a recipe with the same `id`.
- Any recipe without an `id` or `title`, or any file that isn't valid JSON, is skipped. A message tells you what was skipped and why.
- Imported recipes are saved in your browser's `localStorage`. They don't change the files on disk, and they stay until you click **Remove imported**.
- **Export** downloads your whole merged library as a single `recipes.json`. Use it to share recipes or to make your imports the new defaults by committing the file.

---

## ✅ Recipe-writing checklist

- [ ] `id` is unique and won't change. Meal plans refer to recipes by `id`.
- [ ] `meals`, `proteins`, `cultures`, and `starches` list **every** option the recipe genuinely supports.
- [ ] `prepMinutes` and `cookMinutes` are honest, since the time filter depends on them.
- [ ] Every block in `bases` and `boosters` is actually mentioned in a step, with its cube count.
- [ ] Ingredients have an `aisle` so the shopping list groups cleanly.
- [ ] Protein-specific ingredients and steps are tagged with `protein`.
- [ ] Steps include heat level, timing, and how to tell when it's done.
