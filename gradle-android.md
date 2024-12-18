# Gradle trong dự án Android

## Gradle là gì?

- Gradle là một hệ thống build mã nguồn mở dựa trên Java và Groovy/Kotlin DSL (Domain Specific Language), hỗ trợ:

- Tự động hóa các tác vụ build (biên dịch mã, đóng gói ứng dụng, tạo tệp APK/AAB).
- Quản lý phụ thuộc (dependencies) trong dự án.
- Tùy chỉnh các quy trình build bằng cách viết script trong build.gradle.

## Cấu trúc Gradle trong dự án Android

- Khi tạo một dự án Android, bạn sẽ thấy 2 tệp Gradle chính:

  - build.gradle (project-level): Áp dụng cho toàn bộ dự án.
  - build.gradle (module-level): Áp dụng cho từng module (thường là app module).

### Tệp Gradle cấp dự án

- Tệp này nằm ở gốc của dự án, quản lý các cấu hình chung như:
  - Các repository dùng để tải dependencies.
  - Các plugin áp dụng cho dự án.

```
// build.gradle (Project Level)
buildscript {
    repositories {
        google() // Repository của Google
        mavenCentral() // Repository Maven Central
    }
    dependencies {
        classpath "com.android.tools.build:gradle:8.0.0" // Plugin Android Gradle
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.9.10" // Plugin Kotlin
    }
}

```

### Tệp Gradle cấp module

- Tệp này nằm trong từng module (thường là app), quản lý:
  - Cấu hình build cho từng module.
  - Quản lý dependencies (thư viện, plugin).

```
// build.gradle (Module Level)
plugins {
    id 'com.android.application' // Plugin ứng dụng Android
    id 'org.jetbrains.kotlin.android' // Plugin Kotlin cho Android
}

android {
    compileSdk = 33 // Phiên bản SDK để biên dịch ứng dụng

    defaultConfig {
        applicationId "com.example.myapp" // ID của ứng dụng
        minSdk = 21 // Phiên bản SDK tối thiểu
        targetSdk = 33 // Phiên bản SDK mục tiêu
        versionCode = 1 // Mã phiên bản
        versionName = "1.0" // Tên phiên bản
    }

    buildTypes {
        release {
            minifyEnabled false // Tắt R8/Proguard để nén mã
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation "androidx.core:core-ktx:1.9.0" // Thư viện AndroidX Core
    implementation "androidx.appcompat:appcompat:1.5.1"
    implementation "com.google.android.material:material:1.7.0"
}

```

## Các thành phần quan trọng của Gradle

1. Plugin

- Gradle sử dụng plugin để mở rộng chức năng. Các plugin phổ biến:

  1. Android Plugin:
     - com.android.application: Xây dựng ứng dụng Android.
     - com.android.library: Xây dựng thư viện Android.
  2. Kotlin Plugin:
     -org.jetbrains.kotlin.android: Hỗ trợ lập trình Kotlin trên Android.

```
plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
}

```

2. Build Types

- Quản lý các cấu hình build như debug và release.

  - Debug: Thường dùng trong quá trình phát triển (có thêm log, không nén mã).
  - Release: Đóng gói cuối cùng để phát hành (nén mã, ký ứng dụng).

```
android {
    buildTypes {
        debug {
            applicationIdSuffix ".debug"
            versionNameSuffix "-DEBUG"
        }
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

```

3. Flavors

- Build Flavors cho phép tạo nhiều phiên bản ứng dụng từ một mã nguồn, ví dụ: miễn phí và trả phí.

```
android {
    flavorDimensions "version"
    productFlavors {
        free {
            applicationId "com.example.myapp.free"
            versionNameSuffix "-FREE"
        }
        paid {
            applicationId "com.example.myapp.paid"
            versionNameSuffix "-PAID"
        }
    }
}

```

4. Dependencies (Phụ thuộc)

- Phụ thuộc là các thư viện hoặc module mà ứng dụng sử dụng.
- Các loại dependencies:
  - implementation: Chỉ khả dụng cho module này.
  - api: Khả dụng cho module này và các module khác phụ thuộc vào nó.
  - testImplementation: Dùng cho testing.

5.  Gradle Wrapper

- Gradle Wrapper giúp đảm bảo sử dụng đúng phiên bản Gradle cho mọi dự án, bất kể máy tính của bạn có cài đặt Gradle hay không.

- Cấu hình trong gradle-wrapper.properties:

```
distributionUrl=https\://services.gradle.org/distributions/gradle-8.0-bin.zip

```

## Cách chạy Gradle

Gradle hỗ trợ chạy các tác vụ (task) từ dòng lệnh hoặc Android Studio.

- Chạy từ dòng lệnh:

```
./gradlew assembleDebug       # Build APK debug
./gradlew assembleRelease     # Build APK release
./gradlew clean               # Xóa build cũ

```

- Chạy từ Android Studio:
