# 隊列概念
隊列可以並發地分派多個線程，並按指定的順序進行處理，將請求的數據放入隊列容器中，線程無需等待，當隊列處理完數據後，線程再準時來取數據即可。請求數據的線程只與這個隊列容器存在關係，處理數據的線程崩潰不會影響到請求數據的線程，隊列會將這份數據派給其他線程處理，它實現了解耦，提高效率。當在多個線程或進程之間需要安全地交換信息或共享資源時，就需要使用隊列。

## Python四種類型的佇列：

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

