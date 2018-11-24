## Angular Cli command

ติดตั้ง CLI ด้วย npm package manager เรียกใช้ online help สามารถเรียกได้จาก command line และสามารถเรียกดู options ขอแต่ละ command เช่น `ng generate --help`

```
npm install -g @angular/cli
ng help
ng generate --help
```

สร้าง Project ด้วย คำสั่ง `ng new` และ run ด้วย คำสั่ง  `ng serve`  และเปิด browser ไปที่  `localhost:4200`

```
ng new  my-first-project
cd my-first-project
ng serve
```

workspace configuration คือ angular.json จะถูกสร้าง ในระดับ top level ของ project [https://github.com/angular/angular-cli/wiki/angular-workspace](https://github.com/angular/angular-cli/wiki/angular-workspace)

#### คำสั่ง ng generate \( alias ng g\)

ทำหน้า generate หรือ modify files ด้วยอ้างอิงจาก schema ![](/assets/schema.png)

format

```
ng generate <schematic> [options]
ng g <schematic> [options]
```



