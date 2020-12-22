# 有用的 python 代码片段 
解列表嵌套
```
a =[1,2,[3,4],[5,6,7,[8,9]]]
func = lambda x: [y for l in x for y in func(l)] if type(x) is list else [x]
func(a) #[1, 2, 3, 4, 5, 6, 7, 8, 9]
```
读取fasta文件
```
def parseFasta(filename): #seq_api
    fas = {}
    idlis = []
    id = None
    with open(filename, 'r') as fh:
        for line in fh:
            if line[0] == '>':
                header = line[0:].rstrip()
                #header = line[1:].rstrip() # remove >
                id = header.split()[0]
                idlis.append(id)
                fas[id] = []
            else:
                fas[id].append(line.rstrip())
        for id, seq in fas.items():
            fas[id] = ''.join(seq)
    return fas #dict
```
字典点方法
```
class DottableDict(dict):
    def __init__(self, *args, **kwargs):
        dict.__init__(self, *args, **kwargs)
        self.__dict__ = self
    def allowDotting(self, state=True):
        if state:
            self.__dict__ = self
        else:
            self.__dict__ = dict()
a = {'apple':1,'orange':2}
new_a = DottableDict(a)
print(new_a.apple,new_a['orange']) # 1 2
```
