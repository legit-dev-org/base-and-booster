# 🧊 The Base and Booster system
### *A High-Leverage, Stackable Flavor Engine for 15-Minute Meals*

---

## 🌟 Overview

Cooking high-variety, deep-flavor weeknight meals usually requires endless prep, chopping aromatics from scratch, and keeping dozens of perishable ingredients in the fridge. 

The **Modular Freezer Block System** solves this by decoupling **Structure (Texture, Body, Moisture)** from **Regional Identity (Concentrated Spices & Aromatics)**. 

By batch-prepping and freezing **4 Structural Bases** and **4 High-Intensity Flavor Boosters**, you unlock a 2-dimensional matrix ($4 \times 4 + \text{Multi-stacks}$) capable of producing over **100 distinct global dishes** in under 15 minutes. 

The Stacking Studio ships with **365 curated recipes — one for every day of the year** — spanning breakfast, lunch, dinner, and snacks across 8 cuisines and 11 proteins.

```
                       ┌──────────────────────────────────────┐
                       │        YOUR BASE INGREDIENTS         │
                       │ (Protein + Starch + Fresh Garnishes) │
                       └──────────────────┬───────────────────┘
                                          │
                                          ▼
┌───────────────────────────────┐                  ┌───────────────────────────────┐
│     STRUCTURAL BASES (1–4)    │                  │  CULTURAL FLAVOR BOOSTERS (A–D)│
│   (Body, Moisture, Thickness) │   ＋ STACKED WITH │   (High-Intensity Spices/Fats)│
└──────────────┬────────────────┘                  └──────────────┬────────────────┘
               │                                                  │
               └──────────────────────────┬───────────────────────┘
                                          │
                                          ▼
                       ┌──────────────────────────────────────┐
                       │        INSTANT MASTER PAN SAUCE      │
                       │   (Melted & Emulsified in 90 Secs)   │
                       └──────────────────────────────────────┘
```

---

## 🖥️ Using the Stacking Studio

[`index.html`](index.html) is the recipe finder for this system. Use it to:

* **Filter recipes** by meal, total time, protein, culture, starch, freezer base, and booster.
* **View recipes** with the full freezer-block stack, ingredients, and step-by-step method.
* **Build a meal plan and shopping list.** Add recipes to your plan to get a merged grocery list grouped by aisle, plus how many freezer cubes to pull. The batch-prep and weeknight-staples checklists are there too.

The 365 default recipes load from [`recipes.json`](recipes.json). Because browsers block reading local files, serve the folder instead of opening the HTML directly:

```bash
python3 -m http.server
# then open http://localhost:8000
```

### 📖 Add your own recipes

Write recipes in the same JSON format and click **Import** on the page (or drag the file in). Imported recipes merge with the defaults by `id`. **See [RECIPE.md](RECIPE.md)** for the full recipe format, every property, the canonical filter values, protein variants, and how importing works.

---

## 📐 Why This Architecture Works

### 1. Zero Flavor Overlap 🎯
Other meal prep bases often mix spices directly into vegetable purées. This creates "mono-flavor" traps—where every meal tastes like the same generic curry or stew. By keeping **Bases unspiced** and **Flavor Boosters hyper-concentrated**, each cube does one job with maximum precision.

### 2. Physical & Chemical Layering 🧪
* **Bases** leverage slow-cooked alliums, glutamates ($MSG / Guanys$), citrus pectin, and nut/seed emulsifiers to build viscosity and body.
* **Flavor Boosters** leverage *fat-blooming (Tadka)* and reduction techniques to capture volatile aromatic compounds that melt out instantaneously when hit with heat and liquid.

### 3. Rapid 90-Second Emulsification ⚡
When 1 Base block meets 1 Flavor block in a hot skillet with 2–3 tablespoons of broth or water, the fats, starches, and liquid instantly bind into a restaurant-quality pan reduction without needing flour, cornstarch, or hours of simmering.

---

## 🏗️ Part 1: The 4 Structural Bases (Body & Texture)

The Bases govern the physical mechanics of the dish—whether it is clear and light, deep and dark, bright and acidic, or rich and creamy.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                             THE 4 STRUCTURAL BASES                          │
├────────────────────────────┬────────────────────────────────────────────────┤
│ 🧅 1. Clean French Mirepoix │ Sweet, un-browned aromatic cushion           │
├────────────────────────────┼────────────────────────────────────────────────┤
│ 🧄 2. Roasted Allium Jam   │ Deep, dark caramelized umami powerhouse        │
├────────────────────────────┼────────────────────────────────────────────────┤
│ 🌿 3. Green Citrus Slurry  │ Bright, acidic, herbaceous green backbone      │
├────────────────────────────┼────────────────────────────────────────────────┤
│ 🥛 4. Velvet Garlic Cream  │ Silky, nutty emulsion base (Dairy-Free)        │
└────────────────────────────┴────────────────────────────────────────────────┘
```

### 🧅 Base 1: Clean French Mirepoix
* **The Profile:** Sweet yellow onions, sweet carrots, and crisp celery sweated slowly in light fat without any browning.
* **Why it was chosen:** You cannot build delicate clear broths, subtle grain pilafs, or refined bistro sauces using a base laden with garlic or dark roasted tomatoes. Base 1 provides an invisible aromatic backbone that elevates without overpowering.

### 🧄 Base 2: Roasted Allium-Tomato Jam
* **The Profile:** Deeply caramelized onions, roasted garlic cloves, concentrated tomato paste, and balsamic reduction.
* **Why it was chosen:** This is the heavy lifter for comfort food. It supplies natural sugars and heavy glutamates that traditionally take hours of braising to achieve.

### 🌿 Base 3: Green Citrus & Herb Slurry
* **The Profile:** Charred poblano peppers, fresh cilantro/parsley stems, green scallions, ginger, extra virgin olive oil, and fresh citrus.
* **Why it was chosen:** Cooked foods need fresh acidity to taste alive. Base 3 acts as both a cooked green base (for Verde skillets or green curries) and an instant cold dressing when thawed for salads.

### 🥛 Base 4: Velvet Garlic-Nut Cream
* **The Profile:** Blanched cashews (or sunflower seeds), roasted garlic, mild broth, and lemon zest whipped into a dense cream block.
* **Why it was chosen:** Creamy sauces are notoriously difficult to prep without dairy breaking or spoiling. This base provides a stable, rich emulsion that converts any pan sauce into a velvety Alfredo, Tikka Masala, or Bisque in seconds.

---

## 🌶️ Part 2: The 4 Cultural Flavor Boosters (Regional Identity)

The Flavor Boosters are fat-soluble spice concentrates that immediately define the regional lineage of your meal.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          THE 4 CULTURAL BOOSTERS                            │
├────────────────────────────┬────────────────────────────────────────────────┤
│ 🍷 A. Euro-Bistro          │ Red wine, cracked black pepper, thyme, Dijon   │
├────────────────────────────┼────────────────────────────────────────────────┤
│ 🥢 B. East & SE Asian      │ Ginger, scallion, lemongrass, galangal, sesame │
├────────────────────────────┼────────────────────────────────────────────────┤
│ 🕌 C. South Asian Masala   │ Bloomed mustard seed, cumin, curry leaf, hing │
├────────────────────────────┼────────────────────────────────────────────────┤
│ 🌮 D. Tex-Mex & Latin      │ Smoky chipotle, ancho chili, cumin, oregano    │
└────────────────────────────┴────────────────────────────────────────────────┘
```

### 🍷 Flavor A: Euro-Bistro & Steakhouse
* **Key Notes:** Concentrated red wine reduction, cracked black peppercorns, roasted garlic, woodsy thyme, rosemary, and Dijon mustard.
* **Why it was chosen:** Guarantees full coverage for classic European bistro plates, pan-seared steak reductions, pub gravies, and garlic-herb hashes.

### 🥢 Flavor B: East & SE Asian Umami
* **Key Notes:** Fresh ginger, scallions, crushed lemongrass, galangal, toasted sesame oil, tamari, and coconut cream concentrate.
* **Why it was chosen:** Combines the punch of an East Asian ginger-scallion confit with the aromatic florals of Southeast Asian lemongrass, powering everything from lo mein to Tom Kha soups.

### 🕌 Flavor C: South Asian Masala (The Tadka Engine)
* **Key Notes:** Whole black mustard seeds and cumin bloomed in oil with fresh curry leaves, turmeric, ginger, green chilies, and asafoetida.
* **Why it was chosen:** Harnesses the traditional *Tadka* technique (blooming whole spices in hot fat to unlock essential oils), instantly transforming any base into authentic dhals, curries, and spiced hashes.

### 🌮 Flavor D: Latin & Tex-Mex Adobo
* **Key Notes:** Rehydrated dark ancho chilies, smoky chipotle peppers, Mexican oregano, cumin, apple cider vinegar, and garlic.
* **Why it was chosen:** Captures the deep, earthy, tangy heat of slow-simmered Mexican adobos, clinging perfectly to taco fillings, bean chilis, and enchilada glazes.

---

## 🔀 Part 3: The Stacking Logic Matrix

By pairing a **Structural Base** with a **Flavor Booster**, you effortlessly construct sauces across global culinary styles:

```
                  ┌──────────────────────┬──────────────────────┬──────────────────────┬──────────────────────┐
                  │ 🍷 FLAVOR A          │ 🥢 FLAVOR B          │ 🕌 FLAVOR C          │ 🌮 FLAVOR D          │
                  │ (Euro-Bistro)        │ (East/SE Asian)      │ (South Asian)        │ (Tex-Mex/Latin)      │
┌─────────────────┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ 🧅 BASE 1       │ Lemon-Herb Piccata   │ Ginger Lo Mein       │ Yellow Dhal Tadka    │ Arroz Rojo           │
│ (Mirepoix)      │ French Onion Soup    │ Congee / Porridge    │ Mustard Seed Rice    │ Taco Rice Skillet    │
├─────────────────┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ 🧄 BASE 2       │ Bistro Steak Reduction│ Ginger Ramen Broth   │ Tempered Chickpeas   │ 10-Min Black Bean    │
│ (Allium Tomato) │ Braised Shepherd Pie │ Massaman Skillet     │ Tikka Gravy          │ Chipotle Chili       │
├─────────────────┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ 🌿 BASE 3       │ Herb Roasted Potatoes│ Fiery Green Curry    │ South Indian Curry   │ Verde Bean Tacos     │
│ (Green Citrus)  │ Greek Grain Bowl     │ Thai Rice Noodle Soup│ Mint-Cilantro Hash   │ Charred Corn Salad   │
├─────────────────┼──────────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ 🥛 BASE 4       │ Peppercorn Cream Toss│ Miso Sesame Udon     │ Creamy Korma Tofu    │ Creamy Enchilada     │
│ (Velvet Cream)  │ Garlic White Beans   │ Red Coconut Noodle   │ Creamy Tikka Masala  │ Chipotle Chowder     │
└─────────────────┴──────────────────────┴──────────────────────┴──────────────────────┴──────────────────────┘
```

---

## 🍳 Part 4: Dinnertime Workflow (Under 15 Minutes)

```
  1. POP CUBES             2. MELT & EMULSIFY          3. TOSS PROTEIN/STARCH        4. GARNISH & SERVE
┌──────────────┐          ┌──────────────────┐        ┌──────────────────────┐      ┌──────────────────┐
│  Pull 1 Base │          │ Drop into hot    │        │ Add cooked rice,     │      │ Finish with fresh│
│  + 1 Flavor  ├─────────►│ pan with 2-3 tbsp├───────►│ noodles, beans, or   ├────► │ herbs, citrus, or│
│  from freezer│          │ water or broth   │        │ seared protein       │      │ crunchy nuts     │
└──────────────┘          └──────────────────┘        └──────────────────────┘      └──────────────────┘
```

1. **Pop Your Blocks:** Open your freezer bags and grab 1 or 2 Base cubes plus 1 Flavor Booster cube.
2. **Flash Melt:** Drop them directly into a hot skillet over medium heat. Add 2–3 tablespoons of hot water or vegetable broth. Watch the blocks dissolve and emulsify into a rich, aromatic pan glaze in under 90 seconds.
3. **Coat Protein & Starch:** Toss in your pre-cooked grains, boiled noodles, canned beans, or seared proteins directly into the bubbling glaze.
4. **Finish Clean:** Hit the dish with fresh garnishes (chopped cilantro, parsley, toasted nuts, or fresh lemon wedges) to contrast the deep, cooked flavor of the bases.
