# Thao tác với mảng trong Android

## Array trong Kotlin

1. Array là một cấu trúc dữ liệu có kích thước cố định.
2. Tạo Array

```kt
val numbers = arrayOf(1, 2, 3, 4, 5) // Array kiểu Int
val strings = arrayOf("A", "B", "C") // Array kiểu String
val mixed = arrayOf(1, "Hello", true) // Array kiểu Any

```

## Các method thường dùng:

### size: Lấy kích thước của mảng.

```
println(numbers.size) // Output: 5

```

### get(index) hoặc array[index]: Lấy giá trị tại vị trí index.

```kt
println(numbers[2]) // Output: 3

```

### set(index, value) hoặc array[index] = value: Gán giá trị tại vị trí index

```kt
numbers[0] = 10
println(numbers[0]) // Output: 10

```

### forEach: Lặp qua từng phần tử.

```kt
numbers.forEach { println(it) }

```

### filter: Lọc phần tử theo điều kiện.

```kt
val filtered = numbers.filter { it > 2 }
println(filtered) // Output: [3, 4, 5]

```

### map: Biến đổi từng phần tử.

```kt
val mapped = numbers.map { it * 2 }
println(mapped) // Output: [2, 4, 6, 8, 10]

```

## List trong Kotlin

- List là một collection có thể thay đổi kích thước. Kotlin có hai loại List
- Immutable List (Không thay đổi được): listOf().
- Mutable List (Có thể thay đổi): mutableListOf().

```kt
val immutableList = listOf(1, 2, 3) // Không thay đổi được
val mutableList = mutableListOf(4, 5, 6) // Có thể thay đổi

```

### Các method thường dùng:

### Thêm phần tử:

```kt
mutableList.add(7)
println(mutableList) // Output: [4, 5, 6, 7]

```

### Xóa phần tử:

```kt
mutableList.remove(5) // Xóa giá trị
println(mutableList) // Output: [4, 6, 7]

mutableList.removeAt(1) // Xóa theo index
println(mutableList) // Output: [4, 7]


```

### Kiểm tra phần tử:

```kt
println(immutableList.contains(2)) // Output: true

```

### Lặp qua List:

```kt
mutableList.forEach { println(it) }

```

### Kết hợp List:

```kt
val combinedList = immutableList + mutableList
println(combinedList) // Output: [1, 2, 3, 4, 7]

```

### Sort (Sắp xếp):

```kt
val sortedList = mutableList.sorted()
println(sortedList) // Output: [4, 7]

```

### filter và map:

```kt
val filtered = mutableList.filter { it > 4 }
println(filtered) // Output: [7]

val mapped = mutableList.map { it * 2 }
println(mapped) // Output: [8, 14]

```
