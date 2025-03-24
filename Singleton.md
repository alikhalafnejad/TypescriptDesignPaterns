
## **شروع از اولین الگو: Singleton Pattern**

### **تعریف Singleton Pattern**
این الگو اطمینان می‌دهد که فقط یک نمونه از یک کلاس وجود داشته باشد و یک نقطه دسترسی جهانی به آن فراهم کند.

### **کاربرد در دنیای واقعی**
فرض کنید می‌خواهید یک **Database Connection Manager** بسازید. اتصال به پایگاه داده معمولاً منابع زیادی مصرف می‌کند، بنابراین ایجاد چندین نمونه از اتصال به پایگاه داده می‌تواند باعث افزایش هزینه و کاهش عملکرد شود. با استفاده از الگوی Singleton، می‌توانید اطمینان حاصل کنید که فقط یک اتصال به پایگاه داده وجود دارد.

---

### **پیاده‌سازی Singleton Pattern در TypeScript**

```typescript
class DatabaseConnection {
    private static instance: DatabaseConnection;

    private constructor() {
        // مخفی کردن سازنده
        console.log("Database connection established.");
    }

    public static getInstance(): DatabaseConnection {
        if (!DatabaseConnection.instance) {
            DatabaseConnection.instance = new DatabaseConnection();
        }
        return DatabaseConnection.instance;
    }

    public query(sql: string): void {
        console.log(`Executing query: ${sql}`);
    }
}

// استفاده
const db1 = DatabaseConnection.getInstance();
db1.query("SELECT * FROM users");

const db2 = DatabaseConnection.getInstance();
console.log(db1 === db2); // true (هر دو به یک نمونه اشاره دارند)
```

---

### **چطور این الگو به حل مسئله کمک می‌کند؟**
1. **مدیریت منابع**: با اطمینان از اینکه فقط یک نمونه از اتصال به پایگاه داده وجود دارد، از افزایش بی‌رویه منابع جلوگیری می‌کنید.
2. **کنترل دسترسی**: همه قسمت‌های برنامه از طریق یک نمونه واحد به پایگاه داده دسترسی دارند، بنابراین مدیریت و نگهداری آسان‌تر است.
3. **جلوگیری از تداخل**: از ایجاد مشکلاتی مانند تداخل در اتصالات یا ناسازگاری داده‌ها جلوگیری می‌کنید.

---

### **نکات مهم برای استفاده در دنیای واقعی**
- **استفاده از Singleton با احتیاط**: این الگو می‌تواند باعث ایجاد **Global State** شود که ممکن است تست و نگهداری کد را سخت‌تر کند.
- **جایگزین‌ها**: در برخی موارد، استفاده از وابستگی‌های تزریقی (Dependency Injection) می‌تواند جایگزین بهتری برای Singleton باشد.

---
