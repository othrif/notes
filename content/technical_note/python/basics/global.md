---
title: "Alter variable defined in global scope"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
the keyword global within a function to alter the value of a variable defined in the global scope.


```python
team = "teen titans"

def change_team():
    """Change the value of the global variable team."""
    global team
    team = 'justice league'
    

print(team)
change_team()
print(team)
```

    teen titans
    justice league

