# Custom Value Types

if you want to use your own type as a custom value in the lobby, you can create a class that implements the `ILobbyValue` interface.

## ILobbyValue Interface

### Properties

#### `Key`

Type: `string`
{:.info .under-title-h3}

The key of the value. It must be unique within all other custom values in the lobby or player.

#### `Value`

Type: `string`
{:.info .under-title-h3}

The value of the custom value. It must be serializable into a string. To use a more complex type, you can serialize it into a string using JSON or any other serialization method.

#### `IsOutdated`

Type: `bool`
{:.info .under-title-h3}

Determines if the value is outdated and needs to be updated. It needs to be set to `true` when the value is changed in order to be sent to the server.

#### `Visibility`

Type: `VisibilityOptions`
{:.info .under-title-h3}

Determines the visibility of the value. Refer to the [Data access and visibility](https://docs.unity.com/ugs/en-us/manual/lobby/manual/lobby-data-and-player-data#Data_access_and_visibility) for more information.

### Methods

#### `SetUpdatedValue`

**Declaration**

<span class="code"><span class="method">SetUpdatedValue</span>(<span class="param">string</span> <span class="param-name">value</span>)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **value**<span class="required">\*</span>  | *string* | The new value to be set. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Sets the `Value` of the custom value and marks the outdated property as `false`.

## Usage

In order to use your newly created custom value, the file must be placed either in the `Assets/Easy Game Lobby/Runtime` folder or in a new folder with a [Assembly Definition Reference](https://docs.unity3d.com/Manual/class-AssemblyDefinitionReferenceImporter.html) that references the `com.oblige.easygamelobby` assembly.

### Creating the Assembly Definition Reference

1. Create a new folder
2. Add a new [Assembly Definition Reference](https://docs.unity3d.com/Manual/class-AssemblyDefinitionReferenceImporter.html).
      1. Right-click on the new folder and select `Create > Assembly Definition Reference`.
      2. On the `Assembly Definition Reference` inspector, add the `com.oblige.easygamelobby` assembly definition.

### Adding the Custom Value to the Lobby or Player

Locate either the `LocalPlayerCustomValues` or `LocalLobbyCustomValues` files in the `Assets/Easy Game Lobby/Runtime` folder and add a new custom value to the dictionary.

```csharp hl_lines="11 20"
public class LocalPlayerCustomValues
  {
    public readonly Dictionary<string, ILobbyValue> CustomDataMap = new();
    public ILobbyValue[] CustomDataArr => CustomDataMap.Values.ToArray();

    // Auto-generated code for custom values, do not modify manually the code inside this region or changes will be lost.
    #region Custom Data Properties
    public readonly LobbyActionValue<string> Name = new("Name", VisibilityOptions.Member);
    #endregion

    public readonly MyCustomValueClass MyCustomValue = new(); // Your custom value

    public LocalPlayerCustomValues()
    {
      // Auto-generated code for custom values, do not modify manually the code inside this region or changes will be lost.
      #region Custom Data Additions
      CustomDataMap.Add(Name.Key, Name);
      #endregion
        
      CustomDataMap.Add(MyCustomValue.Key, MyCustomValue); // Your custom value
    }
  }
```
