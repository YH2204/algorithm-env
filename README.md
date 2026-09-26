# ---------- 버블 정렬 ----------
def bubble_sort(arr):
    a = list(arr)
    n = len(a)
    for i in range(n - 1):
        swapped = False
        for j in range(n - 1 - i):
            if a[j] > a[j + 1]:
                a[j], a[j + 1] = a[j + 1], a[j]
                swapped = True
        if not swapped:  # 교환이 없으면 이미 정렬된 상태
            break
    return a


# ---------- 셸 정렬 (크누스 간격: 1, 4, 13, 40, ...) ----------
def shell_sort(arr):
    a = list(arr)
    n = len(a)

    h = 1
    while h < n // 3:
        h = 3 * h + 1

    while h >= 1:
        # 간격 h만큼 떨어진 원소끼리 삽입 정렬
        for i in range(h, n):
            item = a[i]
            j = i
            while j >= h and a[j - h] > item:
                a[j] = a[j - h]
                j -= h
            a[j] = item
        h //= 3
    return a


# ---------- 트리 정렬 ----------
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def insert(root, value):
    if root is None:
        return Node(value)
    if value < root.value:
        root.left = insert(root.left, value)
    else:  # 같은 값은 오른쪽으로 (안정 정렬)
        root.right = insert(root.right, value)
    return root


def inorder(root, result):
    if root is not None:
        inorder(root.left, result)
        result.append(root.value)
        inorder(root.right, result)


def tree_sort(arr):
    root = None
    for x in arr:
        root = insert(root, x)
    result = []
    inorder(root, result)
    return result


# ---------- 실행 예시 ----------
if __name__ == "__main__":
    data = [8, 5, 3, 7, 6, 2, 4, 1]
    print("원본:", data)
    print("버블:", bubble_sort(data))
    print("셸  :", shell_sort(data))
    print("트리:", tree_sort(data))
