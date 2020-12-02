# PrimeNG notes

## Filter out nested objects
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
