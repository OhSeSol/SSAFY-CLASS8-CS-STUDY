# Array VS Array List VS Linked List

# Array

- 많은 수의 데이터를 다룰 때 사용하는 자료구조
- 각 데이터와 인덱스를 1:1로 대응
- 데이터가 메모리에 연속적으로 저장

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled.png)

## Array 장점

- Index를 이용하여 접근 속도 빠름 ⇒ 시간복잡도 O(1)
- 초기화시 메모리에 할당되어 속도가 빠르다.

## Array 단점

- 고정 길이 : 미리 최대 길이를 정해서 생성

## 사용법

```java
import java.util.Arrays;

public class ArrayTest{
	public static void main(String[] args) {

//      1차원 배열
        int[] arr; //배열 선언
				arr = new int[5]; //배열 초기화
				//값을 설정하지 않으면 기본값으로 초기화 [0, 0, 0, 0, 0]

				//선언과 동시에 값 설정 가능
				int[] arr2 = {1, 2, 3, 4, 5};

				//배열 길이 확인
				System.out.println(arr.length);
				//결과: 5
				
				//인덱스를 활용한 접근
        arr[1] = 100;
        System.out.println("arr[1] = " + arr[1]);
				//결과: "arr[1] = 100"

				//배열의 출력 1:반복문을 사용하는 방법
				for (int i : arr) {
            System.out.print(i +" ");
        }
				//결과: 0 100 0 0 0
        System.out.println();

				//배열의 출력 2:Arrays.toString() 
				System.out.println(Arrays.toString(arr));
				//결과: [0, 100, 0, 0, 0]

//      2차원 배열
        int[][] arr3 = {{1, 2, 3}, {4, 5, 6}};
        System.out.println(arr3[0][1]);
				//결과: 2

        for(int[] row: arr2) {
            for(int item: row) {
                System.out.print(item +" ");
            }
						System.out.println();
        }
				/*
				결과 : 1 2 3
						   4 5 6
				*/
	}
}
```

## Array 복사

### 얕은 복사 VS 깊은 복사

**얕은 복사** 

- 객체의 주소 값을 복사(원본과 복사본이 같은 주소값을 가리킴)
- 원본이 변경되면 복사본도 변경
    
    ![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%201.png)
    

```java
public class ArrayCopy {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};
        int[] b = a;

        System.out.println("int[] a = "+Arrays.toString(a));
				//결과: int[] a = [1, 2, 3, 4, 5]
        System.out.println("int[] b = "+Arrays.toString(b));
				//결과: int[] a = [1, 2, 3, 4, 5]

        a[2] = 200;
        System.out.println("int[] a = "+Arrays.toString(a));
				//결과: int[] a = [1, 2, 200, 4, 5]
        System.out.println("int[] b = "+Arrays.toString(b));
				//결과: int[] a = [1, 2, 200, 4, 5]

    }
}
```

**깊은 복사**

- 객체의 실제값을 새로운 객체로 복사
- 원본을 변경해도 복사본이 변경되지 않음

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%202.png)

```java
public class ArrayCopy {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};
        int[] b = a.clone();

        System.out.println("int[] a = "+Arrays.toString(a));
				//결과: int[] a = [1, 2, 3, 4, 5]
        System.out.println("int[] b = "+Arrays.toString(b));
				//결과: int[] a = [1, 2, 3, 4, 5]

        a[2] = 200;
        System.out.println("int[] a = "+Arrays.toString(a));
				//결과: int[] a = [1, 2, 200, 4, 5]
        System.out.println("int[] b = "+Arrays.toString(b));
				//결과: int[] a = [1, 2, 3, 4, 5]

    }
}
```

# Array List

- 인덱스로 객체를 관리한다는 점에서  Array와 동일하지만, 크기를 동적으로 늘릴 수 있음
- Array는 초기화할 때 크기를 지정해야 하지만, ArrayList는 그러지 않아도 된다.
- 인덱스를 사용하기에 데이터 참조 시간복잡도 = O(1)
- 데이터를 중간에 삽입하면 새로운 배열을 복사하고 삽입된 자리 이후의 데이터는 인덱스 값이 1씩 증가(삭제 시 감소)  ⇒ 이러한 작업으로 시간복잡도 = O(n)

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%203.png)

## 자바로 Array List 구현해보기

```java
package programmers;

import java.util.Arrays;

public class MyArrayList {

    private int size = 0;

    private int[] arr = new int[0];

    public MyArrayList(){
    }

		//데이터 추가
    public void add(int data){
        arr = Arrays.copyOf(arr, size+1);
        arr[size++] = data;
    }

		//원하는 위치에 데이터 추가
    public void add(int idx, int data){

        if(idx<=size){
            int [] temp = new int[++size];

            for(int i=0; i<size; i++){
                if(i<idx){
                    temp[i] = arr[i];
                }else if(i==idx){
                    temp[i] = data;
                }else{
                    temp[i] = arr[i-1];
                }
            }
            arr = temp;
        }else{
            throw new ArrayIndexOutOfBoundsException();
        }

    }

		//데이터 참조
    public int get(int idx){
        if(idx<size){
            return arr[idx];
        }else{
            throw new ArrayIndexOutOfBoundsException();
        }
    }

		//리스트가 가진 데이터의 수 확인
    public int size(){
        return size;
    }

		//해당 인덱스의 데이터 삭제
    public void remove(int idx){
        if(idx<size){
            int[] temp = new int[size-1];
            for(int i=0; i<size-1; i++){
                if(i<idx){
                    temp[i] = arr[i];
                }else{
                    temp[i] = arr[i+1];
                }
            }
            arr = temp;
            size--;
        }else{
            throw new ArrayIndexOutOfBoundsException();
        }
    }

		//리스트 내 데이터의 유무 확인
    public boolean contains(int data){
        for(int i=0; i<size; i++){
            if(arr[i]==data){
                return true;
            }
        }
        return false;
    }

		//리스트 초기화
    public void clear(){
        arr= new int[0];
        size = 0;
    }

		
    public boolean isEmpty(){
        if(size==0){
            return true;
        }else{
            return false;
        }
    }

    @Override
    public String toString(){
        return Arrays.toString(arr);
    }
}
```

```java
public class MyArrayListTest {
    public static void main(String[] args) {
        MyArrayList arrayList = new MyArrayList();

        System.out.println("------------데이터 추가: 1------------");
        arrayList.add(1);
        System.out.println(arrayList.toString());
        System.out.println();

        System.out.println("------------데이터 추가: 2------------");
        arrayList.add(2);
        System.out.println(arrayList.toString());
        System.out.println();

        System.out.println("------------인덱스 1에 데이터 추가: 10------------");
        arrayList.add(1, 10);
        System.out.println(arrayList.toString());
        System.out.println("size= "+ arrayList.size());
        System.out.println();

        System.out.println("------------인덱스 1인 데이터 삭제------------");
        arrayList.remove(1);
        System.out.println(arrayList.toString());
        System.out.println("size= "+ arrayList.size());
        System.out.println();

        System.out.println("------------인덱스 1인 데이터 삭제------------");
        arrayList.remove(1);
        System.out.println(arrayList.toString());
        System.out.println("size= "+ arrayList.size());
        System.out.println();

        System.out.println("------------데이터 검색: 1------------");
        System.out.println(arrayList.contains(1));
        System.out.println();

        System.out.println("------------리스트 초기화------------");
        arrayList.clear();
        System.out.println(arrayList.toString());
    }
}
```

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%204.png)

## 의문이었던 부분

배열과 리스트의 차이를 설명하는 블로그에서 array list는 다차원이 불가능하다는 블로그가 있었는데 ArrayList<ArrayList<Integer>>는 다차원이 아닌것인지

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%205.png)

# Linked List

- 자료를 링크로 연결하여 관리하는 자료구조
- 자료의 순서는 정해져 있지만 메모리상 연속성이 보장되진 않음
- 데이터의 조회가 빈번한 경우 Array를, 삽입과 삭제가 빈번한 경우 Linked List 사용

## Linked List 종류

### Singly Linked List

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%206.png)

### Doubly Linked List(✨Collections가 사용하는 리스트)

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%207.png)

### Circular Linked List

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%208.png)

## Linked List 장점

- 리스트의 맨 앞/뒤에 자료를 삽입/삭제하는 경우 시간이 빠름 ⇒ 시간복잡도 O(1)

## Linked List 단점

- 다음 노드를 가리키는 포인터를 위한 별도의 메모리 공간 필요
- 데이터 접근 시 리스트를 순차적으로 탐색 ⇒ 시간복잡도 O(n)

## 자바로 Linked List 구현해보기(Singly)

```java
class Node{
    int data;
    Node next;

    public Node() {
    }

    public Node(int data, Node next) {
        this.data = data;
        this.next = next;
    }
}

public class MyLinkedList {
    Node head;
    Node tail;

    public MyLinkedList() {
    }

    public MyLinkedList(Node node) {
        this.head = node;
        this.tail = node;
    }

		//리스트가 비었는지 확인
    public boolean isEmpty(){
        if(head==null){
            return true;
        }else{
            return false;
        }
    }

		//리스트의 마지막에 데이터 추가
    public void add(int data){
        if(head==null){
            head = new Node(data, null);
            tail = head;
        }else{
            tail.next = new Node(data, null);
            tail = tail.next;
        }
    }

		//리스트의 처음에 데이터 추가
    public void addFirst(int data){
        Node temp = new Node(data, head);
        head = temp;
    }

		//리스트의 마지막 데이터 삭제
    public void remove(){
        if(isEmpty()){
            throw new NullPointerException();
        }else{
            Node cur = head;
            Node prev = null;
            while(cur.next!=null){
                prev = cur;
                cur = cur.next;
            }
            prev.next = null;
            tail = prev;
        }
    }

		//리스트의 처음 데이터 삭제
    public void removeFirst(){
        if(isEmpty()){
            throw new NullPointerException();
        }else{
            head = head.next;
        }
    }

		//검색
    public boolean contains(int data){
        if(isEmpty()){
            return false;
        }else{
            Node cur = head;
            while(cur!=null){
                if(cur.data==data){
                    return true;
                }else{
                    cur = cur.next;
                }
            }
        }
        return false;
    }

		//리스트 사이즈 출력
    public int size(){
        if(isEmpty()){
            return 0;
        }else{
            int cnt =1;
            Node cur = head;
            while(cur.next!=null){
                cnt++;
                cur = cur.next;
            }
            return cnt;
        }
    }

		//리스트 초기화
		public void clear(){
        head = null;
    }

    public void showData(){
        if(!isEmpty()){
            Node cur = head;
            System.out.print(cur.data+" ");
            while(cur.next!=null){
                cur = cur.next;
                System.out.print(cur.data+" ");
            }
            System.out.println();
        }else{
            System.out.println("no data");
        }
    }
}
```

```java
public class MyLinkedListTest {
    public static void main(String[] args) {
        MyLinkedList ll = new MyLinkedList();

        System.out.println("------------데이터 추가: 1,2,3------------");
        ll.add(1);
        ll.add(2);
        ll.add(3);
        ll.showData();
        System.out.println();

        System.out.println("------------데이터 검색: 2------------");
        System.out.println(ll.contains(2));
        System.out.println();

        System.out.println("------------처음에 데이터 추가: 0------------");
        ll.addFirst(0);
        ll.showData();
        System.out.println();

        System.out.println("------------마지막 데이터 삭제------------");
        ll.remove();
        ll.showData();
        System.out.println();

        System.out.println("------------처음 데이터 삭제------------");
        ll.removeFirst();
        ll.showData();
        System.out.println();

        System.out.println("------------리스트 크기 출력------------");
        System.out.println(ll.size());
				System.out.println();

        System.out.println("------------리스트 초기화------------");
        ll.clear();
        ll.showData();
    }
}
```

![Untitled](Array%20VS%20Array%20List%20VS%20Linked%20List%20baaaf406a6e9441cbbbb5d6dea56f3b0/Untitled%209.png)