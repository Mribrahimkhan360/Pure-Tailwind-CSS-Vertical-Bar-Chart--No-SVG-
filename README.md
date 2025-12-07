---
<div className="my-10 bg-white p-6 shadow-lg rounded-xl">
          <h3 className="text-2xl font-bold mb-6 text-center">
            Category Wise Visitors (Bar Chart)
          </h3>

          <div className="flex items-end justify-start gap-6 overflow-x-auto h-72 px-4">
            {categoryWiseVisitors.map((item, index) => {
              const max = Math.max(...categoryWiseVisitors.map(d => d.total));
              const heightPercent = (item.total / max) * 100;

              return (
                <div
                  key={index}
                  className="flex flex-col items-center min-w-[70px]"
                >
                  {/* VALUE */}
                  <span className="mb-2 text-sm font-bold text-gray-700">
                    {item.total}
                  </span>

                  {/* BAR */}
                  <div className="h-52 w-12 bg-gray-200 rounded-lg flex items-end overflow-hidden">
                    <div
                      className="w-full bg-gradient-to-t from-blue-500 to-indigo-600 rounded-lg transition-all duration-500"
                      style={{ height: `${heightPercent}%` }}
                    />
                  </div>

                  {/* LABEL */}
                  <span className="mt-2 text-xs text-gray-800 font-medium truncate w-16 text-center">
                    {(item.page_type ?? "Unknown").slice(0, 8)}
                  </span>
                </div>
              );
            })}
          </div>
        </div>
---

---

# ✅ **Container Div (Outer Box)**

```jsx
<div className="my-10 bg-white p-6 shadow-lg rounded-xl">
```

* `my-10` → উপরে–নিচে margin
* `bg-white` → ব্যাকগ্রাউন্ড সাদা
* `p-6` → padding
* `shadow-lg` → সুন্দর ছায়া
* `rounded-xl` → গোলাকার বর্ডার

এটা পুরো চার্টের container box।

---

# ✅ **Heading**

```jsx
<h3 className="text-2xl font-bold mb-6 text-center">
  Category Wise Visitors (Bar Chart)
</h3>
```

* শিরোনাম লেখা
* 2xl সাইজ, bold, মাঝখানে রাখা

---

# ✅ **Chart Wrapper**

```jsx
<div className="flex items-end justify-start gap-6 overflow-x-auto h-72 px-4">
```

এই divটি bar chart রাখার জন্য:

* `flex` → সব বার এক লাইনে থাকবে
* `items-end` → সব বার নিচ থেকে align হবে
* `gap-6` → বারগুলোর মধ্যে ফাঁকা
* `overflow-x-auto` → ডাটা বেশি হলে horizontal scroll হবে
* `h-72` → chart container এর height
* `px-4` → padding left-right

---

# ✅ **Loop For Each Bar**

```jsx
{categoryWiseVisitors.map((item, index) => {
```

API থেকে পাওয়া ডাটা loop করছে।

---

# ✅ **Max Value বের করা**

```jsx
const max = Math.max(...categoryWiseVisitors.map(d => d.total));
```

সবচেয়ে বড় bar কত উঁচু হবে সেটা বের করা।

---

# ✅ **Height Percentage of Each Bar**

```jsx
const heightPercent = (item.total / max) * 100;
```

প্রতিটি bar-এর height হিসাব করছে percentage হিসাবে।

---

# ✅ **Bar Item Wrapper**

```jsx
return (
  <div
    key={index}
    className="flex flex-col items-center min-w-[70px]"
  >
```

একটি bar ও label কে column আকারে vertically সাজায়।

---

# ✅ **Value Above Each Bar**

```jsx
<span className="mb-2 text-sm font-bold text-gray-700">
  {item.total}
</span>
```

প্রতিটি bar-এর উপরে total সংখ্যাটি দেখায়।

---

# ✅ **Bar Background Box**

```jsx
<div className="h-52 w-12 bg-gray-200 rounded-lg flex items-end overflow-hidden">
```

* `h-52` → bar এর max height
* `w-12` → bar width
* ধূসর ব্যাকগ্রাউন্ড
* ভিতরে real bar bottom থেকে grow করবে

---

# ✅ **Actual Animated Bar**

```jsx
<div
  className="w-full bg-gradient-to-t from-blue-500 to-indigo-600 rounded-lg transition-all duration-500"
  style={{ height: `${heightPercent}%` }}
/>
```

এটাই আপনার আসল bar!

* উপরে দিকে গ্রেডিয়েন্ট নীল
* `heightPercent` অনুযায়ী height
* `transition-all duration-500` → smooth animated effect

---

# ✅ **Label Under Each Bar**

```jsx
<span className="mt-2 text-xs text-gray-800 font-medium truncate w-16 text-center">
  {(item.page_type ?? "Unknown").slice(0, 8)}
</span>
```

* নিচে page_type নাম দেখায়
* নাম বড় হলে কাটে → `.slice(0, 8)`
* `Unknown` fallback

---

