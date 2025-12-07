```
// Api
Route::get('/visitor/log-category-wise-visitors', [VisitorTrackingController::class, 'getCategoryWiseVisitors']);

// controller
public function getCategoryWiseVisitors(Request $request)
    {
        $data = VisitorLog::select(
        'page_type',
        DB::raw("COUNT(*) AS total")
        )
        ->groupBy('page_type')
        ->orderByDesc('total')
        ->get();

        return response()->json([
            'status' => true,
            'message' => 'Visitor count by page type',
            'data' => $data
        ], 200);
    }
// modal
     protected $fillable = [
        'visitor_id',
        'page_url',
        'page_type',
        'page_id',
        'page_name',
        'started_at',
        'ended_at',
        'duration_seconds',
    ];

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
```

---

# 📄 README.md

````md
# 📊 Category Wise Visitors Bar Chart (Laravel + React)

This project displays a **Category Wise Visitor Analytics Bar Chart** using Laravel API as backend and React for frontend visualization.

---

## ✅ Features

- Visitor count grouped by `page_type`
- Laravel API for data aggregation
- React bar chart UI with dynamic height
- Responsive & scrollable layout
- Animated bars
- Clean UI with Tailwind CSS
- API based real-time data

---

## 🧱 System Architecture

Visitor Log Database  
⬇  
Laravel Controller  
⬇  
JSON API Response  
⬇  
React Fetch  
⬇  
Bar Chart UI

---

## 🔗 API Endpoint

### Route
```php
Route::get('/visitor/log-category-wise-visitors', 
    [VisitorTrackingController::class, 'getCategoryWiseVisitors']
);
````

### Endpoint URL

```
GET /api/visitor/log-category-wise-visitors
```

---

## 🎯 Controller Method

```php
public function getCategoryWiseVisitors(Request $request)
{
    $data = VisitorLog::select(
        'page_type',
        DB::raw("COUNT(*) AS total")
    )
    ->groupBy('page_type')
    ->orderByDesc('total')
    ->get();

    return response()->json([
        'status' => true,
        'message' => 'Visitor count by page type',
        'data' => $data
    ], 200);
}
```

---

## 📦 API Response Example

```json
{
  "status": true,
  "message": "Visitor count by page type",
  "data": [
    { "page_type": "Home", "total": 120 },
    { "page_type": "Category", "total": 45 }
  ]
}
```

---

## 🗂️ Database Model

### VisitorLog.php

```php
protected $fillable = [
    'visitor_id',
    'page_url',
    'page_type',
    'page_id',
    'page_name',
    'started_at',
    'ended_at',
    'duration_seconds',
];
```

---

## ⚛️ React Bar Chart Component

```jsx
<div className="my-10 bg-white p-6 shadow-lg rounded-xl">
  <h3 className="text-2xl font-bold mb-6 text-center">
    Category Wise Visitors (Bar Chart)
  </h3>

  <div className="flex items-end gap-6 overflow-x-auto h-72 px-4">
    {categoryWiseVisitors.map((item, index) => {
      const max = Math.max(...categoryWiseVisitors.map(d => d.total));
      const heightPercent = (item.total / max) * 100;

      return (
        <div key={index} className="flex flex-col items-center min-w-[70px]">
          <span className="mb-2 text-sm font-bold">{item.total}</span>

          <div className="h-52 w-12 bg-gray-200 flex items-end">
            <div
              className="w-full bg-gradient-to-t from-blue-500 to-indigo-600 transition-all duration-500"
              style={{ height: `${heightPercent}%` }}
            />
          </div>

          <span className="mt-2 text-xs text-center">
            {(item.page_type ?? "Unknown").slice(0, 8)}
          </span>
        </div>
      );
    })}
  </div>
</div>
```

---

## 📐 How Height is Calculated

```js
const max = Math.max(...categoryWiseVisitors.map(d => d.total));
const heightPercent = (item.total / max) * 100;
```

✅ Highest value → 100%
✅ Others scale proportionally

---

## 🎨 UI Features

* Dynamic bar height
* Gradient color
* Smooth animation
* Responsive layout
* Horizontal scroll enabled
* Value shown above each bar
* Label truncation
* Unknown fallback handling

---

## 🛠 Optional Improvements

| Feature        | Description                     |
| -------------- | ------------------------------- |
| Tooltip        | Show exact count on hover       |
| Monthly Filter | Group by month                  |
| Color scale    | Different color by volume       |
| Chart library  | Replace custom UI with Chart.js |

---

## 🚀 Setup Instructions

### Backend (Laravel)

1. Run migrations
2. Ensure `visitor_logs` table exists
3. Add route
4. Add controller method

### Frontend (React)

1. Fetch API

```js
fetch('/api/visitor/log-category-wise-visitors')
  .then(res => res.json())
  .then(data => setCategoryWiseVisitors(data.data));
```

2. Render chart component

---

## 📌 Conclusion

This module provides:

✅ Fast backend aggregation
✅ Clean UI
✅ Simple integration
✅ Expandable structure

It helps visualize traffic patterns across different pages clearly.

---

## 👨‍💻 Author

Developed by Ibrahim Khan
Technology Stack: Laravel + React + Tailwind CSS

---

## ✅ License

Open Source (Free to use & modify)

```


