# Introduction

1 Install Angular 7  และ dependencies

    npm uninstall -g @angular/cli
    npm cache verify
    npm install -g @angular/cli

    npm --version

         _                      _                 ____ _     ___
        / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
       / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
      / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
     /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                    |___/


    Angular CLI: 7.0.6
    Node: 10.6.0
    OS: darwin x64
    Angular:
    ...

    Package                      Version
    ------------------------------------------------------
    @angular-devkit/architect    0.10.6
    @angular-devkit/core         7.0.6
    @angular-devkit/schematics   7.0.6
    @schematics/angular          7.0.6
    @schematics/update           0.10.6
    rxjs                         6.3.3
    typescript                   3.1.6

สร้าง project

```
ng new  hrms
cd hrms

npm install bootstrap --save
```

add angular.json

```
"styles": [
   "src/styles.css",
   "./node_modules/bootstrap/dist/css/bootstrap.min.css"
 ],
```

2 Generate Angular component

ต้องการ CREATE , READ, UPDATE จึงต้องมี 3 component  register ใน employee.module

```
$ ng g m employees --routing --spec=false --module=app.module
CREATE src/app/employees/employees-routing.module.ts (252 bytes)
CREATE src/app/employees/employees.module.ts (291 bytes)
UPDATE src/app/app.module.ts (478 bytes)


$ ng g c employees/employee-add --spec=false
CREATE src/app/employees/employee-add/employee-add.component.scss (0 bytes)
CREATE src/app/employees/employee-add/employee-add.component.html (31 bytes)
CREATE src/app/employees/employee-add/employee-add.component.ts (293 bytes)
UPDATE src/app/employees/employees.module.ts (389 bytes)

$ ng g c employees/employee-get --spec=false
CREATE src/app/employees/employee-get/employee-get.component.scss (0 bytes)
CREATE src/app/employees/employee-get/employee-get.component.html (31 bytes)
CREATE src/app/employees/employee-get/employee-get.component.ts (293 bytes)
UPDATE src/app/employees/employees.module.ts (489 bytes)


$ ng g c employees/employee-edit --spec=false
CREATE src/app/employees/employee-edit/employee-edit.component.scss (0 bytes)
CREATE src/app/employees/employee-edit/employee-edit.component.html (32 bytes)
CREATE src/app/employees/employee-edit/employee-edit.component.ts (297 bytes)
UPDATE src/app/employees/employees.module.ts (593 bytes)
```

**default  class  EmployeeAddComponent   &lt;-  employee-add.component**

```
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-employee-add',
  templateUrl: './employee-add.component.html',
  styleUrls: ['./employee-add.component.scss']
})
export class EmployeeAddComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

}
```

**edit routing employees-routing.module.ts**

```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { EmployeeAddComponent } from './employee-add/employee-add.component';
import { EmployeeGetComponent } from './employee-get/employee-get.component';
import { EmployeeEditComponent } from './employee-edit/employee-edit.component';

const routes: Routes = [
  {path: '',  component: EmployeeGetComponent},
  {path: 'create', component: EmployeeAddComponent },
  {path: 'edit/:id', component: EmployeeEditComponent}
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class EmployeesRoutingModule { }
```

**edit routing ใน app-routing.module**

implement lazy loading  [https://angular.io/guide/lazy-loading-ngmodules](https://angular.io/guide/lazy-loading-ngmodules)

![](https://angular.io/generated/images/guide/lazy-loading-ngmodules/lazy-load-relationship.jpg)Feature module acts as a doorway via router. in app-route เราทำการ config route ให้ชี้มายัง feature modules. เป็นการเชีอมโยงกัน

```
const routes: Routes = [
  {
    path: 'customers',
    loadChildren: './customers/customers.module#CustomersModule'
  },
  {
    path: 'orders',
    loadChildren: './orders/orders.module#OrdersModule'
  },
  {
    path: '',
    redirectTo: '',
    pathMatch: 'full'
  }
];
```

ดังนั้น เช่นดียวกัน

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
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

ระมัดระวัง จะต้อง ไม่ โหลด Module ใน App.module

```
ERROR Error: "Uncaught (in promise): TypeError: __webpack_require__.e is not a function
ไม่ต้อง Load Employee module แล้ว เพราะว่า  จะโหลดด้วย Lazyload 
```

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



