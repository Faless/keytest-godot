Issue Explaination
---

Godot now keeps an internal state for every action, and sets it as pressed or released when parsing events.
The problem is that to check **if the action is released modifiers are counted** (which shouldn't happen).

InputMap:
--

"action_a" -> key "A", modifiers == none
"action_shift" -> key "Shift", modifiers == none
"action_shift_a" -> key "A", modifiers = Shift+a

Usage 1
--

User press: A -> action_a is pressed (keycode == A, modifiers == none)

press Shift -> action_shift is pressed (keycode == Shift)

release A (while still holding shift) -> action_a will stay pressed because the release event will be for shift+A and not A so the action will not be marked as released. (keycode == A, modifiers == shift)

Usage 2
--

User press Shift+A -> action_shift_a is pressed

release Shift -> action_shift_a is now stuck
