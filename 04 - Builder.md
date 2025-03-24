

## ***الگوی چهارم Builder Pattern**

### **تعریف Builder Pattern**
این الگو به شما کمک می‌کند تا اشیاء پیچیده را به صورت مرحله‌ای بسازید. به جای استفاده از یک سازنده (Constructor) طولانی و پیچیده، از یک **Builder** استفاده می‌کنید که مسئولیت تنظیم هر بخش از شیء را بر عهده دارد.

---

### **مثال اول: ساخت یک کامپیوتر با Builder Pattern**

فرض کنید می‌خواهید یک کامپیوتر شخصی (PC) بسازید. یک کامپیوتر شامل قطعات مختلفی مانند **CPU**، **RAM**، **Hard Drive**، و **GPU** است. با استفاده از Builder Pattern، می‌توانید فرآیند ساخت کامپیوتر را به صورت مرحله‌ای مدیریت کنید.

#### **پیاده‌سازی در TypeScript**

```typescript
// کلاس کامپیوتر
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
// کلاس همبرگر
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
