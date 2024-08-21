# 隊列概念
隊列可以並發地分派多個線程，並按指定的順序進行處理，將請求的數據放入隊列容器中，線程無需等待，當隊列處理完數據後，線程再準時來取數據即可。請求數據的線程只與這個隊列容器存在關係，處理數據的線程崩潰不會影響到請求數據的線程，隊列會將這份數據派給其他線程處理，它實現了解耦，提高效率。當在多個線程或進程之間需要安全地交換信息或共享資源時，就需要使用隊列。

## Python四種類型的隊列：

Queue：FIFO 即 first in first out 先進先出
LifoQueue：LIFO 即 last in first out 後進先出
PriorityQueue：優先隊列，級別越低，越優先
deque：雙端隊列

# Queue常用方法

    # -*- coding:utf-8 -*-
    from queue import Queue

    __author__ = 'Evan'


    def queue_usage(put_data):
        """
        Queue常用方法
        :param put_data: 放入的數據，列表或元組類型
        :return:
        """
        q = Queue(maxsize=3)  # 設置隊列上限為3

        for each in put_data:
            print(f'添加({each})到隊列')
            q.put(each)

        print(f'返回隊列的大小: {q.qsize()}')
        print(f'判斷隊列是否為空: {q.empty()}')
        print(f'判斷隊列是否滿了: {q.full()}')

        while not q.empty():
            print(f'取出：{q.get()}')
            q.task_done()  # 告訴隊列，這個數據已經使用完畢

        q.join()  # 阻塞調用線程，直到隊列中的所有任務被處理掉


    if __name__ == '__main__':
        queue_usage(put_data=[1, 2, 3])


## 输出结果：

![01](https://github.com/muchen0926/Data-structure-final-report/blob/main/%E8%BC%B8%E5%87%BA%E7%B5%90%E6%9E%9C1.png)

# 四種隊列使用方式

## 1. Queue 先進先出隊列

    # -*- coding:utf-8 -*-
    from queue import Queue

    __author__ = 'Evan'


    def fifo_queue(put_data):
        """
        FIFO，先進先出隊列
        :param put_data: 放入的數據，列表或元組類型
        :return:
        """
        assert isinstance(put_data, (list, tuple)), '請傳入列表或元組類型的put_data'

        # maxsize為隊列數據上限，小於或等於0則不限制，當容器數量大於這個數則阻塞，直到隊列中的數據被消掉
        q = Queue(maxsize=0)

        # 依次寫入隊列數據
        for each in put_data:
            print(f'添加({each})到隊列')
            q.put(each)

        print(f'當前隊列所有數據：{q.queue}')

        # 逐次取出所有數據
        while not q.empty():
            print(f'取出：{q.get()}')

        print(f'當前隊列所有數據：{q.queue}')


    if __name__ == '__main__':
        fifo_queue(put_data=[3, 2, 1])
        
## 輸出結果

![01](https://github.com/muchen0926/Data-structure-final-report/blob/main/Queue%20%E5%85%88%E9%80%B2%E5%85%88%E5%87%BA%E9%9A%8A%E5%88%97.png)

## 2. LifoQueue 後進先出隊列

    # -*- coding:utf-8 -*-
    from queue import LifoQueue

    __author__ = 'Evan'


    def lifo_queue(put_data):
        """
        LIFO，後進先出隊列
        :param put_data: 放入的數據，列表或元組類型
        :return:
        """
        assert isinstance(put_data, (list, tuple)), '請傳入列表或元組類型的put_data'

        # maxsize為隊列數據上限，小於或等於0則不限制，當容器數量大於這個數則阻塞，直到隊列中的數據被消掉
        q = LifoQueue(maxsize=0)

        # 依次寫入隊列數據
        for each in put_data:
            print(f'添加({each})到隊列')
            q.put(each)

        print(f'當前隊列所有數據：{q.queue}')

        # 逐次取出所有數據
        while not q.empty():
            print(f'取出：{q.get()}')

        print(f'當前隊列所有數據：{q.queue}')


    if __name__ == '__main__':
        lifo_queue(put_data=[3, 2, 1])

## 輸出結果

![01](https://github.com/muchen0926/Data-structure-final-report/blob/main/LifoQueue%20%E5%BE%8C%E9%80%B2%E5%85%88%E5%87%BA%E9%9A%8A%E5%88%97.png)

## 3. PriorityQueue 優先隊列

    # -*- coding:utf-8 -*-
    from queue import PriorityQueue

    __author__ = 'Evan'


    def priority_queue(put_data):
        """
        Priority，優先隊列，級別越低，越優先
        :param put_data: 放入的數據，列表或元組類型
        :return:
        """
        assert isinstance(put_data, (list, tuple)), '請傳入列表或元組類型的put_data'

        # maxsize為隊列數據上限，小於或等於0則不限制，當容器數量大於這個數則阻塞，直到隊列中的數據被消掉
        q = PriorityQueue(maxsize=0)

        # 依次寫入隊列數據
        for each in put_data:
            print(f'添加{each}到隊列，優先級別為：{each[0]}')
            q.put(each)

        print(f'當前隊列所有數據：{q.queue}')

        # 逐次取出所有數據，按優先級獲取
        while not q.empty():
            print(f'取出：{q.get()}')

        print(f'當前隊列所有數據：{q.queue}')


    if __name__ == '__main__':
        priority_queue(put_data=[(3, 'value1'), (1, 'value2'), (2, 'value3')])

## 輸出結果

![01](https://github.com/muchen0926/Data-structure-final-report/blob/main/PriorityQueue%20%E5%84%AA%E5%85%88%E9%9A%8A%E5%88%97.png)

## 4. deque 雙端隊列

    # -*- coding:utf-8 -*-
    from collections import deque

    __author__ = 'Evan'


    def deque_example(put_data):
        """
        Deque，雙端隊列
        :param put_data: 放入的數據，列表或元組類型
        :return:
        """
        assert isinstance(put_data, (list, tuple)), '請傳入列表或元組類型的put_data'

        # 放入數據到雙端隊列
        dq = deque(put_data)
        print(f'當前隊列所有數據：{dq}')
    
        # 增加數據到隊左
        dq.appendleft('aa')
        print(f'當前隊列所有數據：{dq}')

        # 增加數據到隊尾
        dq.append('cc')
        print(f'當前隊列所有數據：{dq}')

        print(f'移除隊尾，並返回：{dq.pop()}')
        print(f'移除隊左，並返回：{dq.popleft()}')

        print(f'當前隊列所有數據：{dq}')


    if __name__ == '__main__':
        deque_example(put_data=['a', 'b', 'c'])

## 輸出結果

![01](https://github.com/muchen0926/Data-structure-final-report/blob/main/deque%20%E9%9B%99%E7%AB%AF%E9%9A%8A%E5%88%97.png)
