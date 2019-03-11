---
title: "JS Snippets & Notes"
published: true
---

## Modify inner object with array of subscripts / path programmatically

```js
function saveCurrentValue (profile, path, value) {
    let getReference = (object, subscripts) => {
        if (subscripts.length <= 1) {
            object[subscripts[0]] = value
            return
        }
        if (!object[subscripts[0]]) { object[subscripts[0]] = {} }
        getReference(object[subscripts[0]], subscripts.splice(1))
    }
    getReference(profile, path.split('/properties/').splice(1))
}
```
