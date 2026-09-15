```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n, q;
    cin >> n >> q;
    vector<int> v(n);
    for (int i = 0; i < n; i++)
    {
        cin >> v[i];
    }

    while (q--)
    {
        int l, r;
        cin >> l >> r;
        int sum = 0;
        for (int i = l; i <= r; i++)
        {
            sum += i;
        }
        cout << sum << endl;
    }

    return 0;
}
```
---

## 🔍 What your code is trying to do

You want to:

* Read `n` numbers into an array
* Answer `q` queries
* Each query gives a range `[l, r]`
* Output the **sum of elements from index `l` to `r`**

This is a **range sum query** problem.

---

## 🧠 Code explanation (line by line)

```cpp
#include <bits/stdc++.h>
using namespace std;
```

Includes all standard C++ libraries (common in competitive programming).

---

```cpp
int n, q;
cin >> n >> q;
```

* `n` → number of elements
* `q` → number of queries

---

```cpp
vector<int> v(n);
for (int i = 0; i < n; i++)
{
    cin >> v[i];
}
```

* Creates a vector of size `n`
* Takes input into the array

---

```cpp
while (q--)
{
    int l, r;
    cin >> l >> r;
```

* Loop runs `q` times
* Each time reads a range `[l, r]`

---

```cpp
int sum = 0;
for (int i = l; i <= r; i++)
{
    sum += i;
}
```

❌ **BIG PROBLEM HERE**

You are adding:

```cpp
sum += i;
```

But `i` is just the **index**, not the array value.

✅ You **should add**:

```cpp
v[i]
```

---

```cpp
cout << sum << endl;
```

Prints the result for each query.

---

## ❌ Issues in your code

1. **Wrong sum calculation**

   ```cpp
   sum += i;   // ❌ wrong
   sum += v[i]; // ✅ correct
   ```

2. **Indexing confusion**

   * If input is **1-based index**, you must convert:

     ```cpp
     l--; r--;
     ```

3. **Slow for large input**

   * Time complexity:

     ```
     O(q × n)
     ```
   * This will **TLE** for big constraints.

---

## ✅ Corrected version (basic fix)

```cpp
while (q--)
{
    int l, r;
    cin >> l >> r;

    int sum = 0;
    for (int i = l; i <= r; i++)
    {
        sum += v[i];
    }
    cout << sum << endl;
}
```

⚠️ Still slow if `n, q` are large.

---

## 🚀 Best & Fast Solution: Prefix Sum

### Idea

Precompute sums so each query runs in **O(1)** time.

---

### 🔧 How prefix sum works

Create an array:

```
prefix[i] = sum of elements from 0 to i
```

Then:

```
sum(l, r) = prefix[r] - prefix[l-1]
```

---

### ✅ Optimized code (BEST PRACTICE)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n, q;
    cin >> n >> q;

    vector<int> v(n), prefix(n);

    for (int i = 0; i < n; i++)
        cin >> v[i];

    // Build prefix sum
    prefix[0] = v[0];
    for (int i = 1; i < n; i++)
        prefix[i] = prefix[i - 1] + v[i];

    while (q--)
    {
        int l, r;
        cin >> l >> r;

        int sum;
        if (l == 0)
            sum = prefix[r];
        else
            sum = prefix[r] - prefix[l - 1];

        cout << sum << endl;
    }
    return 0;
}
```

---

## ⏱️ Time Complexity Comparison

| Method        | Time         |
| ------------- | ------------ |
| Your original | ❌ `O(q × n)` |
| Fixed loop    | ❌ `O(q × n)` |
| Prefix sum    | ✅ `O(n + q)` |

---

## 🧠 When to use prefix sum?

* Range sum queries
* Many queries
* Static array (no updates)

---


```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n, q;
    cin >> n >> q;
    vector<int> v(n);
    for (int i = 0; i < n; i++)
    {
        cin >> v[i];
    }

    while (q--)
    {
        int s;
        cin >> s;
        int flag = 0;
        for (int i = 0; i < n; i++)
        {
            if (v[i] == s)
            {
                flag = 1;
            }
        }
        if (flag == 1)
        {
            cout << "Found"<<endl;
        }
        else
        {
            cout << "Not Found"<<endl;
        }
    }

    return 0;
}
```


---

## 🔍 What this code is trying to do

* Read `n` numbers into an array
* Process `q` queries
* For each query, check whether a number `s` exists in the array
* Print `"Found"` or `"Not Found"`

---

## 🧠 Code explanation

```cpp
int n, q;
cin >> n >> q;
```

* `n` → number of elements
* `q` → number of queries

---

```cpp
vector<int> v(n);
for (int i = 0; i < n; i++)
{
    cin >> v[i];
}
```

Reads `n` integers into vector `v`.

---

```cpp
while (q--)
{
    int s;
    cin >> s;
```

Each query asks:
👉 *Is `s` present in the array?*

---

```cpp
int flag = 0;
for (int i = 0; i < n; i++)
{
    if (v[i] == s)
    {
        flag = 1;
    }
}
```

This loop:

* Scans the array
* Sets `flag = 1` if `s` is found

This part is **logically correct**, but inefficient (keeps searching even after finding).

---

## ❌ **MAIN ERROR (Very Important)**

```cpp
if (flag = 1)
```

### 🚨 Problem

* `=` is **assignment**
* `==` is **comparison**

So this line:

```cpp
flag = 1;
```

* Assigns `1` to `flag`
* Always evaluates to `true`

👉 **Result:**
Your program will **ALWAYS print "Found"**, even if the number is not in the array.

---

## ✅ Correct condition

```cpp
if (flag == 1)
```

OR even better:

```cpp
if (flag)
```

---

## ⚠️ Another improvement

Once the element is found, you should **stop the loop**:

```cpp
break;
```

---

## ✅ Fixed version (minimal changes)

```cpp
while (q--)
{
    int s;
    cin >> s;
    int flag = 0;

    for (int i = 0; i < n; i++)
    {
        if (v[i] == s)
        {
            flag = 1;
            break;
        }
    }

    if (flag == 1)
        cout << "Found\n";
    else
        cout << "Not Found\n";
}
```

---

## 🚀 Better Way 1: Using `std::find`

```cpp
if (find(v.begin(), v.end(), s) != v.end())
    cout << "Found\n";
else
    cout << "Not Found\n";
```

---

## 🚀 Better Way 2 (FASTEST): Using `set` or `unordered_set`

### Best for large `q`

```cpp
unordered_set<int> st(v.begin(), v.end());

while (q--)
{
    int s;
    cin >> s;
    if (st.count(s))
        cout << "Found\n";
    else
        cout << "Not Found\n";
}
```

⏱️ **Time Complexity**

| Method          | Time             |
| --------------- | ---------------- |
| Your loop       | `O(n × q)`       |
| `find()`        | `O(n)` per query |
| `unordered_set` | **O(1)** average |

---

## 🧠 Key Takeaways

* ❌ `=` vs `==` is a **classic exam mistake**
* Always break once found
* Use `unordered_set` for fast searching
* `if(flag)` is cleaner than `if(flag == 1)`




----

``` cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n, q;
    cin >> n >> q;

    vector<int> v(n);
    for (int i = 0; i < n; i++)
    {
        cin >> v[i];
    }

    // Binary search needs sorted array
    sort(v.begin(), v.end());

    while (q--)
    {
        int s;
        cin >> s;

        int flag = 0;
        int b = 0, e = n - 1;

        while (b <= e)
        {
            int mid = b + (e - b) / 2;

            if (v[mid] == s)
            {
                flag = 1;
                break;
            }
            else if (v[mid] < s)
            {
                b = mid + 1;
            }
            else
            {
                e = mid - 1;
            }
        }

        if (flag)
            cout << "Found\n";
        else
            cout << "Not Found\n";
    }

    return 0;
}

```


---

## 🧠 What this code is trying to do

For each query:

* Check if number `s` exists in array `v`
* Using **binary search** (faster than linear search)

⚠️ **Important rule**:
👉 **Binary search ONLY works on a sorted array**

Your code **never sorts** the array.

---

## ❌ Errors in your code (VERY IMPORTANT)

### ❌ 1. Array is not sorted

Binary search requires sorted data.

```cpp
sort(v.begin(), v.end()); // REQUIRED
```

Without sorting → **wrong result**.

---

### ❌ 2. Wrong binary search condition

```cpp
while (b < e)
```

This skips checking the last element.

✅ Correct:

```cpp
while (b <= e)
```

---

### ❌ 3. Boundaries update is WRONG

This is the **biggest logical error** 👇

```cpp
else if(v[mid] < s){
    b = 0;
    e = mid;
}
else{
    b = mid + 1;
    e = n - 1;
}
```

🚫 This **resets** the search range every time
Binary search must **shrink the range**, not reset it.

---

### ✅ Correct boundary logic

```cpp
if (v[mid] < s)
    b = mid + 1;
else
    e = mid - 1;
```

---

### ❌ 4. No `break` after finding element

Even after finding `s`, loop keeps running.

---

## ✅ Correct Binary Search Version (Fixed)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, q;
    cin >> n >> q;

    vector<int> v(n);
    for (int i = 0; i < n; i++) {
        cin >> v[i];
    }

    // Binary search needs sorted array
    sort(v.begin(), v.end());

    while (q--) {
        int s;
        cin >> s;

        int flag = 0;
        int b = 0, e = n - 1;

        while (b <= e) {
            int mid = b + (e - b) / 2;

            if (v[mid] == s) {
                flag = 1;
                break;
            }
            else if (v[mid] < s) {
                b = mid + 1;
            }
            else {
                e = mid - 1;
            }
        }

        if (flag)
            cout << "Found\n";
        else
            cout << "Not Found\n";
    }

    return 0;
}
```

---

## 🚀 Even Better: Use STL `binary_search`

```cpp
sort(v.begin(), v.end());

while(q--){
    int s;
    cin >> s;
    if(binary_search(v.begin(), v.end(), s))
        cout << "Found\n";
    else
        cout << "Not Found\n";
}
```

---

## ⏱️ Time Complexity

| Method            | Time         |
| ----------------- | ------------ |
| Linear search     | `O(n × q)`   |
| Binary search     | `O(q log n)` |
| STL binary_search | `O(log n)`   |

---

## 🧠 Key Takeaways (Exam Gold ⭐)

* Binary search **only on sorted array**
* Use `b <= e`, not `b < e`
* Never reset `b` or `e`
* Always `break` when found
* STL exists → use it when allowed



-----
