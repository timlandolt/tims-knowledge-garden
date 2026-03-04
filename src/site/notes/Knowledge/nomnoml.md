---
{"dg-publish":true,"permalink":"/knowledge/nomnoml/"}
---


---
A tool to create cool [[UML\|UML]] diagrams:

[nomnoml](https://www.nomnoml.com/)

## Example

```js
#background:#FDF6E3

#.box: fill=#8f8 dashed
[<box>
	[<start>start] -> [<state>plunder] -> [<choice>more loot] -> [start]
	[more loot] no ->[<end>e]
]

[Pirate|
  [beard]--[parrot]
  [beard]-:>[foul mouth]
]

[<table>mischief| bawl | sing || yell | drink ]

[<abstract>Marauder]<:--[Pirate]
[Pirate] - 0..7[mischief]
[<actor id=sailor>Jolly;Sailor]
[sailor]->[Pirate]
[sailor]->[rum]
[Pirate]-> *[rum |
	tastiness: Int |
	swig()
]

```

```nomnoml
#background:#FDF6E3

#.box: fill=#8f8 dashed
[<box>
	[<start>start] -> [<state>plunder] -> [<choice>more loot] -> [start]
	[more loot] no ->[<end>e]
]

[Pirate|
  [beard]--[parrot]
  [beard]-:>[foul mouth]
]

[<table>mischief| bawl | sing || yell | drink ]

[<abstract>Marauder]<:--[Pirate]
[Pirate] - 0..7[mischief]
[<actor id=sailor>Jolly;Sailor]
[sailor]->[Pirate]
[sailor]->[rum]
[Pirate]-> *[rum |
	tastiness: Int |
	swig()
]

```

