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

format [https://angular.io/cli/generate](https://angular.io/cli/generate)

```
ng generate <schematic> [options]
ng g <schematic> [options]
```

ต้วอย่าง  workflow สร้าง modules เพื่อ รองรับรับ component

```
ng new hrms
cd hrms
ng g m employees --module=app.module --spec=false
```

##### อะไรคือ AppModule

* AppModule คือ Root module  ที่ทำหน้าที่ bootstrap และ launchs angular application
* Angular  มีลักษณะเป็น Component base framework   Component ทำหน้าที่เป็น Building Block application เพื่อให้สามารถนำ code กลับมาใช้งานได้ใหม่ ประกอบด้วย
  * Class และ มีการ exports เพื่อให้สามารถเรียกใช้งานจาก component อื่น
  * Decorator มีอยู่ 4 ชนิด เพื่อ เพิ่ม function
    * Class decorators  เช่น @NgModule, @NgComponent,  @Directive
    * Property Decorator เช่น @Input, @Output
    * Method Decorator เช่น @HostListener
    * Parameter Decorator เช่น @Inject

 



