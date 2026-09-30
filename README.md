# Blazor Toast Component

A lightweight reusable toast notification component for Blazor Server applications.

The component provides success, warning, and error notifications with custom messages, automatic dismissal, manual closing, and simple status-code based APIs.

Originally created in 2021 and later refactored and cleaned up as a standalone portfolio component.

## Features

- Success notifications
- Warning notifications
- Error notifications
- Custom notification headers and messages
- Automatic dismissal after 4 seconds
- Manual close button
- Cancellation of a previous auto-dismiss operation when a new notification is shown
- Status-code based notification API
- Reusable Razor component
- Standalone CSS styling
- Reduced-motion support
- No external UI component library required

## Repository Structure

```text
BlazorToast/
├── Toast.razor
├── blazor-toast.css
└── toast-images/
    ├── success_icon.png
    ├── warning_icon.png
    └── error_icon.png
```

## Component API

The component exposes three primary methods:

```csharp
ShowSuccess(string header, string message)
ShowWarning(string header, string message)
ShowError(string header, string message)
```

Example:

```csharp
_toast?.ShowSuccess(
    "Success",
    "Changes were saved successfully.");
```

```csharp
_toast?.ShowWarning(
    "Warning",
    "Please check the entered values.");
```

```csharp
_toast?.ShowError(
    "Error",
    "The operation failed.");
```

## Status Code API

Notifications can also be displayed using status codes:

```csharp
ShowByStatusCode(int status, string header, string message)
```

or:

```csharp
ShowByStatusCode(int status, string message)
```

Status codes:

```text
1 = Success
2 = Warning
3 = Error
```

Example:

```csharp
_toast?.ShowByStatusCode(
    1,
    "Operation completed successfully.");
```

The component also contains an overload intended for simple entity/action notifications:

```csharp
ShowByStatusCode(
    int status,
    string itemName,
    string action)
```

## Automatic Dismissal

Notifications are automatically dismissed after:

```csharp
4000 milliseconds
```

The component uses:

```csharp
CancellationTokenSource
```

together with:

```csharp
Task.Delay
```

to manage automatic dismissal.

If another notification is displayed before the current one is dismissed, the previous pending dismissal operation is cancelled.

The component implements `IDisposable` so cancellation resources are cleaned up when the component is disposed.

## Using the Component

Copy:

```text
Toast.razor
```

into your Blazor project.

Copy:

```text
blazor-toast.css
```

into your application's static CSS directory, for example:

```text
wwwroot/css/
```

Copy the image directory:

```text
toast-images/
```

into:

```text
wwwroot/toast-images/
```

Then reference the stylesheet from the application's host page:

```html
<link href="css/blazor-toast.css" rel="stylesheet" />
```

Add the component to a Razor page or layout:

```razor
<Toast @ref="_toast" />
```

Create a component reference:

```csharp
private Toast? _toast;
```

You can then display notifications directly:

```csharp
_toast?.ShowSuccess(
    "Success",
    "The operation completed successfully.");
```

## Styling

The component includes standalone CSS classes for:

- toast container
- header
- body
- close button
- positioning
- success state
- warning state
- error state
- fade transitions

The included stylesheet can be modified to match the visual style of another Blazor application.

## About This Project

This repository contains a small reusable Blazor UI component rather than a complete application.

It is included in my GitHub portfolio as an example of:

- reusable Razor component development
- component-level state management
- asynchronous UI behavior
- cancellation handling
- CSS-based notification states
- simple public component APIs
