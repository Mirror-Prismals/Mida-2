> WHAT IS THIS?!
> this is a wip repo pls forgive the under construction vibe
> why are you reading this? who are you?
> Mida 2 is a programming languge. It's a sequel and companion to mida 1, which you can find information on in this github
> https://github.com/Mirror-Prismals/Mida
# Frog Level
i made a agi puzzle game, its called frog level



level 1:

reach the goal
```mida
[S][=][=][=][G]
```
tell the path you have to take, levels will get more harder



level 2:

reach the goal
```mida
[S][=]

[||]

[||]

[G]
```


level 3:

reach the goal
```mida
[r][=][=][S][=][=][q]

[||]

[||]

[G]
```


correct!

level 4
```mida
[S][T][=][T]

[=][||][=][||]

[||][||][=][||]

[||][p][=][G]
```


p can be entered from the top or bottom and right, then it switches to a q, after which it cannot be exited from the right, only left, and vice versa for q becomes p, its a fun mechanic

frog level is a part of mida 2, its sort of like an arc agi puzzle
# Mida Network Syntax - Layer 3

This document describes the Layer 3 network syntax in Mida, focusing on managed and unmanaged switches, transmitters (`@tx`), receivers (`@rx`), dynamic subscriptions, labels, and network matrix management.

## Overview
Mida’s network layer uses a virtual routing syntax inspired by networking protocols like Dante, allowing flexible, dynamic routing of data between transmitters (`@tx`) and receivers (`@rx`).

## Basic Operators

### Switch Operators
- **Managed Switch**: `(|::::|):`
  - Managed switches handle dynamic subscriptions.

- **Unmanaged Switch** (`|::::|`) (no additional management).

### Transmitter and Receiver Operators
```mida
@rx -> /\/  // receiver pins
@tx -> <>   // transmitter pins
```

## Subscription Syntax
- `->` or `<-` dynamically connects transmitter pins to receiver pins:
```mida
rx.01 <- tx.01
// equivalent to:
tx.01 -> rx.01
```

- `><` dynamically unsubscribes:
```mida
rx.01 >< tx.01
```

## Labeling Pins
Pins can have user-friendly labels:
```mida
@rx.01 *^> as Port.888
@tx.02 *^> as R
```

## Logging the Switch Status
- Use `<~*^` to log the current state of the switch:
```mida
(|::::|): 255.255.255.255
|00|
|00|

rx.01 <- tx.01
(|::::|): <~*^ 255.255.255.255 // logs the updated switch state
```

### Output:
```
|10|
|00|
```

## Unsubscribing with `><`
- Use the `><` operator to unsubscribe dynamically:
```mida
rx.01 >< tx.01
```

## Example
Here's a concise example demonstrating these features clearly:
```mida
(|::::|): 255.255.255.255
|00|
|00|

@rx -> /\/ { 01, 02 }
@tx -> <> {
    01, 02
}

@rx.01 *^> as Port.888
@tx.02 *^> as R

tx.R -> rx.Port.888
(|::::|): <~*^ // Output: |00| |10|

tx.01 >< rx.01
(|::::|): <~*^ // Output after unsubscribing: |00| |00|
```

## Key Points
- **Implicit Definitions**: Pins are implicitly created by the initial switch configuration (`|00| |00|`).
- **Labels**: Pins can be labeled for clarity, aiding readability.
- **Dynamic Routing**: Connections (`->`, `<-`) and disconnections (`><`) happen dynamically in the timeline.
- **Logging**: `<~*^` shows current routing subscriptions clearly.

---

This reference provides a clear foundation for understanding and using Mida’s Layer 3 networking syntax effectively.
