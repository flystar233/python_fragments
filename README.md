# 有用的 python 代码片段 
```
a =[1,2,[3,4],[5,6,7,[8,9]]]
func = lambda x: [y for l in x for y in func(l)] if type(x) is list else [x]
func(a) #[1, 2, 3, 4, 5, 6, 7, 8, 9]

```
