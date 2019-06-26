---
title : heap 구조
date : 2019-06-26
category : algorithm
---
# heap

- 아래와같은 조건을 만족시키는 구조가 힙
  - 부모노드의 값은 항상 자식노드의 값 이상이다.
  - 각 레벨에서 비워져있는 곳이 있다면 다음레벨에 넣지 않는다.

## heap구조의 구현

## 요구기능

1. 힙의 생성
2. 요소의 추가
   - 힙 구조를 먼저 만족시키고 자신의 자리를 찾아가는 방식. 먼저 젤 뒤에 넣고 부모와 값 비교후 교환
3. 요소의 삭제
   - 뺴고싶은 값을 빼고 그자리에 젤 뒤에 요소를 삽입. 그 후 자식들과 비교하며 자리를 바꿔 제자리를 찾아가는 방식
4. 힙 정렬
   - 루트가 항상 최고의 값이기 때문에 루트를 빼고 힙구조 만족시킨후, 또 빼고 힙구조 만족시키는 형태

### 힙 구현

- 요소 추가 기능을 넣고 n개의 배열을 다 추가하는 방식으로 먼저 구현.

```c
#include <iostream>
class heap{
private:
    int end;
    void popchange(int array[],int target){     if(array[target]>=array[target*2+1]&&array[target]>=array[target*2+2]){
            return;
        }
        else{
            int newtarget = array[target*2+1]>array[target*2+2]?target*2+1:target*2+2;
            int tmp = array[newtarget];
            array[newtarget]=array[target];
            array[target]=tmp;
            popchange(array,newtarget);
        }
    }
    void change(int child,int * array){
        if(child==1){
            return;
        }
        else if(array[child]>array[child/2]){
            int tmp = array[child/2];
            array[child/2]=array[child];
            array[child]=tmp;
            change(child/2,array);
            return;
        }
        else return;
    }
public:
    heap(){
        end = 0;
    }
    void push(int array[],int inp){
        array[++end]=inp;
        change(end,array);
    }

    void print(int array[]){
        for(int i=1;i<=end;i++){
            printf("%d ",array[i]);
        }
        printf("\n");
    }
    void pop(int array[],int target){
        array[target]=array[end];
        array[end--]=0;
        popchange(array,target);
    }
};
int main() {
    int array[100];
    heap heap1 = heap();
    heap1.push(array,7);
    heap1.print(array);
    heap1.push(array,15);
    heap1.print(array);
    heap1.push(array,27);
    heap1.print(array);
    heap1.push(array,19);
    heap1.print(array);
    heap1.push(array,12);
    heap1.print(array);
    heap1.push(array,14);
    heap1.print(array);
    heap1.push(array,32);
    heap1.print(array);
    heap1.pop(array,1);
    heap1.print(array);
    return 0;
}
```



