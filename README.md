# 有用的 python 代码片段 
字符同时替换
```
adapter = 'aattc'
r_adapter = adapter.translate(str.maketrans('ACGTacgt', 'TGCAtgca'))
print(r_adapter) # 'tttaag' 同perl tr///
```
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
csv文件去特殊符号开头行（##）
```
def decomment(csvfile):
    for row in csvfile:
        raw = row.split('##')[0].strip()
        if raw: yield raw
with open('test.tsv','r') as IN：
    f_csv = csv.reader(decomment(IN),delimiter='\t')
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
字典构造（双列表）
```
a = ['apple','orange','banana']
number = [1,2,3] 
new_dict = dict(zip(a,number))
print(new_dict) # {'apple': 1, 'orange': 2, 'banana': 3}
```
带参数的装饰器
```
import time
class logger(object):
    def __init__(self, level='INFO'):
        self.level = level
    def __call__(self, func): # 接受函数
        def wrapper(*args, **kwargs):
            print(f'[{self.level}]',time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
            func(*args, **kwargs)
            print(f'[{self.level}]',time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
        return wrapper  #返回函数

@logger(level='time')
def say():
    print('yes')
say()
```
