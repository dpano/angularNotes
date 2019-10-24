# angularNotes
Keep some notes for angular development

### Turbo table sort
set only specific columns to be sortable
https://forum.primefaces.org/viewtopic.php?t=55946
```css
:host >>> .doc-relevance .ui-slider {
    background: #14a4ff
}
:host >>> .doc-relevance .ui-slider-range-min {
    background: #aaa
}
```

### NPM
- Install dependencies from scratch
```
rm -rf node_modules/ -- in windows: rmdir /q /s folder_name
npm cache clean
npm install
```

### UI: Remove html tags except
Use a negative lookahead (by using a regex such as /<(?!br\s*\/?)[^>]+>/g):
```
var html = 'this is my <b>string</b> and it\'s pretty cool<br />isn\'t it?<br>Yep, it is. <strong>More HTML tags</strong>';
html = html.replace(/<(?!br\s*\/?)[^>]+>/g, '');
console.log(html); 
//this is my string and it's pretty cool<br />isn't it?<br>Yep, it is. More HTML tags
```

### UI: Angular Focus form element
Use native angular Renderer2 module
import to constructor and then `this.renderer.selectRootElement('#inputportfolio').focus();`

### UI: Add event listener on dom elements
Inject ElementRef
```ts
constructor(private elementRef: ElementRef)
```
After the view initialization
```ts
ngAfterViewInit(): void {
        this.elementRef.nativeElement.querySelectorAll('.simba-click-element').forEach(item => {
            item.addEventListener('click', this.onClick.bind(this));
        });
    }
```
The event that it will be binded
```ts
onClick(event){
        this.elementRef.nativeElement.querySelector(`#${event.target.attributes.targetId.value}`)
            .scrollIntoView({ behavior: 'smooth', block: 'start', inline: 'nearest' });
    }
```
### UI: innerHTML, detect InnerHtml has been rendered
[[issue link]](https://github.com/angular/angular/issues/21163), [[example stackblitz]](https://stackblitz.com/edit/angular-mutationobserver)

#### Create the directive 
```typescript
import { Directive, ElementRef, EventEmitter, Output, OnDestroy } from '@angular/core';

@Directive({
  selector: '[appAppMotationObserver]'
})
export class AppMotationObserverDirective implements OnDestroy {
  _observer: MutationObserver;
  @Output() innerHtmlRendered = new EventEmitter();

  constructor(private el: ElementRef) {
    this._observer = new MutationObserver((mutations) => {
      mutations.forEach((mutation, index) => {
        if (mutation.type === 'childList') {
          this.innerHtmlRendered.emit();
        }
      });
    });
    this._observer.observe(
      this.el.nativeElement,
      { attributes: true, childList: true, characterData: true }
    );
  }

  ngOnDestroy() {
    if (this._observer) {
      this._observer.disconnect();
    }
  }

}
```
#### component.html
```html
  <p [innerHTML]="text"
    appAppMotationObserver 
    (innerHtmlRendered)="renderedCb()"></p>

  <p *ngIf="!text">wait for async...</p>
```
#### component.ts
```typescript
.
.
.
// catch the emitted event
renderedCb() {
    console.log('rendered...')
  }
.
.
.
```
