# Các loại layout (ConstraintLayout, FrameLayout, LinearLayout, RelativeLayout)

1. LinearLayout: có hai dạng dọc và ngang.

2. FrameLayout: Thằng sau đè lên thằng trước;

3. RelativeLayout: Thằng sau đè lên thằng trước, khác nhau là có thể set được vị trí quá từng Id components UI.

4. ConstraintLayout: Dùng các neo, và mối liên hệ giữa các đối tượng UI điều chỉnh vị trí các UI components

# Sử dụng **_binding_** bắt sự kiện ở UI view;

1. set up

- set the **viewBinding** build option to true in the module-level **build.gradle** file

```kotlin
android {
    ...
    buildFeatures {
        viewBinding = true
    }
}
```

2. Use demo;

- **fragment_home.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/tvNumber"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />


    <Button
        android:id="@+id/btnCounter"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Counter"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="50dp"

        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/tvNumber" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

- **MainActivity.kt**

```kt
package com.example.myapplication

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import com.example.myapplication.databinding.FragmentHomeBinding

class MainActivity : AppCompatActivity() {

    //    private var binding: ActivityMainBinding? = null;
    private lateinit var binding: FragmentHomeBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = FragmentHomeBinding.inflate(layoutInflater)
        setContentView(binding.root)
        var number: Int = 0

        binding.run {
            tvNumber.text = "Number of this time $number"
            btnCounter.setOnClickListener {
                number += 1;
                tvNumber.text = "Number of this time $number"
            }

        }
    }
}
```

# Sử dụng **_finViewById_** bắt sự kiện ở UI view;

```xml
<!-- res/layout/activity_main.xml -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/myButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me" />

</LinearLayout>


```

```kt
// MainActivity.kt
package com.example.myapp

import android.os.Bundle
import android.widget.Button
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Find the button using its ID
        val myButton: Button = findViewById(R.id.myButton)

        // Set an OnClickListener on the button
        myButton.setOnClickListener {
            // Handle the button click event
            Toast.makeText(this, "Button Clicked!", Toast.LENGTH_SHORT).show()
        }
    }
}
```

# Sử dụng **_RecyclerView_** để show list.

1. Tạo file **my_item.xml** để show từng item.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/recyclerLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/background_color"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="hello world" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvCar"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:overScrollMode="never" />

</LinearLayout>

```

2. Tạo file **recycle_view_main.xml** để show ra list

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/recyclerLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/background_color"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="hello world" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvCar"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:overScrollMode="never" />

</LinearLayout>

```

2. Tạo class **SupperCar** để tạo đối tượng.

```kt
// SuperCar.kt
package com.example.myapplication

class SuperCar(
    val name: String,
    val imageId: Int
)
```

3. Tạo thêm class **MyAdapter** để xử lý logic và đem show ra màn hình;

```kt
package com.example.myapplication

import android.view.LayoutInflater
import android.view.ViewGroup
import androidx.core.content.ContextCompat
import androidx.recyclerview.widget.RecyclerView
import com.example.myapplication.databinding.MyItemBinding

class MyAdapter(private val superCarList: List<SuperCar>) :
    RecyclerView.Adapter<MyAdapter.SuperCarViewHolder>() {

    internal var onCLickItem: ((SuperCar) -> Unit) = {}


    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): SuperCarViewHolder =
        SuperCarViewHolder(
            MyItemBinding.inflate(
                LayoutInflater.from(parent.context), parent, false
            )
        )

    override fun onBindViewHolder(holder: SuperCarViewHolder, position: Int) {
        holder.onBind(superCarList[position])

    }

    override fun getItemCount() = superCarList.size


    inner class SuperCarViewHolder(private val binding: MyItemBinding) :
        RecyclerView.ViewHolder(binding.root) {

        init {
            binding.imgCar.setOnClickListener {
                onCLickItem.invoke(superCarList[bindingAdapterPosition])
            }
        }

        fun onBind(superCar: SuperCar) {
            binding.run {
                imgCar.setImageDrawable(
                    ContextCompat.getDrawable(
                        itemView.context,
                        superCar.imageId
                    )
                )
                tvCar.text = superCar.name
            }
        }
    }
}

```

4. Dùng ở **MainActivity.kt**

```kt
package com.example.myapplication
import android.annotation.SuppressLint
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.LinearLayoutManager
import com.example.myapplication.databinding.RecycleViewMainBinding

class MainActivity : AppCompatActivity() {

    private var _binding: RecycleViewMainBinding? = null
    private val binding get() = _binding

    private var superCarList: MutableList<SuperCar> = mutableListOf()
    private var myAdapter: MyAdapter? = null

    @SuppressLint("NotifyDataSetChanged")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        _binding = RecycleViewMainBinding.inflate(layoutInflater)
        setContentView(binding?.root)

        // Set up the RecyclerView

        binding?.rvCar?.run {
            myAdapter = MyAdapter(superCarList)
            layoutManager = LinearLayoutManager(context)
            adapter = myAdapter
        }



        superCarList.run {
            add(
                SuperCar("Lamborghini Aventador", R.drawable.img),
            )
            add(
                SuperCar("Ferrari LaFerrari", R.drawable.img_1),
            )
            add(
                SuperCar("Porsche 911", R.drawable.img_2),
            )
            add(
                SuperCar("Lamborghini Aventador", R.drawable.img),
            )
            add(
                SuperCar("Ferrari LaFerrari", R.drawable.img_1),
            )
            add(
                SuperCar("Porsche 911", R.drawable.img_2),
            )
            add(
                SuperCar("Lamborghini Aventador", R.drawable.img),
            )
            add(
                SuperCar("Ferrari LaFerrari", R.drawable.img_1),
            )
            add(
                SuperCar("Porsche 911", R.drawable.img_2),
            )
            add(
                SuperCar("Lamborghini Aventador", R.drawable.img),
            )
            add(
                SuperCar("Ferrari LaFerrari", R.drawable.img_1),
            )
            add(
                SuperCar("Porsche 911", R.drawable.img_2),
            )
        }

        myAdapter?.notifyDataSetChanged()

        initListener()
    }

    private fun initListener() {
        myAdapter?.onCLickItem = {
            Log.i("xxxxxxxxxxx", it.name)
        }
    }
}
```

5. How to create a new adapter with

# How to navigate to new Screen

1. way 1 - create a new

# Note:

1. Khai báo biến:biến

```kt
    private lateinit var tabLayout: TabLayout
    private lateinit var viewPager2: ViewPager2
    private lateinit var adapter: TabLayoutAdapterT

    đổi thành

    private  var tabLayout: TabLayout? =null
    private  var viewPager2: ViewPager2? =null
    private  var adapter: TabLayoutAdapterT? =null


```

2. Phải dùng viewbinding

3. Chú ý dùng val, var

4. Khi thay đổi list mới dùng

```kt
   myAdapter?.notifyDataSetChanged()
```

5. Dùng invod khi khởi tạo bằng null khi

```kt
   internal var onClickFavorite: ((CardItem) -> Unit) = null
   onClickFavorite.invoke(item)

```

# Khi get data về, nên xử lý format ở tầng Data, rồi sau đó mới sử dụng ở UI. Tránh trường hợp sử dụng nhiều function, code trùng lặp.

# Truyền data giữa các Fragnment và Activity

## Section 20: https://enouvo.udemy.com/course/android-app-development-with-kotlin-beginner-to-advanced/learn/lecture/42314374#overview
