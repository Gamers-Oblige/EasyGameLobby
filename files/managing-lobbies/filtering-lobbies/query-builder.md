# Query Builder

Implemented in: `EasyGameLobby.Infrastructure`
{:.info .under-title}

Query Builder allows you to easily filter lobbies based on any lobby value including custom values. The query builder can be used to filter lobbies on the [`GetLobbies`](../lobby-manager.md#getlobbies) and [`GetLobbiesAsLocal`](../lobby-manager.md#getlobbies) methods, as well as used to quickly join a lobby with the [`QuickJoinLobby`](../lobby-manager.md#quickjoinlobby) method.

Every Query Builder method returns itself, allowing you to chain multiple filters together.

To enable a Lobby Custom Value to be filtered, an index must be defined in the [Custom Lobby Values](../../getting-started/lobby-settings.md#custom-lobby-and-player-values) window.

## Properties

- **`SampleResults`** - *bool*  
If true, results will be randomly sampled and no continuation token will be returned.
- **`Count`** - *int*  
The number of results to return (Min: 1, Max: 100).
- **`Skip`** - *int*  
The number of results to skip.
- **`ContinuationToken`** - *string*  
The continuation token to use for pagination, automatically setted after first [GetLobbies](../lobby-manager.md#getlobbies) call. It's used to get the next page after calling the [NextPage](#methods) method and calling [GetLobbies](../lobby-manager.md#getlobbies).

## Filterable Properties

Those properties are used to filter and order the lobbies results and can be accessed either by the property name or by their FieldOptions (Unity's Lobby Enum, in case of custom values, use the index of the custom value).

```csharp
QueryBuilder queryBuilder = new QueryBuilder();

queryBuilder
  .Name.Contains("My Lobby")
  [QueryFilter.FieldOptions.N2].LessThan("10") // Custom Value of index number 2
  [QueryFilter.FieldOptions.AvailableSlots].GreaterThan("0")
  .MyCustomValue.GreaterThan("5");

List<LocalLobby> results = await LobbyManager.Instance.GetLobbiesAsLocal(queryBuilder);
```

- **`MaxPlayers`** - [*QueryAndSortField*](apply-query-and-sort.md)
- **`Name`** - [*QueryAndSortField*](apply-query-and-sort.md)
- **`Created`** - [*QueryAndSortField*](apply-query-and-sort.md)
- **`LastUpdated`** - [*QueryAndSortField*](apply-query-and-sort.md)
- **`AvailableSlots`** - [*QueryAndSortField*](apply-query-and-sort.md)
- **`IsLocked`** - [*QueryField*](apply-query-and-sort.md)
- **`HasPassword`** - [*QueryField*](apply-query-and-sort.md)
- **`Any Indexed Custom Value`** - [*QueryAndSortField*](apply-query-and-sort.md)

## Methods

Every method return the QueryBuilder instance, allowing you to chain all methods together.

- <span class="code"><span class="return">QueryBuilder</span> <span class="method">Reset</span>( )</span>  
Reset the query builder to its default values.
- <span class="code"><span class="return">QueryBuilder</span> <span class="method">FirstPage</span>( )</span>  
Set the ContinuationToken to null in order to get the first page of results.
- <span class="code"><span class="return">QueryBuilder</span> <span class="method">NextPage</span>( )</span>  
Set the ContinuationToken to the next available token (only available after the first GetLobbies call using this instance of query builder).

```csharp
QueryBuilder queryBuilder = new QueryBuilder();

queryBuilder
  .HasPassword.Equals("false")
  .SetCount(10);

// Returns the first 10 lobbies
List<LocalLobby> firstResults = await LobbyManager.Instance.GetLobbiesAsLocal(queryBuilder);

queryBuilder.NextPage();

// Returns the next 10 lobbies
List<LocalLobby> nextResults = await LobbyManager.Instance.GetLobbiesAsLocal(queryBuilder);
```

**Properties setters:**

Useful to set properties and continue chaining methods.

- <span class="code"><span class="return">QueryBuilder</span> <span class="method">SetSampleResults</span>(<span class="param">bool</span> <span class="param-name">value</span>)</span>
- <span class="code"><span class="return">QueryBuilder</span> <span class="method">SetCount</span>(<span class="param">int</span> <span class="param-name">value</span>)</span>
- <span class="code"><span class="return">QueryBuilder</span> <span class="method">SetSkip</span>(<span class="param">int</span> <span class="param-name">value</span>)</span>
- <span class="code"><span class="return">QueryBuilder</span> <span class="method">SetContinuationToken</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>
