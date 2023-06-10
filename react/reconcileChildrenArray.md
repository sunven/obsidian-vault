第一次遍历
- 从第一个开始找连续的可复用的链表
新的遍历完
- 剩下老节点视为删除, 标记Deletion
老的遍历完
- 剩下新节点视为新增, 标记Placement
第二次遍历
- 从剩下的老fiber中找可复用的fiber

![[reconcileChildrenArray.drawio.svg]]