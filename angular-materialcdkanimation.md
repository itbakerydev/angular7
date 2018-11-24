## Installation

```
npm install @angular/material @angular/cdk
```

**`src/styles.css`**

```
@import "~@angular/material/prebuilt-themes/indigo-pink.css";
```

**Angular Material Gesture**

Some components like [Slide Toggle](https://material.angular.io/components/slide-toggle/overview), [Slider](https://material.angular.io/components/slider/overview), and [Tooltip](https://material.angular.io/components/tooltip/overview) rely on a library called HammerJS to capture touch gestures. So, you will need to install HammerJS and load it into our application.

To do so, from the project root directory, run:

```
npm install hammerjs
```

edit  **src/main.ts**

```
import 'hammerjs'; 
```

Material ICON

```
<!doctype html>
<html lang="en">
<head>
  <!-- ... other tags ... -->
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<!-- ... body and app root ... -->
</html>
```

**add material module**

```
ng g m material --module=app.module --spec=false
```

```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

import {
  MatSidenavModule,
  MatToolbarModule,
  MatIconModule,
  MatListModule,
} from '@angular/material';



@NgModule({
  declarations: [],
  imports: [
    CommonModule,
    MatSidenavModule,
    MatToolbarModule,
    MatIconModule,
    MatListModule,    
  ],
  exports: [
    MatSidenavModule,
    MatToolbarModule,
    MatIconModule,
    MatListModule,
  ]
})
export class MaterialModule { }
```

**import MaterialModule to app.module**

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { MaterialModule } from './material/material.module';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    MaterialModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**app template**

```
<mat-sidenav-container>
  <mat-sidenav  #sidenav role="navigation">
   <mat-nav-list>
    <a mat-list-item>
      <mat-icon class="icon">input</mat-icon>
      <span class="label">Login</span>
    </a>
    <a mat-list-item>
      <mat-icon class="icon">home</mat-icon>  
        <span class="label">Home</span>
    </a>
    <a mat-list-item>
      <mat-icon class="icon">dashboard</mat-icon>  
      <span class="label">Dashboard</span>
    </a>
    <a  mat-list-item type="button">
      <mat-icon class="icon">input</mat-icon>
      <span class="label">LogOut</span>
    </a>  
    </mat-nav-list>
  </mat-sidenav>
  <mat-sidenav-content>
    <mat-toolbar color="primary">
     <div fxHide.gt-xs>
       <button mat-icon-button>
        <mat-icon>menu</mat-icon>
      </button>
    </div>
     <div>
       <a>
          Material Blog
       </a>
     </div>
     <div fxFlex fxLayout fxLayoutAlign="flex-end"  fxHide.xs>
        <ul fxLayout fxLayoutGap="20px" class="navigation-items">
            <li>
                <a>
                  <mat-icon class="icon">input</mat-icon>
                  <span  class="label">Login</span>
                 </a>
            </li>
            <li>
              <a >
                  <mat-icon class="icon">home</mat-icon>
                  <span class="label">Home</span>
              </a>
            </li>
            <li>
                <a>
                    <mat-icon class="icon">dashboard</mat-icon>
                    <span class="label">Dashboard</span>
                </a>
              </li>
            <li>
                <a>
                  <mat-icon class="icon">input</mat-icon>
                  <span class="label">LogOut</span>
                 </a>
            </li>
        </ul>
     </div>
    </mat-toolbar>
    <main>
    </main>
  </mat-sidenav-content>
</mat-sidenav-container>
```



