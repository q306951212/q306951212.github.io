---
layout: post
title:  "基本算法"
date:   2017-10-16 15:03:26 +0800
author:     "陈杨"
header-img: "img/post-bg-2015.jpg"
categories: jekyll update
catalog: true
tags:
    - 学习
---

> “Yeah It's on. ”


## Hello algorithm！

## 基本排序算法

### 冒泡排序

原理分析:在要排序的一组数中，对当前还未排好的序列，从前往后对相邻的两个数依次进行比较和调整，让较大的数往下沉，较小的往上冒。
即，每当两相邻的数比较后发现它们的排序与排序要求相反时，就将它们互换。

{% highlight ruby %}
 function Bubble($arr)
    {
        //判断数组的长度
        $len = count($arr);
        //判断冒泡的轮数
        //如果数组中有三个数字，他们需要冒泡两次，有$len个数字，需要冒泡$len-1次
        for ($i = 1; $i < $len; $i++) {
            //判断每一轮需要冒出一个数字
            //需要比较数字，需从下标零开始,因为有[$k+1]因此不能取到最大值
            for ($k = 0; $k < $len - $i; $k++) {
                if ($arr[$k] > $arr[$k + 1]) {
                    $temp = $arr[$k];
                    $arr[$k] = $arr[$k + 1];
                    $arr[$k + 1] = $temp;
                }
            }
        }
        return $arr;
    }
{% endhighlight %}

### 选择排序

原理:在要排序的一组数中，选出最小的一个数与第一个位置的数交换。然后在剩下的数当中再找最小的与第二个位置的数交换，如此循环到倒数第二个数和最后一个数比较为止。

{% highlight ruby %}
    function SelectSort($arr){
        //查看数组的长度
        $len = count($arr);
        //外层的循环控制轮数，里层的循环控制比较的次数
        //这里的$i用0是为了表示前一个数
        for($i=0;$i<$len-1;$i++){
            //我们先假设第一个值是最小的值
            $p = $i;
            //我们用第一个值依次与后面的值做比较$j代表后一个数的值
            for($j=$i+1;$j<$len;$j++){
                if($arr[$p]>$arr[$j]){
                    $p = $j;
                }
            }
            //我们已经确认了最小值，如果顺序发生改变则$p != $i
            if($p != $i){
                $temp = $arr[$p];
                $arr[$p] = $arr[$i];
                $arr[$i] = $temp;
            }
        }
        print_r($arr);
    }
    {% endhighlight %}

### 插入排序

原理分析:在要排序的一组数中，假设第一个数是插入正确的，然后第二个数就要与第一个数做比较，第三个数就要与前面两个数做比较......

{% highlight ruby %}
function insertSort($arr){
    //查看数组的长度
    $len = count($arr);
    //需要从第二个数开始，因为至少要与第一个数做比较
    for($i = 1;$i<$len;$i++){
        $temp = $arr[$i];
        //比较插入的值
        for($j = $i-1;$j>=0;$j--){
            //然后我们进行比较
            if($temp < $arr[$j]){
                //交换顺序
                $arr[$j+1]=$arr[$j];
                $arr[$j] = $temp;
            }
        }
        break;
    }
    return $arr;
}
    {% endhighlight %}

### 快速排序

原理:选择一个基准元素，通常选择第一个元素或者最后一个元素。通过一趟扫描，将待排序列分成两部分，一部分比基准元素小，一部分大于等于基准元素。此时基准元素在其排好序后的正确位置，然后再用同样的方法递归地排序划分的两部分。

    {% highlight ruby %}
    function quickSort($arr){
        //先判断数组的个数
        $len = count($arr);
        //判断是否执行以下操作
        if($len<=1){
            return $arr;
        }
        //选择一个元素作为基准元素
        $base_num = $arr[0];
        //初始化左右两个数组
        $left_array = array();
        $right_array = array();
        //剩下的数组的元素进行比较分类
        for($i = 1;$i < $len;$i++){
            if($base_num>$arr[$i]){
                $left_array[] = $arr[$i];
            }
            else{
                //放在基准元素的右边
                $right_array[] = $arr[$i];
            }
        }
        $left_array = $this->quickSort($left_array);
        $right_array = $this->quickSort($right_array);
        return array_merge($left_array,array($base_num),$right_array);

    }
    {% endhighlight %}

## 基本查找算法

### 顺序查找
原理:通过循环数组查找对应的值
        {% highlight ruby %}
    function seqSearch($arr,$k){
        foreach($arr as $key=>$val){
            if($val==$k){
                return $key;
            }
        }
        return -1;
    }
          {% endhighlight %}


### 二分法查找
原理:二分法是依靠数组是有序序列进行排序，先判断是否是最小值和最大值，如果不是，则取中间的值判断大小。

    {% highlight ruby %}
    function binSearch($arr,$num){
        //计算数组的个数
        $len = count($arr);
        //数组最小值索引
        $lower = 0;
        //数组最大值索引
        $high = $len-1;
        global $i;

        //当最大值的索引于最小值的索引相等或小于的时候
        while($lower<=$high){
            $i++;
            //查询的值是都是最小值
            if($arr[$lower] == $num){
                return $lower;
            }
            if($arr[$high] == $num){
                return $high;
            }
            //如果都不是，则使用折半查询
            $middle = intval(($lower + $high) / 2);
            if($num < $arr[$middle]){
                $high = $middle - 1;
            }
            if($num > $arr[$middle]){
                $lower = $middle + 1;

            }
            else{
                return $middle;
            }

        }
        return -1;
    }
      {% endhighlight %}



