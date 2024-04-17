# Password Popup

It's a component that displays a popup to the user to input a password, used to join a private lobby.

Joins the given lobby ID when the user clicks the join button, or closes the popup when the user clicks the close button.

## Methods

### `OpenPopup`{:.method}

**Declaration**

<span class="code">void <span class="method">OpenPopup</span>(<span class="param">string</span> <span class="param-name">lobbyId</span>)</span>

**Parameters**

| Parameter | Type | Description |
| --- | --- | --- |
| **lobbyId**<span class="required">\*</span> | *string* | The ID of the lobby to join. |

*<span class="required">\*</span> Required parameter.*
{:.info .under-table}

**Description**

Enables the popup game object and sets the lobby ID to join.
