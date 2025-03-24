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


بله، حتماً! بیایید یک مثال دنیای واقعی بهتر برای **Factory Pattern** ارائه دهیم که کاربرد عملی‌تری داشته باشد.

---

## **پترن Factory Pattern در دنیای واقعی: سیستم مدیریت پیام‌رسانی**

### **سناریوی واقعی**
فرض کنید در یک شرکت، نیاز دارید یک سیستم مدیریت پیام‌رسانی طراحی کنید. این سیستم باید بتواند پیام‌ها را از طریق چندین کانال مختلف ارسال کند، مانند:
1. **ایمیل**
2. **پیامک (SMS)**
3. **اعلان پوش (Push Notification)**

هر کانال ارسال پیام دارای ویژگی‌ها و نحوه عملکرد متفاوتی است. با استفاده از **Factory Pattern**، می‌توانید یک کارخانه طراحی کنید که بسته به نوع کانال درخواستی، پیام را از طریق کانال مناسب ارسال کند.

---

### **پیاده‌سازی Factory Pattern در TypeScript**

```typescript
// Interface برای ارسال پیام
interface MessageSender {
    send(message: string): void;
}

// پیاده‌سازی ارسال ایمیل
class EmailSender implements MessageSender {
    send(message: string): void {
        console.log(`Sending email: ${message}`);
    }
}

// پیاده‌سازی ارسال پیامک (SMS)
class SmsSender implements MessageSender {
    send(message: string): void {
        console.log(`Sending SMS: ${message}`);
    }
}

// پیاده‌سازی ارسال اعلان پوش (Push Notification)
class PushNotificationSender implements MessageSender {
    send(message: string): void {
        console.log(`Sending push notification: ${message}`);
    }
}

// کارخانه برای ایجاد کانال‌های ارسال پیام
class MessageSenderFactory {
    createSender(type: string): MessageSender {
        switch (type) {
            case "email":
                return new EmailSender();
            case "sms":
                return new SmsSender();
            case "push":
                return new PushNotificationSender();
            default:
                throw new Error("Invalid sender type.");
        }
    }
}

// استفاده
const factory = new MessageSenderFactory();

// ارسال پیام از طریق ایمیل
const emailSender = factory.createSender("email");
emailSender.send("Hello via email!");

// ارسال پیام از طریق پیامک
const smsSender = factory.createSender("sms");
smsSender.send("Hello via SMS!");

// ارسال پیام از طریق اعلان پوش
const pushSender = factory.createSender("push");
pushSender.send("Hello via push notification!");
```

---

### **خروجی کد**
وقتی کد بالا اجرا شود، خروجی به صورت زیر خواهد بود:

```
Sending email: Hello via email!
Sending SMS: Hello via SMS!
Sending push notification: Hello via push notification!
```

---

### **چطور این الگو به حل مسئله کمک می‌کند؟**
1. **مدیریت کانال‌های مختلف**: این الگو به شما کمک می‌کند که کانال‌های مختلف ارسال پیام را به صورت یکپارچه مدیریت کنید.
2. **افزایش انعطاف‌پذیری**: اگر بخواهید کانال جدیدی اضافه کنید (مثلاً ارسال پیام از طریق شبکه‌های اجتماعی)، فقط کافی است یک کلاس جدید پیاده‌سازی کنید و آن را در Factory اضافه کنید. بقیه کد بدون تغییر باقی می‌ماند.
3. **جدا کردن منطق ایجاد اشیاء**: مشابه قبل، منطق ایجاد کانال‌ها از بخش‌های دیگر کد جدا می‌شود.

---

### **نکات مهم برای استفاده در دنیای واقعی**
- **استفاده در سیستم‌های پیچیده**: این الگو برای سیستم‌هایی که نیاز به مدیریت چندین نوع کانال یا سرویس دارند، ایده‌آل است.
- **افزایش قابلیت توسعه**: اضافه کردن کانال جدید بدون تغییر در کد موجود امکان‌پذیر است.

---
