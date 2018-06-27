---
title: Overlay Service - Positioning Strategies
_description: Explanation and example about the Overlay Service's IPositionStrategy interface and the classes that implement it.
---

# Position strategies

Position strategies determine where to display the component in the provided IgxOverlayService. There are three position strategies:

1. **Global** - Positions the element based on the directions passed in through `positionSettings`. These are Top/Middle/Bottom for `verticalDirection` and Left/Center/Right for `horizontalDirection`. Defaults to:

    | horizontalDirection        | verticalDirection        |
    |:---------------------------|:-------------------------|
    | HorizontalAlignment.Center | VerticalAlignment.Middle |
<br/>

2. **Connected** - Positions the element based on the directions and start point passed in through `positionSettings`. It is possible to either pass a start point (type `Point`) or an `HTMLElement` as a positioning base. Defaults to:

    | target          | horizontalDirection       |  verticalDirection       | horizontalStartPoint     | verticalStartPoint       |
    |:----------------|:--------------------------|:-------------------------|:-------------------------|:-------------------------|
    | new Point(0, 0) | HorizontalAlignment.Right | VerticalAlignment.Bottom | HorizontalAlignment.Left | VerticalAlignment.Bottom |
<br/>

3. **Auto** - Positions the element as in **Connected** positioning strategy and re-positions the element in the view port (calculating a different start point) in case the element is partially out of view. Defaults to:

    | target          | horizontalDirection       |  verticalDirection       | horizontalStartPoint     | verticalStartPoint       |
    |:----------------|:--------------------------|:-------------------------|:-------------------------|:-------------------------|
    | new Point(0, 0) | HorizontalAlignment.Right | VerticalAlignment.Bottom | HorizontalAlignment.Left | VerticalAlignment.Bottom |

*Note*: Will not try to reposition the element if the strategy is using  HorziontalDirection = Center / VericalDirection = Middle.

## Usage
Position an element based on an existing button as a target, so it's start point is the button's Bottom/Left corner.
```typescript
const positionSettings: PositionSettings = {
    target: buttonElement.nativeElement,
    horizontalDirection: HorizontalAlignment.Right,
    verticalDirection: VerticalAlignment.Bottom,
    horizontalStartPoint: HorizontalAlignment.Left,
    verticalStartPoint: VerticalAlignment.Bottom
};

const strategy =  new ConnectedPositioningStrategy(positionSettings);
strategy.position(contentWrapper, size);
```

## Getting Started
The position strategy is passed as a property in the `overlaySettings` parameter when the `overlay.show()` method is called:
```typescript
    // Initializing and using overlay settings
    const overlaySettings: OverlaySettings = {
        positionStrategy: new GlobalPositionStrategy(), // Passes the positioning strategy
        scrollStrategy: new AbsoluteScrollStrategy(),
        modal: true,
        closeOnOutsideClick: true
    }
    overlay.show(dummyElement, overlaySettings); 
``` 
To change the position strategy used by the overlay, override the `positionStrategy` property of the `overlaySettings` object passed to the overlay:
```typescript
    // overlaySettings is an existing object of type OverlaySettings
    // to override the position strategy
    const newOverlaySettings = Object.assing({}, overlaySettings);
    Object.assing(newOverlaySettings, {
        positionStrategy: new AutoPositionStrategy()
    })
    overlay.show(dummyElement, newOverlaySettings); 
```
To change the position settings an already existing strategy is using, override any of the settings of that strategy:
```typescript
    // overlaySettings is an existing object of type OverlaySettings
    // overlaySettings.positionStrategy is an existing PositionStrategy with settings of type PositionSettings
    // to override the position setting of an existing PositionStrategy
    Object.assign(overlaySettings.positionStrategy.settings, {
        target: dummyHTMLElement,
        horizontalStartPoint: HorizontalAlignment.Left,
        horizontalDirection: HorizontalAlignment.Left
    });
    overlay.show(dummyElement, overlaySettings);
    // the element will now start to the left of the target (dimmyHTMLElement)
    // and will align itself to the left
```

### Dependencies

Import the desired position strategy if needed like:

```typescript
import {AutoPositionStrategy, GlobalPositionStrategy, ConnectedPositioningStrategy } from './position/global-position-strategy';
```

## API

##### Methods
| Position Strategy | Name                                         | Description                                     |
|:------------------|:---------------------------------------------|:------------------------------------------------|
| Global            | `position(contentElement)`                   | Positions the element, based on the horizontal and vertical directions. |
| Connected         | `position(contentElement, size{})`           | Positions the element, based on the position strategy used and the size passed in.|
| Auto              | `position(contentElement, size{}, document?)`| Positions the element, based on the position strategy used and the size passed in.|

###### PositionSettings
| Name               | Type                        | Description |
| :----------------- | :-------------------------- | :---------- |
|target              | Point | HTMLElement         | Attaching target for the component to show          |
|horizontalDirection | HorizontalAlignment         | Direction in which the component should show        |
|verticalDirection   | VerticalAlignment           | Direction in which the component should show        |
|horizontalStartPoint| HorizontalAlignment         | Target's starting point                             |
|verticalStartPoint  | VerticalAlignment           | Target's starting point                             |
|openAnimation       | AnimationReferenceMetadata  | Animation applied while overlay opens               |
|closeAnimation      | AnimationReferenceMetadata  | Animation applied while overlay closes              |