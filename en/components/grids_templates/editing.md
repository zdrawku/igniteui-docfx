---
title: Grid Editing - Native Angular | Ignite UI for Angular
_description: The Ignite UI for Angular Data Grid control provides default cell templates for editable columns which are based on the data type of the column.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Native Angular Component, Angular Grid, Angular Data Grid component, Angular Data Grid control, Angular Grid component, Angular Grid control, Angular High Performance Grid, Cell Editing
---

### Grid Editing

The Grid component in Ignite UI for Angular provides you a default cell templates for editable columns which are based on the data type of the column. In addition you can define your own custom templates for editable columns and override default behavior for committing and discarding changes in the cell value .

#### Demo

<div class="sample-container loading" style="height:650px">
    <iframe id="grid-editing-sample-iframe" src='{environment:demosBaseUrl}/grid/grid-editing' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<br/>
<div>
<button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="grid-editing-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider--half"></div>

In order to be able to enter edit mode for specific cell, you should first set the column to be [`editable`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#editable). If you want to use a data type specific *edit templates*, you should specify the column [`dataType`]({environment:angularApiUrl}/classes/igxcolumncomponent.html#datatype) property. So let's now see what are the default templates for each type:

 - For `string` data type, default template is using [**igxInput**]({environment:angularApiUrl}/classes/igxinputdirective.html)
 - For `number` data type, default template is using **[igxInput]({environment:angularApiUrl}/classes/igxinputdirective.html) type="number"**, so if you try to update cell to a value which can not be parsed to a number your change is going to be discarded, and the value in the cell will be set to **0**.
 - For `date` data type, default template is using [**igx-date-picker**]({environment:angularApiUrl}/classes/igxdatepickercomponent.html)
 - For `boolean` data type, default template is using [**igx-checkbox**]({environment:angularApiUrl}/classes/igxcheckboxcomponent.html)

You can enter edit mode for specific cell, when an editable cell is focused in one of the following ways:
 - on double click;
 - on single click - Single click will enter edit mode only if the previously selected cell was in edit mode and currently selected cell is editable. If the previously selected cell was not in edit mode, single click will select the cell without entering edit mode;
 - on key press `Enter`;
 - on key press `F2`;

You can exit edit mode **without committing** the changes in one of the following ways:
 - on key press `Escape`;
 - when you perform *sorting*, *filtering*, *searching* and *hiding* operations;

You can exit edit mode and **commit** the changes in one of the following ways:
 - on key press `Enter`;
 - on key press `F2`;
 - on key press `Tab`;
 - on single click to another cell - when you click on another cell in the grid, your changes will be submitted.
 - operations like paging, resize, pin, move, sort column or change page, will exit edit mode and changes will be submitted.

> [!NOTE]
> The cell remains in edit mode when you scroll vertically or horizontally or click outside the grid. This is valid for both cell editing and row editing.

You can also modify the cell value through the IgxGrid API but only if primary key is defined:

```typescript
...
    public updateCell() {
        this.grid1.updateCell(newValue, rowID, 'ReorderLevel');
    }
...
```
Please notice that if the cell you want to update is outside grid's display container the new value will not be submitted.

Another way to update cell is directly through [`update`]({environment:angularApiUrl}/classes/igxgridcellcomponent.html#update) method of [`IgxGridCellComponent`]({environment:angularApiUrl}/classes/igxgridcellcomponent.html):

```typescript
...
    public updateCell() {
        const cell = this.grid1.getCellByColumn(rowIndex, 'ReorderLevel');
        // You can also get cell by rowID if primary key is defined
        // cell = this.grid1.getCellByKey(rowID, 'ReorderLevel');
        cell.update(70);
    }
...
```
If you want to define a custom template which will be applied when the cell is in edit mode, you can see the documentation for [Grid Columns configuration](grid.md#columns-configuration).

### CRUD operations

> [!NOTE]
> Please keep in mind that when you perform some **CRUD operation** all of the applied pipes like **filtering**, **sorting** and **grouping** will be re-applied and your view will be automatically updated.

The [`IgxGridComponent`]({environment:angularApiUrl}/classes/igxgridcomponent.html) provides a straigtforward API for basic CRUD operations.

#### Adding a new record

The grid component exposes the [`addRow`]({environment:angularApiUrl}/classes/igxgridcomponent.html#addrow) method which will add the provided data to the data source itself.

```typescript
// Adding a new record
// Assuming we have a `getNewRecord` method returning the new row data.
const record = this.getNewRecord();
this.grid.addRow(record);
```

#### Updating data in the grid

Updating data in the grid is achieved through [`updateRow`]({environment:angularApiUrl}/classes/igxgridcomponent.html#updaterow) and [`updateCell`]({environment:angularApiUrl}/classes/igxgridcomponent.html#updatecell) methods but **only if primary key for the grid is defined**. You can also directly update a cell and row value through their [`update`]({environment:angularApiUrl}/classes/igxgridcellcomponent.html#update) method.

```typescript
// Updating the whole row
this.grid.updateRow(newData, this.selectedCell.cellID.rowID);

// Just a particualr cell through the Grid API
this.grid.updateCell(newData, this.selectedCell.cellID.rowID, this.selectedCell.column.field);

// Directly using the cell `update` method
this.selectedCell.update(newData);

// Directly using the row `update` method
const row = this.grid.getRowByKey(rowID);
row.update(newData);
```

#### Deleting data from the grid

Please keep in mind that [`deleteRow()`]({environment:angularApiUrl}/classes/igxgridcomponent.html#deleterow) method will remove the specified row only if primary key is defined.

```typescript
// Delete row through Grid API
this.grid.deleteRow(this.selectedCell.cellID.rowID);
// Delete row through row object
const row = this.grid.getRowByIndex(rowIndex);
row.delete();
```
These can be wired to user interactions, not necessarily related to the **igx-grid**; for example, a button click:
```html
<button igxButton igxRipple (click)="deleteRow($event)">Delete Row</button>
```

<div class="divider--half"></div>

## API References

* [IgxGridCellComponent]({environment:angularApiUrl}/classes/igxgridcellcomponent.html)
* [IgxGridComponent Styles]({environment:sassApiUrl}/index.html#function-igx-grid-theme)
* [IgxGridRowComponent]({environment:angularApiUrl}/classes/igxgridrowcomponent.html)
* [IgxInputDirective]({environment:angularApiUrl}/classes/igxinputdirective.html)
* [IgxDatePickerComponent]({environment:angularApiUrl}/classes/igxdatepickercomponent.html)
* [IgxDatePickerComponent Styles]({environment:sassApiUrl}/index.html#function-igx-date-picker-theme)
* [IgxCheckboxComponent]({environment:angularApiUrl}/classes/igxcheckboxcomponent.html)
* [IgxCheckboxComponent Styles]({environment:sassApiUrl}/index.html#function-igx-checkbox-theme) 
* [IgxOverlay]({environment:angularApiUrl}/interfaces/overlaysettings.html)
* [IgxOverlay Styles]({environment:sassApiUrl}/index.html#function-igx-overlay-theme)


### Additional Resources
<div class="divider--half"></div>

* [Grid overview](grid.md)
* [Virtualization and Performance](virtualization.md)
* [Paging](paging.md)
* [Filtering](filtering.md)
* [Sorting](sorting.md)
* [Summaries](summaries.md)
* [Column Pinning](column_pinning.md)
* [Column Resizing](column_resizing.md)
* [Selection](selection.md)
* [Searching](search.md)