## Installation

```
npm i --save angular-bootstrap-md chart.js@2.5.0 font-awesome hammerjs
```

**edit  /src/app/app.module.ts**

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, NO_ERRORS_SCHEMA } from '@angular/core';
import { MDBBootstrapModule } from 'angular-bootstrap-md';
```

* **NO\_ERRORS\_SCHEMA**

  tells the compiler to not error based on unknown elements, which are used by MdBootstrap

**edit @NgModule**

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, NO_ERRORS_SCHEMA } from '@angular/core';
import { MDBBootstrapModule } from 'angular-bootstrap-md';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    MDBBootstrapModule.forRoot()
  ],
  providers: [],
  schemas: [ NO_ERRORS_SCHEMA ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

angular.json

```
            "styles": [
              "./node_modules/font-awesome/scss/font-awesome.scss",
              "./node_modules/angular-bootstrap-md/scss/bootstrap/bootstrap.scss",
              "./node_modules/angular-bootstrap-md/scss/mdb-free.scss",
              "src/styles.scss"
            ],
            "scripts": [
              "./node_modules/chart.js/dist/Chart.js",
              "./node_modules/hammerjs/hammer.min.js"
            ]
```

tsconfig.json  เพิ่ม บรรทัดสุดท้าย

```
 {
  "compileOnSave": false,
  "compilerOptions": {
    "baseUrl": "./",
    "outDir": "./dist/out-tsc",
    "sourceMap": true,
    "declaration": false,
    "module": "es2015",
    "moduleResolution": "node",
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "target": "es5",
    "typeRoots": [
      "node_modules/@types"
    ],
    "lib": [
      "es2018",
      "dom"
    ]
  },
  "include": ["node_modules/angular-bootstrap-md/**/*.ts",  "src/**/*.ts"]
}
```

run

```
ng serve --open
```

![](https://s3.amazonaws.com/coursetro/posts/content_images/1-1517416493468.png)

**Integrate  bootstrap Navigation**

Copy and paste the first one into  **/src/app/app.component.html**

[https://mdbootstrap.com/legacy/angular/4.1.0/?page=components/navbars](https://mdbootstrap.com/legacy/angular/4.1.0/?page=components/navbars)

```
<navbar SideClass="navbar navbar-toggleable-md navbar-dark bg-primary">
    <logo><a class="logo navbar-brand" href="#">Navbar</a></logo>
    <links>
        <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
                <a class="nav-link">Home<span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item">
                <a class="nav-link">Features</a>
            </li>
            <li class="nav-item">
                <a class="nav-link">Pricing</a>
            </li>
            <li class="nav-item dropdown btn-group" dropdown>
                <a dropdownToggle ripple-radius type="button" class="nav-link dropdown-toggle">
                Basic dropdown<span class="caret"></span></a>
                <div *dropdownMenu class="dropdown-menu dropdown dropdown-primary" role="menu">
                    <a class="dropdown-item" href="#">Action</a>
                    <a class="dropdown-item" href="#">Another action</a>
                    <a class="dropdown-item" href="#">Something else here</a>
                    <div class="divider dropdown-divider"></div>
                    <a class="dropdown-item" href="#">Separated link</a>
                </div>
            </li>
        </ul>
        <form class="form-inline">
            <input class="form-control" type="text" placeholder="Search">
        </form>
    </links>
</navbar>
```

```
<!--Main Navigation-->
<header>
  <nav class="navbar fixed-top navbar-expand-lg navbar-dark pink scrolling-navbar">
    <a class="navbar-brand" href="#"><strong>Navbar</strong></a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Features</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Pricing</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Opinions</a>
        </li>
      </ul>
      <ul class="navbar-nav nav-flex-icons">
        <li class="nav-item">
          <a class="nav-link"><i class="fa fa-facebook"></i></a>
        </li>
        <li class="nav-item">
          <a class="nav-link"><i class="fa fa-twitter"></i></a>
        </li>
        <li class="nav-item">
          <a class="nav-link"><i class="fa fa-instagram"></i></a>
        </li>
      </ul>
    </div>
  </nav>

</header>
<!--Main Navigation-->
```



