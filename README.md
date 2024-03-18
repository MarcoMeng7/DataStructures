# DataStructures
堆積（Heap）是一種特殊的樹狀資料結構，通常用來實現優先佇列。
在堆中，每個節點都有一個值，通常以陣列的形式儲存，並且滿足堆屬性：對於任意給定節點 i，父節點的值小於或等於子節點的值（最小堆），或者父節點的值大於或等於子節點的值（最大堆）。
以下是一段Python程式，實現了一個最小堆，併包含插入和提取最小值的功能。
class MinHeap:
    def __init__(self):
        self.heap = []

    def insert(self, val):
        self.heap.append(val)
        self._bubble_up(len(self.heap) - 1)

    def extract_min(self):
        if not self.heap:
            return None
        if len(self.heap) == 1:
            return self.heap.pop()
        min_val = self.heap[0]
        self.heap[0] = self.heap.pop()
        self._sink_down(0)
        return min_val

    def _bubble_up(self, idx):
        while idx > 0:
            parent_idx = (idx - 1) // 2
            if self.heap[parent_idx] > self.heap[idx]:
                self.heap[parent_idx], self.heap[idx] = self.heap[idx], self.heap[parent_idx]
                idx = parent_idx
            else:
                break

    def _sink_down(self, idx):
        while 2 * idx + 1 < len(self.heap):
            left_child_idx = 2 * idx + 1
            right_child_idx = 2 * idx + 2 if 2 * idx + 2 < len(self.heap) else None
            min_child_idx = left_child_idx
            if right_child_idx is not None and self.heap[right_child_idx] < self.heap[left_child_idx]:
                min_child_idx = right_child_idx
            if self.heap[idx] > self.heap[min_child_idx]:
                self.heap[idx], self.heap[min_child_idx] = self.heap[min_child_idx], self.heap[idx]
                idx = min_child_idx
            else:
                break

#heap = MinHeap()
heap.insert(5)
heap.insert(3)
heap.insert(8)
heap.insert(1)
print("Extracted min value:", heap.extract_min())  # 输出最小值
print("Extracted min value:", heap.extract_min())  # 输出最小值


