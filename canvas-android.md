# Canvas trong Android

Canvas trong Android là một công cụ mạnh mẽ để vẽ đồ họa tùy chỉnh. Nó được sử dụng để tạo giao diện độc đáo, hiệu ứng đặc biệt hoặc xử lý đồ họa phức tạp.

## Tổng quan

Canvas là một lớp cung cấp các phương thức để vẽ:

- **Hình học cơ bản** (đường thẳng, hình tròn, hình chữ nhật, hình elip).
- **Đoạn văn bản**.
- **Bitmap**.

### Canvas hoạt động cùng với lớp `Paint` để định nghĩa các thuộc tính đồ họa như màu sắc, độ dày nét vẽ, và kiểu vẽ.

- Lớp Paint không phải là bắt buộc, nhưng nó rất quan trọng để định nghĩa cách các đối tượng đồ họa được vẽ.
- Một số thuộc tính quan trọng của Paint:
  - color: Đặt màu sắc.
  - style: Định nghĩa kiểu vẽ (nét viền STROKE, màu đầy FILL, hoặc cả hai FILL_AND_STROKE).
  - strokeWidth: Độ dày của đường nét.
  - textSize: Kích thước chữ khi vẽ văn bản.

---

## Phương thức Canvas API thông dụng:

Dưới đây là bảng liệt kê các phương thức phổ biến trong API của Canvas được phân loại theo từng nhóm chức năng:

### **Hình học cơ bản**

| **Phương thức**                                                               | **Mô tả**                                  |
| ----------------------------------------------------------------------------- | ------------------------------------------ |
| `drawRoundRect(left, top, right, bottom, rx, ry, paint)`                      | Vẽ hình chữ nhật với các góc được bo tròn. |
| `drawArc(left, top, right, bottom, startAngle, sweepAngle, useCenter, paint)` | Vẽ một cung tròn hoặc hình quạt.           |
| `drawPoints(floatArray, paint)`                                               | Vẽ một danh sách các điểm từ mảng tọa độ.  |
| `drawPoint(x, y, paint)`                                                      | Vẽ một điểm tại tọa độ `(x, y)`.           |

### **Bitmap**

| **Phương thức**                                                                                | **Mô tả**                                                 |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| `drawBitmap(bitmap, left, top, paint)`                                                         | Vẽ một `Bitmap` tại tọa độ `(left, top)`                  |
| `drawBitmap(bitmap, srcRect, destRect, paint)`                                                 | Vẽ một phần của `Bitmap` từ vùng `srcRect` đến `destRect` |
| `drawBitmapMesh(bitmap, meshWidth, meshHeight, verts, vertOffset, colors, colorOffset, paint)` | Vẽ bitmap với hiệu ứng lưới biến dạng.                    |

### **Văn bản**

| **Phương thức**                                                               | **Mô tả**                                                              |
| ----------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `drawTextOnPath(text, path, hOffset, vOffset, paint)`                         | Vẽ văn bản dọc theo đường dẫn `Path`.                                  |
| `drawTextRun(text, start, end, contextStart, contextEnd, x, y, isRtl, paint)` | Vẽ một đoạn văn bản với nhiều ngữ cảnh hơn (hỗ trợ ngôn ngữ phức tạp). |

### **Đường dẫn (Path)**

| **Phương thức**                                                                                                        | **Mô tả**                                                    |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `drawPath(path, paint)`                                                                                                | Vẽ một hình dựa trên đối tượng `Path`.                       |
| `drawVertices(mode, vertexCount, verts, vertOffset, texs, texOffset, colors, colorOffset, indices, indexCount, paint)` | Vẽ đồ họa dựa trên các đỉnh (vertices) để tạo hình phức tạp. |

### **Hiệu ứng Clip**

| **Phương thức**                                 | **Mô tả**                               |
| ----------------------------------------------- | --------------------------------------- |
| `clipRect(left, top, right, bottom, Region.Op)` | Giới hạn vùng vẽ vào một hình chữ nhật. |
| `clipPath(path, Region.Op)`                     | Giới hạn vùng vẽ dựa trên một `Path`.   |

### **Biến đổi Canvas**

| **Phương thức**           | **Mô tả**                                                          |
| ------------------------- | ------------------------------------------------------------------ |
| `rotate(degrees, px, py)` | Xoay Canvas quanh điểm `(px, py)` với góc `degrees`.               |
| `scale(sx, sy, px, py)`   | Thay đổi tỉ lệ Canvas theo tỷ lệ `(sx, sy)` quanh điểm `(px, py)`. |
| `translate(dx, dy)`       | Dịch chuyển hệ tọa độ gốc của Canvas theo `(dx, dy)`.              |
| `skew(sx, sy)`            | Nghiêng Canvas theo hệ số `sx` và `sy`.                            |

### **Thông tin Canvas**

| **Phương thức**           | **Mô tả**                                                     |
| ------------------------- | ------------------------------------------------------------- |
| `getClipBounds(outRect)`  | Lấy vùng bị cắt (clip bounds) hiện tại của Canvas.            |
| `isHardwareAccelerated()` | Kiểm tra Canvas có đang sử dụng tăng tốc phần cứng hay không. |

# Cách sử dụng

## 1. drawCircle()

- Mô tả: Vẽ một hình tròn.
- Cú pháp:

```
canvas.drawCircle(cx, cy, radius, paint)
```

- Thuộc tính:

  - cx, cy: Tọa độ của tâm hình tròn.
  - radius: Bán kính của hình tròn.
  - paint: Đối tượng Paint xác định màu sắc, độ dày, kiểu nét vẽ của hình tròn.

- Ví dụ:

```kt
val paint = Paint().apply {
    color = Color.RED
    style = Paint.Style.FILL
}

canvas.drawCircle(200f, 200f, 100f, paint)

```

- Kết quả: Vẽ một hình tròn màu đỏ với tâm tại (200, 200) và bán kính 100px.

## 2. drawRect()

- Mô tả: Vẽ một hình chữ nhật.
- Cú pháp:

```kt
canvas.drawRect(left, top, right, bottom, paint)
```

- Thuộc tính:
  - left, top: Tọa độ góc trên bên trái của hình chữ nhật.
  - right, bottom: Tọa độ góc dưới bên phải của hình chữ nhật.
  - paint: Đối tượng Paint xác định màu sắc, độ dày, kiểu nét vẽ của hình chữ nhật.
- Ví dụ:

```kt
val paint = Paint().apply {
    color = Color.BLUE
    style = Paint.Style.FILL
}

canvas.drawRect(50f, 50f, 300f, 300f, paint)

```

- Kết quả: Vẽ một hình tròn màu đỏ với tâm tại (200, 200) và bán kính 100px.

## 3. drawLine()

- Mô tả: Vẽ một đường thẳng giữa hai điểm
- Cú pháp:

```kt
 canvas.drawLine(startX, startY, endX, endY, paint)
```

- Thuộc tính:
  - startX, startY: Tọa độ điểm bắt đầu của đường thẳng.
  - endX, endY: Tọa độ điểm kết thúc của đường thẳng.
  - paint: Đối tượng Paint xác định màu sắc, độ dày, kiểu nét vẽ của đường thẳng.
- Ví dụ:

```kt
 val paint = Paint().apply {
    color = Color.GREEN
    strokeWidth = 5f
}

canvas.drawLine(100f, 100f, 500f, 100f, paint)

```

- Kết quả: Vẽ một đường thẳng màu xanh lá từ (100, 100) đến (500, 100).

## 4. drawOval()

- Mô tả: Vẽ một hình elip.
- Cú pháp:

```kt
 canvas.drawOval(left, top, right, bottom, paint)
```

- Thuộc tính:
  - left, top: Tọa độ góc trên bên trái của hình elip.
  - right, bottom: Tọa độ góc dưới bên phải của hình elip.
  - paint: Đối tượng Paint xác định màu sắc, độ dày, kiểu nét vẽ của hình elip.
- Ví dụ:

```kt
 val paint = Paint().apply {
    color = Color.YELLOW
    style = Paint.Style.FILL
}

canvas.drawOval(100f, 100f, 400f, 300f, paint)

```

- Kết quả: Vẽ một hình elip màu vàng trong vùng (100, 100) và (400, 300).

## 5. drawText()

- Mô tả: Vẽ một đoạn văn bản tại một vị trí cụ thể.
- Cú pháp:

```kt
 canvas.drawText(text, x, y, paint)
```

- Thuộc tính:
  - text: Chuỗi văn bản cần vẽ.
  - x, y: Tọa độ điểm bắt đầu của văn bản (góc dưới bên trái của chữ cái đầu tiên).
  - paint: Đối tượng Paint xác định màu sắc, kích thước font chữ, độ dày của chữ
- Ví dụ:

```kt
val paint = Paint().apply {
    color = Color.BLACK
    textSize = 50f
}

canvas.drawText("Hello, Canvas!", 100f, 200f, paint)


```

- Kết quả: Vẽ văn bản "Hello, Canvas!" tại tọa độ (100, 200).

## 6. drawBitmap()

- Mô tả: Vẽ một hình ảnh (Bitmap) tại một vị trí cụ thể.

- Cú pháp:

```kt
canvas.drawBitmap(bitmap, left, top, paint)
```

- Thuộc tính:
  - bitmap: Hình ảnh (Bitmap) cần vẽ.
  - left, top: Tọa độ góc trên bên trái của vị trí vẽ.
  - paint: Đối tượng Paint có thể sử dụng để áp dụng hiệu ứng cho Bitmap (tùy chọn).
- Ví dụ:

```kt
val bitmap = BitmapFactory.decodeResource(resources, R.drawable.sample_image)
canvas.drawBitmap(bitmap, 50f, 50f, null)

```

- Kết quả: Vẽ hình ảnh sample_image tại tọa độ (50, 50).

## 7. drawPath()

- Mô tả: Vẽ một hình vẽ dựa trên đối tượng Path.

- Cú pháp:

```kt
canvas.drawPath(path, paint)
```

- Thuộc tính:

* path: Đối tượng Path xác định hình dạng của hình vẽ.
* paint: Đối tượng Paint xác định màu sắc, độ dày, kiểu nét vẽ của đường dẫn.

- Ví dụ:

```kt
val path = Path().apply {
    moveTo(100f, 100f)
    lineTo(200f, 200f)
    lineTo(300f, 100f)
    close()
}

val paint = Paint().apply {
    color = Color.RED
    strokeWidth = 5f
    style = Paint.Style.STROKE
}

canvas.drawPath(path, paint)


```

- Kết quả: Vẽ một hình tam giác với các góc tại (100, 100), (200, 200), và (300, 100).

## Sử dụng cơ bản

### 1. Tạo Custom View

Tạo một lớp kế thừa `View` hoặc `SurfaceView` để vẽ lên Canvas.

```kotlin
class CustomView(context: Context, attrs: AttributeSet?) : View(context, attrs) {
    private val paint = Paint().apply {
        color = Color.BLUE
        style = Paint.Style.FILL
        strokeWidth = 8f
    }

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)

        // Vẽ hình tròn
        canvas.drawCircle(200f, 200f, 100f, paint)

        // Vẽ hình chữ nhật
        paint.color = Color.RED
        canvas.drawRect(100f, 400f, 300f, 600f, paint)

        // Vẽ đường thẳng
        paint.color = Color.GREEN
        paint.strokeWidth = 5f
        canvas.drawLine(50f, 50f, 400f, 50f, paint)

        // Vẽ text
        paint.color = Color.BLACK
        paint.textSize = 40f
        canvas.drawText("Hello Canvas", 50f, 700f, paint)
    }
}

```

### 2. Tạo một đồng hồ analog tùy chỉnh:

```kt
class ClockView(context: Context, attrs: AttributeSet?) : View(context, attrs) {
    private val paint = Paint(Paint.ANTI_ALIAS_FLAG)

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)

        val cx = width / 2f
        val cy = height / 2f
        val radius = minOf(cx, cy) - 20

        // Vẽ mặt đồng hồ
        paint.color = Color.WHITE
        paint.style = Paint.Style.FILL
        canvas.drawCircle(cx, cy, radius, paint)

        // Vẽ viền
        paint.color = Color.BLACK
        paint.style = Paint.Style.STROKE
        paint.strokeWidth = 8f
        canvas.drawCircle(cx, cy, radius, paint)

        // Vẽ kim phút
        paint.strokeWidth = 6f
        canvas.save()
        canvas.rotate(90f, cx, cy)  // Xoay 90 độ
        canvas.drawLine(cx, cy, cx, cy - radius + 30, paint)
        canvas.restore()

        // Vẽ kim giờ
        paint.strokeWidth = 10f
        canvas.save()
        canvas.rotate(45f, cx, cy)  // Xoay 45 độ
        canvas.drawLine(cx, cy, cx, cy - radius + 50, paint)
        canvas.restore()
    }
}

```
