

## **الگوی چهارم Builder Pattern**

### **تعریف Builder Pattern**
این الگو به شما کمک می‌کند تا اشیاء پیچیده را به صورت مرحله‌ای بسازید. به جای استفاده از یک سازنده (Constructor) طولانی و پیچیده، از یک **Builder** استفاده می‌کنید که مسئولیت تنظیم هر بخش از شیء را بر عهده دارد.

---

### **مثال اول: ساخت یک کامپیوتر با Builder Pattern**

فرض کنید می‌خواهید یک کامپیوتر شخصی (PC) بسازید. یک کامپیوتر شامل قطعات مختلفی مانند **CPU**، **RAM**، **Hard Drive**، و **GPU** است. با استفاده از Builder Pattern، می‌توانید فرآیند ساخت کامپیوتر را به صورت مرحله‌ای مدیریت کنید.

#### **پیاده‌سازی در TypeScript**

```typescript
class Computer {
    private cpu: string = "";
    private ram: string = "";
    private hardDrive: string = "";
    private gpu: string = "";

    setCPU(cpu: string): void {
        this.cpu = cpu;
    }

    setRAM(ram: string): void {
        this.ram = ram;
    }

    setHardDrive(hardDrive: string): void {
        this.hardDrive = hardDrive;
    }

    setGPU(gpu: string): void {
        this.gpu = gpu;
    }

    showSpecs(): void {
        console.log(`Computer Specs:
            CPU: ${this.cpu}
            RAM: ${this.ram}
            Hard Drive: ${this.hardDrive}
            GPU: ${this.gpu}`);
    }
}

// Builder برای ساخت کامپیوتر
class ComputerBuilder {
    private computer: Computer;

    constructor() {
        this.computer = new Computer();
    }

    addCPU(cpu: string): ComputerBuilder {
        this.computer.setCPU(cpu);
        return this;
    }

    addRAM(ram: string): ComputerBuilder {
        this.computer.setRAM(ram);
        return this;
    }

    addHardDrive(hardDrive: string): ComputerBuilder {
        this.computer.setHardDrive(hardDrive);
        return this;
    }

    addGPU(gpu: string): ComputerBuilder {
        this.computer.setGPU(gpu);
        return this;
    }

    build(): Computer {
        return this.computer;
    }
}

// استفاده
const builder = new ComputerBuilder();
const myComputer = builder
    .addCPU("Intel i9")
    .addRAM("32GB DDR5")
    .addHardDrive("1TB SSD")
    .addGPU("NVIDIA RTX 4090")
    .build();

myComputer.showSpecs();
```

#### **خروجی کد**
```
Computer Specs:
    CPU: Intel i9
    RAM: 32GB DDR5
    Hard Drive: 1TB SSD
    GPU: NVIDIA RTX 4090
```

---

### **مثال دوم (دنیای واقعی): ساخت یک همبرگر با Builder Pattern**

فرض کنید در یک رستوران زنجیره‌ای، مشتریان می‌توانند همبرگرهای سفارشی بسازند. یک همبرگر شامل بخش‌های مختلفی مانند **نان**، **گوشت**، **سبزیجات**، و **سس** است. با استفاده از Builder Pattern، می‌توانید فرآیند ساخت همبرگر را به صورت مرحله‌ای مدیریت کنید.

#### **پیاده‌سازی در TypeScript**

```typescript
class Burger {
    private bun: string = "";
    private patty: string = "";
    private vegetables: string[] = [];
    private sauces: string[] = [];

    setBun(bun: string): void {
        this.bun = bun;
    }

    setPatty(patty: string): void {
        this.patty = patty;
    }

    addVegetable(vegetable: string): void {
        this.vegetables.push(vegetable);
    }

    addSauce(sauce: string): void {
        this.sauces.push(sauce);
    }

    showDetails(): void {
        console.log(`Burger Details:
            Bun: ${this.bun}
            Patty: ${this.patty}
            Vegetables: ${this.vegetables.join(", ")}
            Sauces: ${this.sauces.join(", ")}`);
    }
}

// Builder برای ساخت همبرگر
class BurgerBuilder {
    private burger: Burger;

    constructor() {
        this.burger = new Burger();
    }

    addBun(bun: string): BurgerBuilder {
        this.burger.setBun(bun);
        return this;
    }

    addPatty(patty: string): BurgerBuilder {
        this.burger.setPatty(patty);
        return this;
    }

    addVegetable(vegetable: string): BurgerBuilder {
        this.burger.addVegetable(vegetable);
        return this;
    }

    addSauce(sauce: string): BurgerBuilder {
        this.burger.addSauce(sauce);
        return this;
    }

    build(): Burger {
        return this.burger;
    }
}

// استفاده
const builder = new BurgerBuilder();
const myBurger = builder
    .addBun("Sesame Seed Bun")
    .addPatty("Beef Patty")
    .addVegetable("Lettuce")
    .addVegetable("Tomato")
    .addSauce("Ketchup")
    .addSauce("Mayonnaise")
    .build();

myBurger.showDetails();
```

#### **خروجی کد**
```
Burger Details:
    Bun: Sesame Seed Bun
    Patty: Beef Patty
    Vegetables: Lettuce, Tomato
    Sauces: Ketchup, Mayonnaise
```

---

### **چطور این الگو به حل مسئله کمک می‌کند؟**
1. **مدیریت ساخت اشیاء پیچیده**: این الگو به شما کمک می‌کند که فرآیند ساخت اشیاء پیچیده را به صورت مرحله‌ای مدیریت کنید.
2. **افزایش انعطاف‌پذیری**: می‌توانید اجزای مختلف را به صورت جداگانه تنظیم کنید و ساخت را سفارشی‌سازی کنید.
3. **جدا کردن منطق ساخت**: منطق ساخت از نمایش یا استفاده از شیء جدا می‌شود.

---

### **نکات مهم برای استفاده در دنیای واقعی**
- **استفاده در سیستم‌های پیچیده**: این الگو برای سیستم‌هایی که نیاز به ساخت اشیاء پیچیده دارند (مثل کامپیوترها، خودروها، یا همبرگرها)، ایده‌آل است.
- **افزایش قابلیت توسعه**: اضافه کردن ویژگی‌های جدید بدون تغییر در کد موجود امکان‌پذیر است.

---

بله، حتماً! یک مثال کاربردی و مرتبط با **مهندسی نرم‌افزار** برای **Builder Pattern** این است که فرض کنید در حال توسعه یک سیستم مدیریت API هستید. این سیستم باید درخواست‌های HTTP پیچیده (مثل GET، POST، PUT و DELETE) را با تنظیمات مختلف مانند **Headers**، **Query Parameters**، **Body** و **Authentication** بسازد. 

---

## **مثال: ساخت درخواست HTTP با Builder Pattern**

### **سناریوی واقعی**
فرض کنید در یک پروژه نرم‌افزاری، نیاز دارید یک کتابخانه برای ارسال درخواست‌های HTTP طراحی کنید. هر درخواست HTTP می‌تواند شامل اجزای مختلفی باشد:
1. **URL**: آدرس مقصد
2. **Method**: نوع درخواست (GET, POST, PUT, DELETE)
3. **Headers**: سربرگ‌های HTTP (مثل `Content-Type`, `Authorization`)
4. **Query Parameters**: پارامترهای موجود در URL
5. **Body**: داده‌های ارسالی در بدنه درخواست

با استفاده از **Builder Pattern**، می‌توانید فرآیند ساخت درخواست HTTP را به صورت مرحله‌ای و انعطاف‌پذیر مدیریت کنید.

---

### **پیاده‌سازی در TypeScript**

```typescript
class HttpRequest {
    private url: string = "";
    private method: string = "GET";
    private headers: { [key: string]: string } = {};
    private queryParams: { [key: string]: string } = {};
    private body: any = null;

    setUrl(url: string): void {
        this.url = url;
    }

    setMethod(method: string): void {
        this.method = method;
    }

    addHeader(key: string, value: string): void {
        this.headers[key] = value;
    }

    addQueryParam(key: string, value: string): void {
        this.queryParams[key] = value;
    }

    setBody(body: any): void {
        this.body = body;
    }

    send(): void {
        console.log(`Sending ${this.method} request to ${this.url}`);
        console.log("Headers:", this.headers);
        console.log("Query Params:", this.queryParams);
        console.log("Body:", this.body);
    }
}

// Builder برای ساخت درخواست HTTP
class HttpRequestBuilder {
    private request: HttpRequest;

    constructor() {
        this.request = new HttpRequest();
    }

    setUrl(url: string): HttpRequestBuilder {
        this.request.setUrl(url);
        return this;
    }

    setMethod(method: string): HttpRequestBuilder {
        this.request.setMethod(method);
        return this;
    }

    addHeader(key: string, value: string): HttpRequestBuilder {
        this.request.addHeader(key, value);
        return this;
    }

    addQueryParam(key: string, value: string): HttpRequestBuilder {
        this.request.addQueryParam(key, value);
        return this;
    }

    setBody(body: any): HttpRequestBuilder {
        this.request.setBody(body);
        return this;
    }

    build(): HttpRequest {
        return this.request;
    }
}

// استفاده
const builder = new HttpRequestBuilder();
const request = builder
    .setUrl("https://api.example.com/data")
    .setMethod("POST")
    .addHeader("Content-Type", "application/json")
    .addHeader("Authorization", "Bearer token123")
    .addQueryParam("page", "1")
    .addQueryParam("limit", "10")
    .setBody({ name: "John Doe", age: 30 })
    .build();

request.send();
```

---

### **خروجی کد**
```
Sending POST request to https://api.example.com/data
Headers: { 'Content-Type': 'application/json', Authorization: 'Bearer token123' }
Query Params: { page: '1', limit: '10' }
Body: { name: 'John Doe', age: 30 }
```

---

### **چطور این الگو به حل مسئله کمک می‌کند؟**
1. **مدیریت درخواست‌های پیچیده**: این الگو به شما کمک می‌کند که فرآیند ساخت درخواست‌های HTTP را به صورت مرحله‌ای و سازمان‌یافته مدیریت کنید.
2. **افزایش انعطاف‌پذیری**: می‌توانید اجزای مختلف درخواست را به صورت جداگانه تنظیم کنید و ساخت را سفارشی‌سازی کنید.
3. **جدا کردن منطق ساخت**: منطق ساخت درخواست از اجرای آن (ارسال) جدا می‌شود، بنابراین کد تمیزتر و قابل نگهداری‌تر است.
