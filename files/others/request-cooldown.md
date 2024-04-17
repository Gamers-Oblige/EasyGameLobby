# Request Cooldown class

This class is used to manage every type of lobby request and its [rate limits](https://docs.unity.com/ugs/en-us/manual/lobby/manual/rate-limits). It provides a way to queue requests and execute them when the rate limit allows it. Also provides events to notify when a type of request is Over the rate limit and when it is available to be executed.

## Properties

### `IsAvailable`

Type: [ActionValue](action-value.md)<bool\>
{:.info .under-title-h3}

A boolean [ActionValue](action-value.md) that indicates if the request is available to be executed. Is set to `false` as soon as the request rate limit is reached.

### `OnOverRequestLimit`

Type: Action<bool>
{:.info .under-title-h3}

An event that is triggered when the request is called again while it's not available. It provides a boolean parameter that is true when the request is over the rate limit and false when it is available to be executed.

**Example**

If the request limit is 4 requests per minute, and the request is called 5 times in a minute, on the 4th call the `IsAvailable` property will be set to `false` and in the 5th call the `OnOverRequestLimit` event will be triggered with the parameter `true`. After a minute, the `IsAvailable` property will be set to `true` and the `OnOverRequestLimit` event will be triggered with the parameter `false`.

## Methods

### `WaitForRequestCooldown()`

**Declaration**

<span class="code"><span class="return">Task</span> <span class="method">WaitForRequestCooldown</span>( )</span>

**Description**

Awaitable method that waits until the request is available to be executed. Always call this method before executing a request to ensure that the request is not over the rate limit.
