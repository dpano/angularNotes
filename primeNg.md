# PrimeNG notes

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

### Filter out nested objects
```typescript

// component.ts

cols = [
        { field: 'name', header: 'Name', subfield: 'title' }, // here
        { field: 'settings', header: 'Settings' },
        { field: 'lastUpdateDate', header: 'Last update date' },
        { field: 'status', header: 'Status' },
        { field: 'actions', header: '' }
    ];

// component.html
<th *ngFor="let col of cols" class="clustering-{{col.field}}" [ngSwitch]="col.field" >
        <input *ngSwitchCase="'name'" placeholder="Name" pInputText type="text"
          (input)="tt.filter($event.target.value, 'name.title', 'contains')">
</th>
```
