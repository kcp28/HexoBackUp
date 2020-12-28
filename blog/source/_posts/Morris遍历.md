---
title: Morris中序遍历
date: 2020-09-24 15:46:27
categories: 算法
tags:
- Morris遍历
---

Morris遍历是遍历二叉树的一种方式，它能够以o(n)的时间复杂度和o(1)的空间复杂度实现二叉树的遍历。该文主要介绍Morris中序遍历。

Morris遍历的关键就是找前驱。<!--more-->

<b>算法思想：</b>

设当前节点为cur。

1.当cur左孩子为空时，处理当前结点，并遍历右子树。

2.当cur左孩子不为空时。找到cur的前驱节点pre。中序遍历时，当前节点的前驱节点就是<b>当前节点的左子树的最右的结点</b>。

​	1）当前驱结点pre的右孩子为空时。让pre的右孩子指向当前节点，然后遍历cur的左子		   树。

​	2）当前驱结点pre的右孩子不为空时，将pre的有孩子重新置为空(恢复原树)，然后处理当前节点并遍历右子树。

<b>c语言代码：</b>

```c
//寻找node结点的前驱结点
 struct TreeNode* findPre(struct TreeNode* node){
    struct TreeNode* pre=node->left;//pre：node的前驱节点
     //中序遍历时，当前结点的前驱节点就是它左子树的最右结点
    while(pre->right && pre->right!=node){
        pre=pre->right;
    }
    return pre;
 }
 void Morris(struct TreeNode* root){
    struct TreeNode* cur=root;//cur:当前的节点
    struct TreeNode* pre=NULL;//前驱
    while(cur!=NULL){
        if(!cur->left){//当前结点的左孩子为空，即没有左子树时
            //处理当前节点
            printf("%d ",cur->val);
            cur=cur->right;//遍历右子树
        }else{//当前结点有左孩子
            pre=findPre(cur);//寻找当前节点的前驱节点
            if(!pre->right){//前驱节点的右孩子为空
                pre->right=cur;//让前驱右孩子指向当前结点
                cur=cur->left;//遍历左子树
            }else{//前驱结点的有孩子不为空，即指向了当前节点
                pre->right=NULL;//将前驱右孩子置空，恢复原树
                //处理当前节点
                printf("%d",cur->val);
                cur=cur->right;//遍历右孩子
            }
        }
    }
 }
```

