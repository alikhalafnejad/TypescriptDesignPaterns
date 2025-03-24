
## **Abstract Factory Pattern**

### **تعریف Abstract Factory Pattern**
این الگو به شما کمک می‌کند تا خانواده‌ای از محصولات مرتبط را بدون مشخص کردن کلاس‌های دقیق آنها ایجاد کنید. به عبارت دیگر، یک **Factory انتزاعی** (Abstract Factory) دارید که مسئولیت ایجاد چندین نوع محصول مرتبط را بر عهده دارد.

### **تفاوت با Factory Pattern**
- **Factory Pattern**: یک کارخانه ساده است که یک نوع محصول ایجاد می‌کند.
- **Abstract Factory Pattern**: یک کارخانه انتزاعی است که خانواده‌ای از محصولات مرتبط را ایجاد می‌کند.

---

### **کاربرد در دنیای واقعی**
فرض کنید در یک شرکت تولید مبلمان، دو خط تولید وجود دارد:  
1. **مبلمان کلاسیک**  
2. **مبلمان مدرن**  

هر خط تولید شامل چندین محصول مرتبط است، مانند **صندلی**، **میز**، و **کاناپه**. با استفاده از **Abstract Factory Pattern**، می‌توانید یک کارخانه انتزاعی طراحی کنید که بسته به نوع درخواست، خانواده‌ای از محصولات مرتبط (کلاسیک یا مدرن) را ایجاد کند.

---

### **پیاده‌سازی Abstract Factory Pattern در TypeScript**

```typescript
// Interfaces برای محصولات
interface Chair {
    sitOn(): void;
}

interface Table {
    placeItems(): void;
}

// پیاده‌سازی محصولات کلاسیک
class ClassicChair implements Chair {
    sitOn() {
        console.log("Sitting on a classic chair.");
    }
}

class ClassicTable implements Table {
    placeItems() {
        console.log("Placing items on a classic table.");
    }
}

// پیاده‌سازی محصولات مدرن
class ModernChair implements Chair {
    sitOn() {
        console.log("Sitting on a modern chair.");
    }
}

class ModernTable implements Table {
    placeItems() {
        console.log("Placing items on a modern table.");
    }
}

// Abstract Factory
interface FurnitureFactory {
    createChair(): Chair;
    createTable(): Table;
}

// پیاده‌سازی کارخانه‌های خاص
class ClassicFurnitureFactory implements FurnitureFactory {
    createChair(): Chair {
        return new ClassicChair();
    }

    createTable(): Table {
        return new ClassicTable();
    }
}

class ModernFurnitureFactory implements FurnitureFactory {
    createChair(): Chair {
        return new ModernChair();
    }

    createTable(): Table {
        return new ModernTable();
    }
}

// استفاده
function clientCode(factory: FurnitureFactory) {
    const chair = factory.createChair();
    const table = factory.createTable();

    chair.sitOn();
    table.placeItems();
}

// ایجاد مبلمان کلاسیک
const classicFactory = new ClassicFurnitureFactory();
clientCode(classicFactory);

// ایجاد مبلمان مدرن
const modernFactory = new ModernFurnitureFactory();
clientCode(modernFactory);
```

---

### **چطور این الگو به حل مسئله کمک می‌کند؟**
1. **مدیریت خانواده‌ای از محصولات**: این الگو به شما کمک می‌کند که خانواده‌ای از محصولات مرتبط را به صورت یکپارچه مدیریت کنید.
2. **افزایش انعطاف‌پذیری**: اگر بخواهید خط تولید جدیدی اضافه کنید، فقط کافی است یک کارخانه جدید و محصولات مرتبط آن را پیاده‌سازی کنید. بقیه کد بدون تغییر باقی می‌ماند.
3. **جدا کردن منطق ایجاد اشیاء**: مشابه Factory Pattern، منطق ایجاد اشیاء از بخش‌های دیگر کد جدا می‌شود.

---

### **مثال دنیای واقعی: سیستم مدیریت UI**
فرض کنید در یک برنامه وب، دو نوع رابط کاربری وجود دارد:  
1. **Light Theme**  
2. **Dark Theme**  

هر رابط کاربری شامل چندین عنصر مرتبط است، مانند **دکمه**، **فیلد ورودی**، و **منو**. با استفاده از Abstract Factory Pattern، می‌توانید یک کارخانه انتزاعی طراحی کنید که بسته به نوع تم (Light یا Dark)، خانواده‌ای از عناصر مرتبط را ایجاد کند.

---

### **نکات مهم برای استفاده در دنیای واقعی**
- **استفاده در سیستم‌های پیچیده**: این الگو برای سیستم‌هایی که نیاز به مدیریت خانواده‌ای از محصولات مرتبط دارند، ایده‌آل است.
- **افزایش قابلیت توسعه**: اضافه کردن خط تولید جدید (یا تم جدید) بدون تغییر در کد موجود امکان‌پذیر است.
