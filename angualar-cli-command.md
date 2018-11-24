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

แต่ละ decorator จะมี basic configuration ด้วยกำหนด  properties เช่น

* Selector เป็นการเรียกใช้ Component จาก Template
* Template เป็นการกำหนด html template inline ใน view
* TemplateUrl  เป็นการกำหนด URL ของ External file สำหรับ template
* Styles กำหนด CSS แบบ inline 
* Styles กำหนด CSS แบบ External file
* viewProviders  เป็นการระบุ List of providers ทำ component สามารถเรียกใช้งานได้

#### Angular Module

เราสามารถแบ่ง Angular Application ออกเป็น Module ย่อยๆๆ การใช้ @NgModule  แต่ละ Module สามารถ contain Components , Service providers และ code อื่นๆ

แต่ละ Angular App จะต้องมี root module ชื่อว่า AppModule อยู่ใน file app.module.ts  ทำหน้าที่ lauch

##### NgModule metadata

* declarations เป็นการประกาศว่า components, directives, pips ที่ เป็นของ NgModule
* exports เป็น subset ของ declarations ที่จะบอกว่า components ได้ สามารถมองเป็นจาก component templates ของ ngModules
* imports เป็นการ imports class  ที่ NgModule  export ออกมาก
* provides เป็น Creator ของ services ที่ ngModule สร้างขึ้นและต้องการ Contribute ไปยัง Global collections of services ทำให้สามารถเรียกใช้งาน service  ได้จากทุกที่ใน App
* bootstrap เป็น การระบุว่า main application

ตัวอย่าง workflow สำหรับ module

```
ng new hrms
cd hrms

ng g m employees --routing --module=app.module --spec=false
ng g c employees/employee-list --spec=false
```

##### step1  set module's route  add route in module to inside component \(to component\)

```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { EmployeeListComponent } from './employee-list/employee-list.component';

const routes: Routes = [
  {
    path: '',
    component: EmployeeListComponent
  }
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class EmployeesRoutingModule { }
```

##### step2 set  app.route to add  module route with loadChildren \(to module\)

```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

const routes: Routes = [
  {
    path: 'employees',
    loadChildren: './employees/employees.module#EmployeesModule'
  },
  {
    path: '',
    redirectTo: '',
    pathMatch: 'full'
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes, {enableTracing: true})],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

##### found error

```
ERROR
Error: "Uncaught (in promise): TypeError: __webpack_require__.e is not a function
```

step 3 Remove all imports of your lazy loaded Module จาก root module

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { EmployeesModule } from './employees/employees.module';  //<xxx remove

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    EmployeesModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

เหลือ

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

run

```
ng serve --aot

options:
  --aot
    Build using Ahead of Time compilation
```



