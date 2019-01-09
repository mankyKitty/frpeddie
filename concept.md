# The General Idea

> I have a display with 2 elements, which are based on some input streams common
> to both and some input streams unique to each. If one does something
> complicated that takes a second or two to finish, can the program be written
> so that the other one continues to update promptly?
> - curiosity kitty

### Conceptually

#### Inputs

`{f,g,i}`

- `f`: Thread reading from `/dev/random` 
- `g`: Tick value (sine curve of UNIX epoch?)
- `i`: Process info (shell out, using given PID)

#### Displays

`{A, B}`

- `A` : `{f,g}`
- `B` : `{g,i}`

Inputs are displayed independently and as some sort of function over both.

#### Interaction

`Pause {f|i}`: Send a sleep to the input stream to simulate complex operation.
Display that does not require this input should continue unaffected.

`Capture {A|B}`: Trigger a capture where input is stopped and accumulated for a
set duration before displaying a result. Other display should continue unaffected.
