# MutiLiv



# run, let
- Dùng run khi bạn muốn tập trung vào this và thực hiện các thao tác tuần tự.
```kotlin
val result = myObject.run {
    // các thao tác với myObject
    this.someFunction()
    anotherFunction()
    // trả về giá trị từ khối
    "Result"
}
```
- Dùng let khi bạn chỉ cần làm việc với một đối tượng không null và không cần trực tiếp sử dụng this.

```kotlin
val result = myObject?.let {
    // các thao tác với myObject
    it.someFunction()
    anotherFunction()
    // trả về giá trị từ khối
    "Result"
}
```
# Biến và hằng số

- Biến (variable): Dùng từ khóa **var**. Giá trị của biến có thể thay đổi.

```kotlin

var age: Int = 25
println("Age: $age") // Output: Age: 25
age = 26
println("Updated Age: $age") // Output: Updated Age: 26

```

- Hằng số: Dùng từ khóa **val**. Giá trị của hằng số không thể thay đổi sau khi được gán.

```kotlin
fun main() {
    // Declares the variable x and initializes it with the value of 5
    val x: Int = 5
    // 5
    println(x)
}
```

- Kotlin supports type inference and automatically identifies the data type of a declared variable. When declaring a variable, you can omit the type after the variable name:

```kotlin
fun main() {
    // Declares the variable x with the value of 5;`Int` type is inferred
    val x = 5
    print(x)
    // 5
    println(x)
}
```

# Các kiểu dữ liệu

- Int: Số nguyên

```kotlin
val myInt: Int = 10
println("Int: $myInt") // Output: Int: 10

```

- Double: Số thực

```kotlin
val myDouble: Double = 10.5
println("Double: $myDouble") // Output: Double: 10.5

```

- String: Chuỗi ký tự

```kotlin
val myString: String = "Hello, Kotlin"
println("String: $myString") // Output: String: Hello, Kotlin
```

- Boolean: Giá trị đúng hoặc sai

```kotlin
val myBoolean: Boolean = true
println("Boolean: $myBoolean") // Output: Boolean: true

```

- List: Danh sách các phần tử

```kotlin
val myList: List<Int> = listOf(1, 2, 3, 4, 5)
println("List: $myList") // Output: List: [1, 2, 3, 4, 5]

```

- Map: Tập hợp các cặp key-value

```kotlin

fun main() {
    // Tạo một map chỉ đọc để lưu trữ thông tin sinh viên
    val studentMap: Map<Int, String> = mapOf(
        101 to "Nguyễn Văn A",
        102 to "Trần Thị B",
        103 to "Lê Văn C"
    )

    // Truy cập giá trị theo key
    println(studentMap[101])  // Output: Nguyễn Văn A
    println(studentMap[102])  // Output: Trần Thị B

    // Duyệt qua các phần tử trong map
    for ((id, name) in studentMap) {
        println("ID: $id, Name: $name")
    }
}

//output

Nguyễn Văn A
Trần Thị B
ID: 101, Name: Nguyễn Văn A
ID: 102, Name: Trần Thị B
ID: 103, Name: Lê Văn C


//Tìm kiếm sinh viên theo ID
fun main() {
    fun findStudentName(studentMap: Map<Int, String>, studentId: Int): String? {
    return studentMap[studentId]
}

    val studentMap: Map<Int, String> = mapOf(
        101 to "Nguyễn Văn A",
        102 to "Trần Thị B",
        103 to "Lê Văn C"
    )

    val studentIdToFind = 100
    val studentName = findStudentName(studentMap, studentIdToFind)

    if (studentName != null) {
        println("Tên sinh viên có mã số $studentIdToFind là $studentName")
    } else {
        println("Không tìm thấy sinh viên có mã số $studentIdToFind")
    }
}

```

# Package definition and imports

```kotlin
package my.demo

import kotlin.text.*

// ...
```

# Program entry point

```kotlin
fun main() {
    println("Hello world!")
}

fun main(args: Array<String>) {
    println(args.contentToString())
}
```

# Functions

```kotlin
//demo1
fun sum(a: Int, b: Int): Int {
    return a + b
}

//demo2
fun sum(a: Int, b: Int) = a + b

//demo3
fun printSum(a: Int, b: Int) {
    println("sum of $a and $b is ${a + b}")
}

```

# Creating classes and instances

- To define a class, use the class keyword:

```kotlin
class Shape
```

- Properties of a class can be listed in its declaration or body

```kotlin
class Rectangle(val height: Double, val length: Double) {
    val perimeter = (height + length) * 2
}
```

- Rectangle kế thừa thuộc tính của Shape

```kotlin
open class Shape

class Rectangle(val height: Double, val length: Double): Shape() {
    val perimeter = (height + length) * 2
}

```

# Conditional expressions

- **if else**:

```kotlin
val a = 5
val b = 10
if (a > b) {
    println("a lớn hơn b")
} else if (a == b) {
    println("a bằng b")
} else {
    println("a nhỏ hơn b")
}
// Output: a nhỏ hơn b


```

- **when** (case)

```kotlin
val x = 2
when (x) {
    1 -> println("x là 1")
    2 -> println("x là 2")
    3 -> println("x là 3")
    else -> println("x không phải là 1, 2, hay 3")
}
// Output: x là 2
```

# Vòng lặp

- **for**: Dùng để lặp qua một dãy các phần tử.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
for (number in numbers) {
    println(number)
}
// Output:
// 1
// 2
// 3
// 4
// 5


//demo2
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}

//output
//item at 0 is apple
//item at 1 is banana
//item at 2 is kiwifruit

```

- **while**: Lặp khi điều kiện còn đúng.

```kotlin
var i = 0
while (i < 5) {
    println(i)
    i++
}
// Output:
// 0
// 1
// 2
// 3
// 4
```

- **do-while**: Lặp ít nhất một lần, sau đó kiểm tra điều kiện.

```kotlin
var j = 0
do {
    println(j)
    j++
} while (j < 5)
// Output:
// 0
// 1
// 2
// 3
// 4


```

# SpannableString in androidkotlin

1. Mở res/layout/activity_main.xml và thêm một TextView:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!"
        android:textSize="18sp"
        android:layout_centerInParent="true"/>
</RelativeLayout>


```

2.

```kt
package com.example.spannablestringexample

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val textView = findViewById<TextView>(R.id.textView)
        val spannableString = SpannableString("This is a SpannableString example.")

        // Apply bold style to "SpannableString"
        spannableString.setSpan(
            StyleSpan(Typeface.BOLD),
            10,
            24,
            Spannable.SPAN_INCLUSIVE_INCLUSIVE
        )

        // Apply background color to "example"
        spannableString.setSpan(
            BackgroundColorSpan(Color.YELLOW),
            25,
            32,
            Spannable.SPAN_INCLUSIVE_INCLUSIVE
        )

        // Apply foreground color to "This"
        spannableString.setSpan(
            ForegroundColorSpan(Color.RED),
            0,
            4,
            Spannable.SPAN_INCLUSIVE_INCLUSIVE
        )

        // Apply underline to "SpannableString"
        spannableString.setSpan(
            UnderlineSpan(),
            10,
            24,
            Spannable.SPAN_INCLUSIVE_INCLUSIVE
        )

        textView.text = spannableString
    }
}


```

# **_Parcelable_** cho phép truyền các oject thông qua các **_newInstance_**

- documemt: https://developer.android.com/kotlin/parcelize

1. Tạo data class **CardItem**

```kt
package com.example.aspenbase.data

import android.os.Parcelable
import kotlinx.parcelize.Parcelize

@Parcelize
data class CardItem(
    var imageRes: Int,
    var title: String,
    var rating: Double,
    var isFavorite: Boolean = false
): Parcelable
```

2. Truyền data:

```kt

//truyền
 companion object {

        private  const val  KEY_CARD_ITEM = "key_card_item"

        internal fun newInstance(item: CardItem): DetailFragment = DetailFragment().apply {
            arguments = Bundle().apply {
                putParcelable(KEY_CARD_ITEM, item)
            }
        }
    }

//nhận
    private  fun initView (){
        cardItem = arguments?.getParcelable(KEY_CARD_ITEM) //thông qua key

        cardItem?.run {
            val drawable = ContextCompat.getDrawable(requireContext(), imageRes)

            binding?.run {
                tvTitle.text = title
                tvRating.text = rating.toString()
                ivCard.setImageDrawable(drawable)
                imageButtonFavorite.setImageResource(
                    if (isFavorite) {
                        R.drawable.baseline_favorite
                    } else {
                        R.drawable.baseline_favorite_border
                    }
                )
            }
        }
}
```

# Function Declaration

1. Demo

```kt

fun addNumber(x:Int, y:Int): Int {
    var sum = 0;
    sum = x +y;
    return sum
}

```

# Object and Class

1.
