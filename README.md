# CastModifier

This addon allows you to use a small subset of the macro conditionals, first introduced in the TBC expansion, in your 1.12.1 Vanilla client.

(Outdated) Demo video:

[![Example Video](https://img.youtube.com/vi/R5wtyhUbaLs/0.jpg)](https://www.youtube.com/watch?v=R5wtyhUbaLs)

### Installation

  - [Download](https://github.com/DennisWG/CastModifier/archive/master.zip) the latest version of CastModifier directly from the repository and extract it into your `WoW/Interface/AddOns/` folder.
  - Rename `CastModifier-master` to `CastModifier`
  - Run World of Warcraft and make sure to enable this addon in the character select screen

## Conditionals

### Branching

Since every Conditional may fail, it might be desireable to have the ability to specify an alternative Conditional to check or a fallback ability to cast. This allows the user to chain together a set of Conditionals in an 'if-else' equivalent branch. For example:
```lua
/cast [mod:ctrl] Healing Wave; Healing Wave (Rank 1)
```
If CTRL is pressed the highest rank of Healing Wave will be casted. If it isn't rank 1 will be casted instead. You may chain together as many Conditionals as you want by just separating them with semicolons:
```lua
/cast [mod:ctrl] Healing Wave; [mod:alt] Windfury Totem; [mod:shift] Healing Wave (Rank 3); Frost Shock
```

Note, that you may use any spell you want within each Conditional. Also, there mustn't be a whitespace character after each semicolon. You may use them to improve readability.

### mod:ctrl/shift/alt

Modifier keys are a convenient way to save action bar space and make certain decisions.

Example:
```lua
/cast [mod:ctrl] Healing Wave; Healing Wave (Rank 1)
```

This will cast your highest rank of Healing Wave whenever you have the CTRL key pressed, otherwise Healing Wave rank 1.

### help / harm

The [help] condition is true when the unit can receive a beneficial effect, e.g., a healing spell. The [harm] condition is true when the unit would get an adverse effect, e.g., a damaging spell.

Example:
```lua
/cast [harm] Frost Shock; [help] Healing Wave
```

This will cast Frost Shock on hostile targets and Healing Wave on friendly targets.

### target=[UnitID](http://wow.gamepedia.com/index.php?title=UnitId&oldid=204442)

Sets the target of the spell. Can be any valid Unit ID, including 'mouseover'. However, 'mouseover' currently still requires the use of the ClassicMouseover addon. I'll integrate this part into the addon if I ever find the time for it.

Example:
```lua
/cast [harm target=target] Frost Shock; [help target=mouseover] Healing Wave
```

You will cast Frost Shock on your current target if it is considered hostile. If it isn't and your mouseover target is considered friendly, your character will cast Healing Wave on your mouseover target instead.

### Combining Conditionals

In the previous example I've made use of the feature of combining Conditionals. You're able to combine one Conditional of each category to create an 'and' equivalent conjunction, by adding additional Conditionals, seperated by white spaces, into the brackets.

Example:
```lua
/cast [mod:ctrl harm target=player] Holy Light
```

You will only cast Holy Light if you have CTRL pressed and the target is hostile. It will also target yourself.

### Todos

 - Write Tests
 - Implement proper mouseover targeting
 - Add Code Comments

License
----

MIT

