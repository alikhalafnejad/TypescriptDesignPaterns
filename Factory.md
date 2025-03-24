## **الگوی دوم: Factory Pattern (الگوی کارخانه)**

### **تعریف Factory Pattern**
این الگو به شما کمک می‌کند تا اشیاء را بدون مشخص کردن کلاس دقیق آنها ایجاد کنید. به عبارت دیگر، شما یک **Factory** (کارخانه) دارید که مسئولیت ایجاد اشیاء را بر عهده دارد.

### **کاربرد در دنیای واقعی**
فرض کنید در یک سیستم مدیریت محصولات، انواع مختلفی از محصولات وجود دارد، مانند **لپ‌تاپ**، **موبایل**، و **هدفون**. هر محصول دارای ویژگی‌ها و رفتارهای متفاوتی است. با استفاده از الگوی Factory، می‌توانید یک کارخانه طراحی کنید که بسته به نوع درخواست، محصول مناسب را ایجاد کند.

---

### **پیاده‌سازی Factory Pattern در TypeScript**

```typescript
// Interface برای محصولات
interface Product {
    use(): void;
}

// کلاس‌های پیاده‌سازی محصولات
class Laptop implements Product {
    use() {
        console.log("Laptop is being used.");
    }
}

class Mobile implements Product {
    use() {
        console.log("Mobile is being used.");
    }
}

class Headphone implements Product {
    use() {
        console.log("Headphone is being used.");
    }
}

// کارخانه برای ایجاد محصولات
class ProductFactory {
    createProduct(type: string): Product {
        switch (type) {
            case "laptop":
                return new Laptop();
            case "mobile":
                return new Mobile();
            case "headphone":
                return new Headphone();
            default:
                throw new Error("Invalid product type.");
        }
    }
}

// استفاده
const factory = new ProductFactory();
const laptop = factory.createProduct("laptop");
laptop.use(); // Laptop is being used.

const mobile = factory.createProduct("mobile");
mobile.use(); // Mobile is being used.
```

---

### **چطور این الگو به حل مسئله کمک می‌کند؟**
1. **جدا کردن منطق ایجاد اشیاء**: با استفاده از Factory، منطق ایجاد اشیاء از بخش‌های دیگر کد جدا می‌شود. این کار باعث می‌شود کد تمیزتر و قابل نگهداری‌تر شود.
2. **افزایش انعطاف‌پذیری**: اگر بخواهید محصول جدیدی اضافه کنید، فقط کافی است یک کلاس جدید پیاده‌سازی کنید و آن را در Factory اضافه کنید. بقیه کد بدون تغییر باقی می‌ماند.
3. **کاهش وابستگی‌ها**: کلاس‌هایی که محصولات را استفاده می‌کنند، مستقیماً به کلاس‌های محصول وابسته نیستند و فقط با Factory تعامل دارند.

---

### **مثال دنیای واقعی: سیستم مدیریت حمل‌ونقل**
فرض کنید در یک شرکت حمل‌ونقل، انواع مختلفی از وسایل نقلیه وجود دارد، مانند **کامیون**، **ماشین**، و **موتورسیکلت**. هر وسیله نقلیه دارای ویژگی‌ها و عملکردهای متفاوتی است. با استفاده از Factory Pattern، می‌توانید یک کارخانه طراحی کنید که بسته به نوع درخواست، وسیله نقلیه مناسب را ایجاد کند.

---

### **نکات مهم برای استفاده در دنیای واقعی**
- **استفاده از Factory برای مدیریت پیچیدگی**: وقتی تعداد زیادی کلاس دارید که اشیاء مشابه ایجاد می‌کنند، Factory می‌تواند کد را ساده‌تر کند.
- **Abstract Factory**: اگر نیاز دارید چندین Factory برای خانواده‌ای از محصولات ایجاد کنید، می‌توانید از **Abstract Factory Pattern** استفاده کنید.
