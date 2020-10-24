# Python Notation

1. list.sort(cmp=None, key=None, reverse=False)
   sorted(iterable, cmp=None, key=None, reverse=False)
   cmp -- 可选参数, 如果指定了该参数会使用该参数的方法进行排序。
   key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
   reverse -- 排序规则，reverse = True 降序， reverse = False 升序（默认）

2. python list.pop() == java ArrayList.remove()

   python list.append(a) == java ArrayList.add(a)

   python list(list) = new ArrayList<T>(arraylist)

3. set 初始化 set()

   ​      增加 add(a)

   ​      删除 remove(a)

4. 选出原list符合条件的数重新构造list: `left = [v for v in nums if v < nums[0]]`

5. 计算C(n, k) : `math.comb(n, k)`

6. python dict = java hashmap

