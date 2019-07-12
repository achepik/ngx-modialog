# ngx-bootstrap-modialog (previously ngx-modialog`)

## Install
```bash
project is in development
```

## Quick start

**In your application root module definition add `ModalModule` and the plugin you want to use:**

We will use the bootstrap plugin (`BootstrapModalModule`) for this introduction.

```typescript
import { ModalModule } from 'ngx-modialog';
import { BootstrapModalModule } from 'ngx-modialog/plugins/bootstrap';

// lots of code...

@NgModule({
  bootstrap: [ /* ... */ ],
  declarations: [ /* ... */ ],
  imports: [
    /* ... */
    ModalModule.forRoot(),
    BootstrapModalModule
  ],
})
export class AppModule { /* lots of code... */ }
```

**In any angular component or service inject the `Modal` service and open a modal**:


```typescript
import { Component, ViewContainerRef } from '@angular/core';
import { Overlay } from 'ngx-modialog';
import { Modal } from 'ngx-modialog/plugins/bootstrap';

@Component({
  selector: 'my-app',
  template: `<button (click)="onClick()">Alert</button>`
})
export class AppComponent {
  constructor(public modal: Modal) { }

  onClick() {
    const dialogRef = this.modal.alert()
        .size('lg')
        .showClose(true)
        .title('A simple Alert style modal window')
        .body(`
            <h4>Alert is a classic (title/body/footer) 1 button modal window that 
            does not block.</h4>
            <b>Configuration:</b>
            <ul>
                <li>Non blocking (click anywhere outside to dismiss)</li>
                <li>Size large</li>
                <li>Dismissed with default keyboard key (ESC)</li>
                <li>Close wth button click</li>
                <li>HTML content</li>
            </ul>`)
        .open();

    dialogRef.result
        .then( result => alert(`The result is: ${result}`) );
  }
}
```

The demo application comes with a [dynamic modal generator](http://shlomiassaf.github.io/ngx-modialog#/bootstrap-demo/customizeModals) for the **Boostrap** plugin

## Plugins
Plugins serve as a concrete UI implementation for a modal.

It can be an implementation for a known library (e.g: bootstrap) or something completely unique

While `ngx-modialog` has some built in plugins it is also possible to use external plugins from NPM, if someone decide to build one.

> Built a plugin? I would love to know :)

# Known bugs
### The dialog closes when removing the target DOM element in a click event
ref [issue#111](https://github.com/shlomiassaf/ngx-modialog/issues/111)

To avoid this problem use `event.stopPropagation();` or put the element removal inside a `setTimeout` call
