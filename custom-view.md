# Custom View Demo

## Custom View trong Android là một thành phần giao diện người dùng (UI component) do bạn tự tạo, thay vì sử dụng các thành phần giao diện có sẵn như TextView, Button, hay ImageView. Nó cho phép bạn thiết kế và tạo một thành phần UI theo yêu cầu cụ thể, có thể tái sử dụng nhiều lần và tùy chỉnh dễ dàng.

1. Tạo layout cho StudentCardView, giả sử là student_card.xml.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="16dp"
    android:background="@drawable/card_background">

    <!-- Avatar của học sinh -->
    <ImageView
        android:id="@+id/imgAvatar"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:layout_marginEnd="16dp"
        android:src="@drawable/ic_avatar_placeholder"
        android:scaleType="centerCrop" />

    <!-- Thông tin học sinh -->
    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:orientation="vertical">

        <TextView
            android:id="@+id/txtName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Tên học sinh"
            android:textSize="16sp"
            android:textStyle="bold" />

        <TextView
            android:id="@+id/txtClass"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Lớp: 12A1"
            android:textSize="14sp"
            android:textColor="#666" />

        <TextView
            android:id="@+id/txtAge"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Tuổi: 17"
            android:textSize="14sp"
            android:textColor="#666" />
    </LinearLayout>
</LinearLayout>

```

2. Tạo class StudentCardView và sử dụng View Binding để làm việc với layout.

```kt
package com.example.studentcard

import android.content.Context
import android.util.AttributeSet
import android.view.LayoutInflater
import android.widget.LinearLayout
import com.example.studentcard.databinding.StudentCardBinding

class StudentCardView @JvmOverloads constructor(
    context: Context,
    attrs: AttributeSet? = null,
    defStyleAttr: Int = 0
) : LinearLayout(context, attrs, defStyleAttr) {

    private val binding: StudentCardBinding

    init {
        // Inflate layout using View Binding
        binding = StudentCardBinding.inflate(LayoutInflater.from(context), this, true)
    }

    // Hàm để set thông tin học sinh
    fun setStudentInfo(name: String, className: String, age: Int, avatarResId: Int) {
        binding.txtName.text = name
        binding.txtClass.text = "Lớp: $className"
        binding.txtAge.text = "Tuổi: $age"
        binding.imgAvatar.setImageResource(avatarResId)
    }
}

```

3. Sử dụng Custom View trong XML

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <com.example.studentcard.StudentCardView
        android:id="@+id/studentCard1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp" />

    <com.example.studentcard.StudentCardView
        android:id="@+id/studentCard2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
</LinearLayout>

```

4. Sử dụng trong Activity/Fragment

```kt
package com.example.studentcard

import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.example.studentcard.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {

    // Khai báo biến binding
    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // Khởi tạo binding
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        // Cập nhật thông tin cho từng StudentCardView
        binding.studentCard1.setStudentInfo(
            name = "Nguyễn Văn A",
            className = "12A1",
            age = 17,
            avatarResId = R.drawable.ic_student_avatar_1
        )

        binding.studentCard2.setStudentInfo(
            name = "Trần Thị B",
            className = "11B2",
            age = 16,
            avatarResId = R.drawable.ic_student_avatar_2
        )
    }
}


```
