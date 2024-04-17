# Apply filters and Sorting to the Query Builder

The [`QueryBuilder`](query-builder.md) class contains two types of [filterable properties](query-builder.md#filterable-properties): `QueryField` and `QueryAndSortField`. Sorting can only be applied to `QueryAndSortField` fields, while filters can be applied to both types.

## Filtering Methods

Every filter method returns the `QueryBuilder` instance, allowing you to chain multiple filters together.

### `Clear`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">Clear</span>( )</span>

**Description**

Clears the value of the field.

### `SetOp`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">SetOp</span>(<span class="param">QueryFilter.OpOptions</span> <span class="param-name">op</span>, <span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use. Use the `QueryFilter.OpOptions` enum to specify the operation.

### `Equals`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">Equals</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as Equals.

### `NotEquals`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">NotEquals</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as NotEquals.

### `Contains`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">Contains</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as Contains.

### `GreaterThan`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">GreaterThan</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as GreaterThan.

### `LessThan`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">LessThan</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as LessThan.

### `GreaterThanOrEquals`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">GreaterThanOrEquals</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as GreaterThanOrEquals.

### `LessThanOrEquals`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">LessThanOrEquals</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Description**

Sets the value to be filtered and the operation to use as LessThanOrEquals.

## Sorting Methods

### `SetIsAscending`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">SetIsAscending</span>(<span class="param">bool</span> <span class="param-name">value</span>)</span>

**Description**

Sets the order of the field. Use `true` for ascending and `false` for descending.

### `Ascending`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">Ascending</span>( )</span>

**Description**

Sets the order of the field to Ascending.

### `Descending`{:.method}

**Declaration**

<span class="code"><span class="return">QueryBuilder</span> <span class="method">Descending</span>( )</span>

**Description**

Sets the order of the field to Descending.
