# Request Listener Behaviour

It's a base class that provides a way to listen to when a [`RequestCooldown`](../../others/request-cooldown.md) is over the rate limit and when it's available again.

## Inspector Options

- **OnOverRequestLimit**: Flags Enum with the types of requests that this component should listen to when it's over the rate limit.
- **OnIsAvailable**: Flags Enum with the types of requests that this component should listen to when it's available again.

## Abstract Methods

- <span class="code"><span class="method">HandleOverRequestLimit</span>(<span class="param">bool</span> <span class="param-name">isOverRequestLimit</span>)</span>  
Method called when the request is over the rate limit.

- <span class="code"><span class="method">HandleIsAvailableChanged</span>(<span class="param">bool</span> <span class="param-name">isAvailable</span>, <span class="param">bool</span> <span class="param-name">wasAvailable</span>)</span>  
Method called when the request is available again after being over the rate limit.

## Request Selectable

The `RequestSelectable` is a utility component that implements the `RequestListenerBehaviour` class, useful to disable/enable a selectable component when the request is over the rate limit or available again. In the template it's used to disable the buttons when the request is over the rate limit and enable them when it's available again.

## Request Canvas Group

The `RequestCanvasGroup` is a utility component that implements the `RequestListenerBehaviour` class, useful to show/hide a canvas group when the request is over the rate limit or available again. In the template it's used to show a loading panel when the request is over the rate limit and hide it when it's available again.

<!-- markdownlint-disable MD024 -->
### Inspector Options
<!-- markdownlint-enable MD024 -->

- **Visible When Over Request Limit**: If true, the canvas group will be visible when the request is over the rate limit and hidden when it's available again.
- **Visible When Available**: If true, the canvas group will be visible when the request is available again and hidden when it's over the rate limit.
