---
{"dg-publish":true,"permalink":"/knowledge/apache-velocity-templates-in-jetbrains/"}
---


---

Velocity is a java based templating language. Used for Java MVC views.
It should also be usable for non-devs.

BUT: You can also write file Templates in JetBrains IDEs.

### Variables

```velocity
<html>
  <body>
  #set( $foo = "Velocity" )
  Hello $foo World!
  
  ## Alternatively:
  Hello ${foo} World!
  </body>
</html>
```

### If / Else
```velocity
#if( $foo < 10 )
    Output 1
#elseif( $foo == 10 )
    Output 2
#else
    Output
#end
```

### Loops
There is only the foreach loop

```velocity
<ul>
#foreach( $product in $allProducts )
    <li>$product</li>
#end
</ul>
```

But you can use ranges to emulate a regular for.

```velocity
#foreach($i in [1..$ITERATIONS])
  Item Number $i: This is a repeated block.
#end
```

## File Templates
In JetBrains IDEs you can create file templates using Velocity.

`Settings > Editor > File and Code Templates`

To get an Input, just reference an undeclared variable. Underscores get turned into spaces:

```velocity
Hello $Your_Name
```

![Pasted image 20260213073823.png](/img/user/Ressources/Pasted%20image%2020260213073823.png)
Sadly, it's not possible to get other inputs than text.

You can also use all the possibilities that Live Templates bring (like cursor positioning, tabbing through, enums, ...). > [Create live templates \| IntelliJ IDEA Documentation](https://www.jetbrains.com/help/idea/creating-and-editing-live-templates.html)

### Example: Stimulus Controller
**File name:**
```velocity
${Controller_Name.toLowerCase().replace(" ", "_")}_controller
```

```velocity
import { Controller } from "@hotwired/stimulus"

#set( $className = $Controller_Name.replace(" ", "") + "Controller" )
export default class $className extends Controller {
  #[[$END$]]#
}
```

#### Result
![Pasted image 20260213074814.png](/img/user/Ressources/Pasted%20image%2020260213074814.png)
```js
// hello_world_controller.js
import { Controller } from "@hotwired/stimulus"  
  
export default class HelloWorldController extends Controller {  
  |
}
```
